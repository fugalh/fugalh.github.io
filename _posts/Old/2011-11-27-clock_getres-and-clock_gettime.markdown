---
layout: post
status: publish
published: true
title: clock_getres() and clock_gettime()
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1260
wordpress_url: http://hans.fugal.net/blog/?p=1260
date: '2011-11-27 19:21:45.000000000 -08:00'
tags:
- audio
- linux
- realtime
- posix
- hrt
- config_high_res_timers
comments: []
---
In Linux kernel 2.6.33 at least, when you call clock_getres() you may not be getting the whole story if the kernel was compiled without high-res timers. (CONFIG_HIGH_RES_TIMERS)

clock_getres() returns {0, 999848}, which you might think means clock_gettime() has a resolution of about 1ms. But no, if you call clock_gettime() twice in rapid succession you find that it is far higher resolution than that—I usually get either 698 or 699 nanoseconds as the difference. So is clock_getres() wrong? No, not exactly. It is reporting the jiffy that limits clock_settime() and the timers. If you time clock_nanosleep() you find that even if you ask to sleep for 1ns you will sleep until the next jiffy boundary, i.e. as much as 1ms and about 0.5ms on average.

If you look at /proc/timer_list on this machine, it reports a tick resolution of 999848, but hrtimer functions are being used underneath the covers:

<code>
active timers:
 #0: <ffff880dd05d5ea8>, hrtimer_wakeup, S:01, hrtimer_start_range_ns, smc_proxy/14652
 # expires at 1322421490000000000-1322421490000050000 nsecs [in 1303778479239642688 to 1303778479239692688 nsecs]
 clock 1:
  .base:       ffff88002820e680
  .index:      1
  .resolution: 999848 nsecs
  .get_time:   ktime_get
</code>

My guess is that clock_gettime() is using HRT and giving high-resolution answers even though you didn't enable using HRT for POSIX timer functions by leaving CONFIG_HIGH_RES_TIMERS unset.

A side effect of this silly situation is that gettimeofday() is also accurate (to µs), though usleep() and nanosleep(), like clock_nanosleep(), are limited to 1ms ticks.
