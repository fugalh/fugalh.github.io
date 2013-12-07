---
layout: post
status: publish
published: true
title: JACK and ZynAddSubFX Survive Intense Thrashing!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 9
wordpress_url: urn:uuid:4eae9394-4312-41b4-afd5-8a8bf70a2f6b
date: '2005-10-22 19:57:40.000000000 -07:00'
tags:
- audio
comments: []
---
<p>I wrote a program with a serious memory leak, and filled up my 512MB RAM and
1GB swap. My computer, falcon, was in serious thrashing mode. The red led was
on solid, X was completely unresponsive (characters I typed in my xterm showed
up about 10 minutes later).  Even my laptop's network connection was
unresponsive (because falcon is my router here)</p>

<p>While I was debating as to why the Out-Of-Memory killer hadn't reaped my
runaway process yet, I got curious as to whether JACK would work at all. So I
reached over and pressed some keys on my MIDI keyboard (ZynAddSubFX was
running, as it usually is), and sure enough Zyn came sounding through loud and
clear. In fact, I couldn't hear a single XRUN. It was as if the computer was as
idle as could be. I was seriously impressed.</p>

<p>Impressed, but not overly surprised. I did ask for this after all. I have
2.6.13 with Ingo Molnar's realtime-preempt patch, and rtlimits configured
properly. jackd runs at priority 65, and my sound card at priority 99. I have
the realtime-preempt patch configured at <code>PREEMPT_DESKTOP</code>, because I've had
stability issues with <code>PREEMPT_RT</code>. <code>PREEMPT_DESKTOP</code> has been solid though, I
have a 33-day uptime, and I use falcon heavily.</p>

<p>I won't go into the details again on how to get where I am, because the
information in the last paragraph coupled with <a href="http://tapas.affenbande.org/">tapas' excellent
instructions</a> for <a href="http://tapas.affenbande.org/?page_id=6">realtime
preemption</a> and
<a href="http://tapas.affenbande.org/?page_id=22">rtlimits</a> are all you need. </p>

<p>One last statistic, in case you still don't believe me. That thrashing session
started about an hour ago and lasted about half an hour. Here's the screenshot
from qjackctl: </p>

<p><img src="/images/qjackctl_after_thrash.png" alt="qjackctl status screenshot"/></p>
