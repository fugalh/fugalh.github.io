---
layout: post
status: publish
published: true
title: NX Desktop Sharing
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 851
wordpress_url: urn:uuid:33d535e2-c8ec-4011-b72c-89a4d5893304
date: '2007-07-16 10:18:22.000000000 -07:00'
tags:
- nx
- vnc
comments:
- id: 1583
  author: Tene
  author_email: ''
  author_url: ''
  date: '2007-07-16 16:33:59 -0700'
  date_gmt: ''
  content: <p>X has had builtin VNC support for quite a while, providing VNC access
    to running X sessions.  Just load the 'vnc' module in your X config.</p>
- id: 1584
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-07-16 23:09:57 -0700'
  date_gmt: ''
  content: <p>Ah, that's good to hear. I wouldn't be surprised if this is the mechanism
    that NX is using.</p>
---
<p>I just learned of a very neat new feature in NX 3. Now you can shadow sessions,
and even more importantly you can share local X displays. This latter bit works
like VNC does in Windows. To my knowledge this has been a missing feature from
all related products (vnc flavors, nx, etc.) in the past. Indeed it is a source
of confusion when someone tries to set up vnc on linux, thinking they'll get
remote access to what's on the screen, but instead setting up a vnc-only X
session.</p>

<p>The OS X client is a bit more polished now as well. For the NX free server
(from NoMachine.com, not FreeNX), I had to uninstall the old nx packages on my
debian box before installing the debs for version 3, because of some upgrade
problems, but it works great. I gave up on FreeNX long ago when NoMachine
started providing debs and FreeNX stopped working despite all my best efforts.</p>
