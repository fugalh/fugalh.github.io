---
layout: post
status: publish
published: true
title: X-Sendfile
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 895
wordpress_url: urn:uuid:9d420050-a39a-41e3-9360-5cbc67a0d525
date: '2007-11-05 14:01:00.000000000 -08:00'
tags:
- rails
- ruby
- x-sendfile
- http
- performance
comments:
- id: 1637
  author: fankai@gmail.com
  author_email: ''
  author_url: ''
  date: '2008-01-07 23:06:29 -0800'
  date_gmt: ''
  content: |-
    <p>Hi, Hans</p>

    <p>I met the problem as you describing. I find your patch file does not match the source code of mod_fastcgi.c in lighttpd-1.4.18. Such as:</p>

    <p>these line is not exists in mod_fastcgi.c:</p>

    <pre><code>-                                       log_error_write(srv, __FILE__, __LINE__, "sb",
    -                                    "send-file error: couldn't get stat_cache entry for:",
    </code></pre>

    <p>This make patch process fail, command info is:</p>

    <pre><code>patching file mod_fastcgi.c
    Hunk #1 FAILED at 2530.
    Hunk #2 FAILED at 59.
    2 out of 2 hunks FAILED -- saving rejects to file mod_fastcgi.c.rej
    </code></pre>

    <p>Could you give me some advice? Thank your very much!</p>

    <p>Robbin Fan</p>
---
<p>I'm writing a little photo gallery of my own, because everything out there stinks. But sending big images files in Rails (using <code>send_file</code> and <code>send_data</code>) is slow, mostly because you tie up a whole rails process just feeding data to the web. Web servers like Apache, Lighttpd, and Mongrel are good at serving static files, let them do it.</p>

<p>That's the idea behind X-Sendfile. If you send an X-Sendfile header with the path of the file you want to send, then a supporting webserver will do the dirty work and do it fast, and you can get on with serving other requests.</p>

<p>That's the theory anyway, but there's some bumps in the road. First, AFAICT
mongrel doesn't support X-Sendfile. This is fine when mongrel is running behind
an Apache proxy which does, but kind of throws a wet blanket on development and
apachephobes like myself. Ok, apachephobe might be a bit strong, but I don't
want to set that monster on my laptop just for some rails development. So mongrel's out. Correct me if I'm wrong.</p>

<p>Lighttpd supposedly invented X-Sendfile, but 1.4.x and earlier don't seem to
support it. Instead, you have to use the header X-LIGHTTPD-send-file. Also, it
doesn't work unless Content-Length is properly set (or perhaps if it's absent).
This is bad news for rails users, since a bug in rails causes the
Content-Length header to be set to the content, which is not the file. If you
do <code>render :nothing =&gt; true</code>, then the content is one space character, and the
Content-Length is 1, and Lighttpd defiantly refuses to fix it. So you either
have to work around the rails bug, or upgrade to lighttpd version 1.5.x (now in
release candidate) which supposedly works (I haven't tested it—I can't get it
to compile on Leopard). I say bug in rails, but frankly I'm more inclined to
consider this bad behavior on the part of lighttpd. In that vein, here is a
patch for lighttpd version 1.4.18 that will enable both X-LIGHTTPD-send-file
and X-Sendfile headers with rails 1.2.3 which has the Content-Length resetting
behavior. It makes lighttpd set the Content-Length on its own. Thanks to
stbuehler for the patch.</p>

