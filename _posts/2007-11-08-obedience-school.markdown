---
layout: post
status: publish
published: true
title: Send it to Obedience School
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 899
wordpress_url: urn:uuid:b5821776-4ca4-4ebf-8c84-5f780b2a9ba6
date: 2007-11-08 10:55:00.000000000 -08:00
tags:
- rails
- lighttpd
- mod_proxy
- mongrel
comments: []
---
<p>I have <a href="http://foton.fugal.net">a little rails app</a> that can have a lot of
images on each page. It worked fine in development, but when I went to deploy
it with mongrel behind apache's mod_proxy, it started behaving oddly. It would
randomly and inexplicably not serve up thumbnails. I checked all my code, the
thumbnails were being generated properly, and my code checked out. Apache would
complain with something like this:</p>

<pre><code>[error] proxy: error reading status line from remote server 127.0.0.1, referer: http://foton.fugal.net/album/detail/23
[error] proxy: Error reading from remote server returned by /foto/thumbnail/93, referer: http://foton.fugal.net/album/detail/23
</code></pre>

<p>Carefully watching my rails logs, I noticed they weren't mentioning the
offending files (that Apache was complaining about), so I guessed the problem
must be between Apache and my code, i.e. in Mongrel. So I fired it up with
Lighttpd instead of Mongrel, and lo and behold it worked fine. To be fair, I
didn't try upgrading Mongrel (from 1.0.1 to whatever's current—1.1 I think).
Maybe this is a fixed bug. But now you know it's Mongrel's fault, if you're
seeing something similar.</p>
