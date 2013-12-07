---
layout: post
status: publish
published: true
title: Radium in Ubuntu
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 970
wordpress_url: urn:uuid:1496130a-8bc9-40d0-a82b-40a2a6f18ed6
date: 2008-06-02 11:41:00.000000000 -07:00
tags:
- linux
- ubuntu
- radium
- keystation
- midisport
comments:
- id: 1822
  author: Midisport redux | The Fugue
  author_email: ''
  author_url: http://hans.fugal.net/blog/2009/02/04/midisport-redux
  date: '2009-02-04 18:21:44 -0800'
  date_gmt: '2009-02-04 18:21:44 -0800'
  content: '[...] blogged about setting up my Radium keyboard in Ubuntu 8.04. Now
    in Ubuntu 8.10 the problem is the same but the solution is different (but [...]'
- id: 1909
  author: Ponnaiguisa
  author_email: fauckceam@gmail.com
  author_url: http://www.google.com
  date: '2009-03-20 13:28:17 -0700'
  date_gmt: '2009-03-20 13:28:17 -0700'
  content: very  intresting
---
<p>My Radium 61 MIDI controller (read: MIDI keyboard that doesn't make any sound
of its own accord) has worked great in Linux from day one, but it was always a
bit of a pain to get set up.</p>

<p>When the keyboard is plugged in (USB), it needs firmware uploaded to it before
it will show up as a USB MIDI device. In the past the way this is done has changed several times. In the devfs days you did one thing. Then someone wrote a package that made it even simpler. Then udev came along and messed everything up. Then udev changed and messed everything up. Then it happened again (stupid udev). Then I brought my keyboard to school and only used it with OS X for a year or so, and now here we are.</p>

<p>Now Ubuntu 8.04 has a package <code>midisport-firmware</code> which installs the firmware and the udev rules. Awesome! Except, it doesn't work. It turns out that the <code>midisport-firmware</code> package (which obviously must be coming from Debian unstable, or it would probably work) depends on usbfs, and apparently Ubuntu has disabled it. Or broken it. Or something. The fix is quite easy: uncomment the four lines under the comment "Magic to make /proc/bus/usb work" in <code>/etc/init.d/mountdevsubfs.sh</code>, then issue <code>/etc/init.d/mountdevsubfs.sh start</code>. It should Just Work&trade; in the future after reboots.</p>
