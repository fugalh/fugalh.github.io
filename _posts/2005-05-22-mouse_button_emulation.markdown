---
layout: post
status: publish
published: true
title: 3-button emulation on an iBook
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 79
wordpress_url: urn:uuid:555faa64-9f52-4800-a3f3-1e439a349941
date: '2005-05-22 09:10:11.000000000 -07:00'
tags:
- mac
comments: []
---
<p>Google is full of old information, or misinformation, about getting 3-button
emulation on an iBook. Here is the real story (for vanilla 2.6.11.10 on Debian,
anyhow):</p>

<pre><code>echo 1 &gt; /proc/sys/dev/mac_hid/mouse_button_emulation
</code></pre>

<p>Middle click is fn-ctrl, and right click is fn-alt. I wasn't excited
about F11/F12, or alt-2/alt-3, but this I think I can get used to. To make it
permanent, you want to do this:</p>

<pre><code>echo dev.mac_hid.mouse_button_emulation=1 &gt;&gt; /etc/sysctl.conf
</code></pre>

<p>If you don't have that proc file, you probably don't have <code>MAC_EMUMOUSEBTN</code>
compiled into your kernel.</p>