<pre><code>--- src/mod_fastcgi.c.orig      2007-11-05 13:52:47.000000000 -0700
+++ src/mod_fastcgi.c   2007-11-05 13:55:17.000000000 -0700
@@ -2530,22 +2530,28 @@
                }

                if (host-&gt;allow_xsendfile &amp;&amp;
-                                   NULL != (ds = (data_string *) array_get_element(con-&gt;response.headers, "X-LIGHTTPD-send-file"))) {
+                                   ((NULL != (ds = (data_string *) array_get_element(con-&gt;response.headers, "X-LIGHTTPD-send-file")))
+                                     || (NULL != (ds = (data_string *) array_get_element(con-&gt;response.headers, "X-Sendfile"))))) {
                    stat_cache_entry *sce;

                                         if (HANDLER_ERROR != stat_cache_get_entry(srv, con, ds-&gt;value, &amp;sce)) {
-                                               /* found */
-                                                con-&gt;parsed_response &amp;= ~HTTP_CONTENT_LENGTH;
-
+                                               data_string *dcls = data_string_init();
+                                                /* found */
                        http_chunk_append_file(srv, con, ds-&gt;value, 0, sce-&gt;st.st_size);
                        hctx-&gt;send_content_body = 0; /* ignore the content */
                        joblist_append(srv, con);
-                                       }
-                                        else
-                                        {
-                                               log_error_write(srv, __FILE__, __LINE__, "sb",
-                                                       "send-file error: couldn't get stat_cache entry for:",
-                                                       ds-&gt;value);
+
+                                               buffer_copy_string_len(dcls-&gt;key, "Content-Length", sizeof("Content-Length")-1);
+                                               buffer_copy_long(dcls-&gt;value, sce-&gt;st.st_size);
+                                               dcls = (data_string*) array_replace(con-&gt;response.headers, (data_unset *)dcls);
+                                               if (dcls) dcls-&gt;free((data_unset*)dcls);
+
+                                               con-&gt;parsed_response |= HTTP_CONTENT_LENGTH;
+                                               con-&gt;response.content_length = sce-&gt;st.st_size;
+                                       } else {
+                                               log_error_write(srv, __FILE__, __LINE__, "sb",
+                                                       "send-file error: couldn't get stat_cache entry for:",
+                                                       ds-&gt;value);
                                         }
                }
--- src/response.c.orig 2007-11-05 14:08:26.000000000 -0700
+++ src/response.c      2007-11-05 14:04:49.000000000 -0700
@@ -59,7 +59,8 @@
    ds = (data_string *)con-&gt;response.headers-&gt;data[i];

    if (ds-&gt;value-&gt;used &amp;&amp; ds-&gt;key-&gt;used &amp;&amp;
-                   0 != strncmp(ds-&gt;key-&gt;ptr, "X-LIGHTTPD-", sizeof("X-LIGHTTPD-") - 1)) {
+                   0 != strncmp(ds-&gt;key-&gt;ptr, "X-LIGHTTPD-", sizeof("X-LIGHTTPD-") - 1) &amp;&amp;
+                   0 != strncmp(ds-&gt;key-&gt;ptr, "X-Sendfile", sizeof("X-Sendfile") - 1)) {
            if (buffer_is_equal_string(ds-&gt;key, CONST_STR_LEN("Date"))) have_date = 1;
            if (buffer_is_equal_string(ds-&gt;key, CONST_STR_LEN("Server"))) have_server = 1;
</code></pre>

<p>Then, you need to configure your lighttpd server. Run <code>script/server lighttpd</code> once to generate <code>config/lighttpd.conf</code>, and add this bit to the <code>fastcgi.server</code> section:</p>

<pre><code>    "allow-x-send-file" =&gt; "enable"
</code></pre>

<p>Finally, use it—either by setting the X-Sendfile header manually or by using the rails <a href="http://john.guen.in/rdoc/x_send_file/"><code>x_send_file</code> plugin</a> (I recommend the latter).</p>

<p>Here's some links for more reading:</p>

<ul>
<li><a href="http://wiki.rubyonrails.org/rails/pages/HowtoSendFilesFast">HOWTO Send Files Fast</a></li>
<li><a href="http://john.guen.in/past/2007/4/17/send_files_faster_with_xsendfile/">Send files faster with X-Sendfile</a></li>
<li><a href="http://blog.lighttpd.net/articles/2006/07/02/x-sendfile">X-Sendfile</a> (for lighttpd 1.4.x—remember the correct Content-Length requirement and that Rails doesn't)</li>
<li><a href="http://blog.lighttpd.net/articles/2006/07/22/mod_proxy_core-got-x-sendfile-support"><code>mod_proxy_core</code> got X-Sendfile support</a> (for lighttpd 1.5.x—this looks really nice)</li>
<li><a href="http://dev.rubyonrails.org/ticket/7643">The Rails "bug"</a> that ruined X-Sendfile on lighttpd 1.4.x</li>
<li><a href="http://tn123.ath.cx/mod_xsendfile/"><code>mod_xsendfile</code></a> for Apache 2 (I haven't used it, but I assume it works fine)</li>
</ul>
