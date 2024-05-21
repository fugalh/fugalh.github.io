---
layout: post
status: publish
published: true
title: ~/.Xresources on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 95
wordpress_url: urn:uuid:64ba2774-7ec8-461f-aab9-853a9bc5f94b
date: '2005-04-15 23:13:54.000000000 -07:00'
tags:
- mac
comments: []
---
<p>I thought X11 had gone bonkers&mdash;I couldn't get it to listen to
<code>~/.Xresources</code> or any variation thereof. It turns out I just needed to install
the X11 SDK (which I did along with all the other SDKs), and things worked
great. I'm guessing the reason is the same reason xrdb didn't work either:
<code>/usr/bin/cpp</code> didn't exist and xrdb failed with a complaint to that effect.</p>
