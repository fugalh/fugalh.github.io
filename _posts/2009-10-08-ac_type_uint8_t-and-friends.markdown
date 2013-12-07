---
layout: post
status: publish
published: true
title: AC_TYPE_UINT8_T and friends
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1187
wordpress_url: http://hans.fugal.net/blog/2009/10/08/ac_type_uint8_t-and-friends
date: 2009-10-08 23:15:00.000000000 -07:00
tags:
- cs
- linux
- C
- autoconf
- autotools
- unix
comments: []
---
If you get errors like this:

<code>$ autoreconf
configure.ac:110: error: possibly undefined macro: AC_TYPE_UINT8_T
      If this token and others are legitimate, please use m4_pattern_allow.
      See the Autoconf documentation.
configure.ac:111: error: possibly undefined macro: AC_TYPE_UINT16_T
configure.ac:112: error: possibly undefined macro: AC_TYPE_UINT32_T
configure.ac:113: error: possibly undefined macro: AC_TYPE_UINT64_T
configure.ac:115: error: possibly undefined macro: AC_TYPE_SSIZE_T
autoreconf: /usr/bin/autoconf failed with exit status: 1</code>

It probably just means you have an old autoconf. These macros were introduced in autoconf 2.60. But it's probably no big deal if you have a sensible <code>stdint.h</code>.
