---
layout: post
status: publish
published: true
title: Midisport redux
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1088
wordpress_url: http://hans.fugal.net/blog/2009/02/04/midisport-redux
date: '2009-02-04 18:21:01.000000000 -08:00'
tags:
- midi
- udev
- usb
- ubuntu
- radium
- midisport
- firmware
- ibex
comments: []
---
I <a href="http://hans.fugal.net/blog/2008/06/02/radium-in-ubuntu">blogged about setting up my Radium keyboard in Ubuntu 8.04</a>. Now in Ubuntu 8.10 the problem is the same but the solution is different (but easier).

Install the <code>midisport-firmware</code> package, and then add this line to <code>/etc/fstab</code>:
<pre><code>none /proc/bus/usb usbfs devgid=46,devmode=664 0 0</code></pre>

Mount it, or reboot. Once usbfs is mounted, then it will work as advertised for a midisport 2x2, at least. It doesn't work for my Radium, I imagine because the udev rules aren't sufficient. But since I have a midisport 2x2 sitting here, I'm not going to bother figuring it out. Sorry, but I bet you can figure it out with that head start.
