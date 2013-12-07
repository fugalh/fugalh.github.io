---
layout: post
status: publish
published: true
title: Help! My MPlayer VIDIX output stopped working!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 780
wordpress_url: urn:uuid:4543da90-e300-4323-b14b-bdc9934c3c1c
date: 2007-02-05 19:03:42.000000000 -08:00
tags:
- linux
- mplayer
- vidix
- dont panic
comments: []
---
<p>If when you upgrade MPlayer the wonderful VIDIX output mysteriously stops working (I have a Radeon card, but I don't think it matters), <em>Don't Panic</em>.</p>

<p>It's probably just that you forgot to <code>chmod +s /usr/bin/mplayer</code> (or run
mplayer as root, you decide which is the lesser evil). Incidentally, if you
know the device file to change permissions on so that you can run mplayer as
user without the setuid bit, I'm theoretically interested in acquiring that bit of knowledge. </p>
