---
layout: post
status: publish
published: true
title: EINVAL on sendmsg() to a UNIX Doman Socket
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1186
wordpress_url: http://hans.fugal.net/blog/2009/10/08/einval-on-sendmsg-to-a-unix-doman-socket
date: '2009-10-08 20:32:05.000000000 -07:00'
tags:
- cs
- C
- network
- socket
- mystery
comments: []
---
I'm seeing an EINVAL result when trying to do a <code>sndmsg()</code> call to a UNIX socket. The man page says that means that the sum of the <code>iov_len</code>s overflows an <code>ssize_t</code>, but an <code>ssize_t</code> is 8 bytes on this machine and there's only one iov and its length is 671. Last I checked that doesn't overflow anything but a char. What gives? Same code works fine in Linux and when using UDP or TCP. 
