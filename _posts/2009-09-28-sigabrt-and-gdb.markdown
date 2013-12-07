---
layout: post
status: publish
published: true
title: SIGABRT and gdb
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1182
wordpress_url: http://hans.fugal.net/blog/?p=1182
date: '2009-09-28 18:13:45.000000000 -07:00'
tags:
- cs
- gdb
- assert
- SIGABRT
comments: []
---
So you fire up gdb and pepper your code with <code>assert()</code> calls. Then one of your assertions fails and you see this:
<code>
Assertion failed: (item_idx < si.slabclass[clsid].perslab), function ITEM, file slabs_items.h, line 78.
Program received signal SIGABRT, Aborted.
0x00007fff83efab16 in kevent ()
(gdb)
</code>
Well shucks, you think you're screwed because gdb doesn't seem to have left you in a useful state. So you investigate conditional breakpoints (that are a pain to set and don't seem want to work in inline functions), and generally beat yourself over the head for awhile.

Then you realize that gdb's throwing you out into a different thread, and your pretty backtrace <em>is</em> there for the exploring, you just have to switch to the right thread. Yeah, remember that. Then maybe you can set a breakpoint on the actual assert code (which you can find with the backtrace—it was <code>__assert_rtn()</code> in my case) so you're already in the right thread and just need to go up the backtrace one level to get to debugging goodness.
