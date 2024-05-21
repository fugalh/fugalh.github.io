---
layout: post
status: publish
published: true
title: Prepend the Area Code with Asterisk
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 100
wordpress_url: urn:uuid:58ed53d0-b783-443b-9c99-38f101a454f9
date: '2006-03-29 10:18:10.000000000 -08:00'
tags:
- voip
comments: []
---
<p>If you want to prefix the area code for 7-digit numbers with Asterisk, it
usually looks like something like this:</p>

<pre><code>ext =&gt; _NXXXXXX,1,goto(505${EXTEN},1)
</code></pre>

<p>But if you need to server all area codes dynamically, you can do something like
this:</p>

<pre><code>ext =&gt; _NXXXXXX,1,goto(${CALLERID(number):0:3}${EXTEN},1)
</code></pre>

<p>This assumes caller id is set, and that your callers are using standard
PSTN-like DIDs.</p>
