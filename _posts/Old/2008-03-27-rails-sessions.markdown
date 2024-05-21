---
layout: post
status: publish
published: true
title: Rails Sessions
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 949
wordpress_url: urn:uuid:d99a157d-b9bf-415b-88b8-d2e9aea3afa0
date: '2008-03-27 09:05:00.000000000 -07:00'
tags:
- typo
- rails
- ruby
- session
- web
comments:
- id: 1736
  author: mmo
  author_email: KevFisk@hotmail.com
  author_url: http://http:/www.characterplanet.com
  date: '2008-04-21 00:20:06 -0700'
  date_gmt: ''
  content: <p>Yikes..thats a big strain from the db...glad you were able to resolve
    it</p>
---
<p>I was doing some maintenance on my blog, and was devastated to find that <a href="http://typosphere.org">Typo</a> was taking 225 megabytes of resident RAM. Yikes! After some creative debug thinking and digging I figured out it was due to sessions. Typo now stores sessions in the database, so my maintenance cron job to delete old sessions didn't clean up old sessions. (Ha! had you going for a second!)</p>

<p>Well I could write a cron job to run a script to clean the sessions out of the db, like:</p>

<pre><code>#!/bin/sh
sqlite3 /path/to/typo/db/production.db 'delete from sessions'
</code></pre>

<p>Ok, that's a bit extreme, but you get the idea. But when I deleted the sessions in this manner the memory usage didn't drop at all until I had restarted the server, which seems unnecessary. So instead I changed typo's configuration to use a different session store. I commented out this line in <code>config/environment.rb</code>:</p>

<pre><code>-  config.action_controller.session_store = :active_record_store
+  #config.action_controller.session_store = :active_record_store
</code></pre>

<p>Then I restarted the server and fired up a browser. "Huh, that's odd… no sessions in <code>tmp/sessions</code> or <code>/tmp</code> or anywhere I can see. No, they're not in the database…" What I was seeing didn't match up with what all the stuff Google said. The default session store was PStore, aka file system, so they said. But apparently that recently changed in Rails, and now the default is CookieStore. From <a href="http://rails.rubyonrails.com/classes/ActionController/Base.html">ActionController::Base documentation</a>:</p>

<blockquote>
    <p>Sessions are stored in a browser cookie that‘s cryptographically signed, but unencrypted, by default. This prevents the user from tampering with the session but also allows him to see its contents.</p>

    <p>Do not put secret information in session! </p>
</blockquote>

<p>Well a quick <code>grep -ri session app lib</code> told me that typo wasn't storing
anything secret, so I decided that default was alright with me. Now I don't
have to set up any session cleanup script at all. Sweet.</p>

<p>Now, don't stop there. You should set your session key and secret while you're
hanging out in <code>config/environment.rb</code>. Add the following lines in the same
place as the line you commented out above:</p>

<pre><code>config.action_controller.session['session_key'] = 'something unique'
config.action_controller.session['secret'] = 'get this from rake secret'
</code></pre>
