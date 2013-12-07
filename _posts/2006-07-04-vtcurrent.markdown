---
layout: post
status: publish
published: true
title: vtcurrent
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 659
wordpress_url: urn:uuid:cc08efb6-49b4-456a-924f-3d3152571e11
date: '2006-07-04 17:49:13.000000000 -07:00'
tags:
- linux
- vt
comments: []
---
<p>Have you ever wanted to know programatically which virtual terminal is the
current one? You know, so that you can have lirc toggle between vt 7 (regular
X) and vt 8 (Freevo). I couldn't figure out how to do this with available tools
so I dove in head first and figured out how to do it with <code>ioctl()</code>.</p>

<p><a href="http://hans.fugal.net/src/vtcurrent">http://hans.fugal.net/src/vtcurrent</a> is the code including Makefile, and utility functions from <a href="http://lct.sourceforge.net/">console-tools</a>.
<a href="http://hans.fugal.net/src/vtcurrent/vtcurrent.c"><code>vtcurrent.c</code></a> is the meat,
<a href="http://hans.fugal.net/src/vtcurrent/vtswitch.sh"><code>vtswitch.sh</code></a> is the end
result. </p>
