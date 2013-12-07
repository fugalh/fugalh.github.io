---
layout: post
status: publish
published: true
title: Defeating the AC_CHECK_HEADER cache
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1201
wordpress_url: http://hans.fugal.net/blog/?p=1201
date: '2010-02-02 02:47:52.000000000 -08:00'
tags:
- linux
- autotools
- cppflags
- AC_CHECK_HEADER
comments: []
---
The <code>AC_CHECK_HEADER</code> macro caches its result, so if you want to call it again with a different <code>CPPFLAGS</code> it will just remember the result of the first execution.

If you want to defeat this cache, as I did, this is the pattern:
<code>
header=foo.h
cache_var=AS_TR_SH([ac_cv_header_$header])
...
AC_CHECK_HEADER([$header])
...
CPPFLAGS="-I/opt/local/include"
$as_unset $cache_var
AC_CHECK_HEADER([$header])
...
</code>

<code>AS_TR_SH</code> does the escaping (giving <code>ac_cv_header_foo_h</code> in this case), <code>$as_unset</code> is the portable way to unset a shell variable in autotools.

Incidentally, if you don't restore <code>CPPFLAGS</code> to its original user-set value, I will hunt you down and shave your head.
