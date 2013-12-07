---
layout: post
status: publish
published: true
title: What is my IP?
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1031
wordpress_url: urn:uuid:81c32734-9f0e-44d7-8365-3291aa3e3f22
date: 2009-01-04 06:23:00.000000000 -08:00
tags:
- linux
- nat
- bash
- sh
- ip
- address
- curl
- php
- REMOTE_ADDR
comments:
- id: 2144
  author: IP Tejji
  author_email: ''
  author_url: http://www.tejji.com
  date: '2009-10-31 12:46:36 -0700'
  date_gmt: '2009-10-31 12:46:36 -0700'
  content: "You can also use below url\r\n\r\nhttp://www.tejji.com/ip/whatismyip.aspx\r\n\r\nThanks,\r\nIP
    Tejji"
---
<p>"What is my IP?" A frequent question while we all remain under the oppression of NAT. Of course most of you are familiar with <a href="http://whatismyip.com/">whatismyip.com</a> and friends, but did you know you can do the same thing yourself very easily? All you need is a webserver (across the NAT in question, of course).</p>

<p>Here's a CGI version:</p>

<pre><code>#!/bin/sh
echo "Content-type: text/plain"
echo
echo $REMOTE_ADDR
</code></pre>

<p>If CGI is a pain but you have PHP:</p>

<pre><code>&lt;?php
  header("Content-type: text/plain");
  echo $_SERVER['REMOTE_ADDR'];
?&gt;
</code></pre>

<p>Both of these are suitable for scripting, e.g.</p>

<pre><code>#!/bin/bash
URL=http://fugal.net/ip.cgi
echo Your IP address is `curl -s "$URL"`
</code></pre>
