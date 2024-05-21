---
layout: post
status: publish
published: true
title: Minicom and SLIP
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 66
wordpress_url: urn:uuid:ac92e20d-1092-455b-a75f-2c24213fe35c
date: '2005-04-05 15:10:37.000000000 -07:00'
tags:
- linux
comments: []
---
<p>I was trying to establish a SLIP connection with a stupid managed switch that
claimed it talks SLIP in the docs. It doesn't - it talks serial just like
everything else with a serial console port. But that was hard to discover
because using slattach to try to establish a slip connection seemed to render
my serial port useless. I imagine you could reset it somehow with setserial,
but I'm easily confused by serial stuff so I just rebooted. Store that away in
your databanks: using minicom after slattach (even if you rmmod slip and all
that good stuff) doesn't work without voodoo or reboot.</p>
