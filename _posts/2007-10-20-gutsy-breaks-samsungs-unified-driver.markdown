---
layout: post
status: publish
published: true
title: Gutsy breaks Samsung's Unified Driver
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 882
wordpress_url: urn:uuid:9add610c-1ed5-4ff5-aa91-53c1824d4719
date: '2007-10-20 11:35:00.000000000 -07:00'
tags:
- samsung
- cups
- ubuntu
- gutsy
comments:
- id: 1625
  author: Ernie
  author_email: ''
  author_url: ''
  date: '2007-11-12 11:08:10 -0800'
  date_gmt: ''
  content: <p><a href="https://bugs.launchpad.net/ubuntu/+source/cupsys/+bug/152537"
    rel="nofollow">https://bugs.launchpad.net/ubuntu/+source/cupsys/+bug/152537</a>
    resolved the problem for me.</p>
---
<p>I have a Samsung SCX-4100 monochrome laser printer and scanner. I am quite happy with it as a printer, but it occasionally gives me heartburn because of the driver situation. Samsung has put together a binary driver, and not an especially bad one at that. It has a nice installer, and for the most part it Just Works™ and works well. But if you're a sysadmin or FSF (free software freak), it will get on your nerves. It futzes about with cups and sane, though it hasn't broken either in a long time. It has a history of changing apps like xsane, OpenOffice, etc. to setuid, though it no longer does this either. The biggest problem is that just about every other time you update Ubuntu it stops working.</p>

<p>This time, there's one and possibly two problems. The first and primary problem is that <code>/usr/lib/cups/backend/mfp</code> segfaults. I don't know why, but my best guess is version incompatibilties (maybe cups version or system libraries). The second problem, which I came across while googling around, <em>may</em> be that there's going to be a problem with <a href="https://wiki.ubuntu.com/AppArmor">AppArmor</a>. If you get past the segfault, you might try disabling AppArmor for cups. I don't know much about AppArmor, but it looks like this is the mantra: <code>sudo aa-complain cups</code>. Or, turn it off entirely with <code>/etc/init.d/apparmor stop</code>. Neither of these fixed things, but the logs did change so it might be a needed step.</p>

<p>In the meantime I'm hooking the printer up to my Debian server, and thanks to cups things will be completely transparent. Until I want to scan something, of course, but I can probably use NX in a pinch if it still doesn't work in Ubuntu by then.</p>
