---
layout: post
status: publish
published: true
title: Mental UTC Conversion
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1037
wordpress_url: urn:uuid:bdd9cf51-45f0-4af0-8bce-da50f3cb464e
date: 2009-01-15 13:06:00.000000000 -08:00
tags:
- utc
- mental
- math
- aviation
- wx
- weather
- pilot
- zulu
- timezone
comments:
- id: 1797
  author: Jacob Fugal
  author_email: lukfugl@gmail.com
  author_url: ''
  date: '2009-01-15 15:38:02 -0800'
  date_gmt: '2009-01-15 15:38:02 -0800'
  content: |
    <p>The way I do it is to establish a few reference points:</p>

    <p><pre><code>5pm local = midnight UTC
    5am local = noon UTC
    7pm UTC = noon local
    7am UTC = midnight local
    </code></pre></p>

    <p>Then you can say things like "it's three hours to midnight UTC, which puts it three hours to 5pm local, that's 2pm local" or "it's 2 past noon local, so that's 2 past 7pm UTC, or 9pm UTC"</p>

    <p>It doesn't address the DST problem though (you have to reset your reference points when you switch back and forth, and this does trip me up sometimes), and it kind of anchors you to a specific "local". So it's not perfect, but it usually works for me.</p>
- id: 1810
  author: Russel Fugal
  author_email: rfugal@gmail.com
  author_url: ''
  date: '2009-01-26 06:53:50 -0800'
  date_gmt: '2009-01-26 06:53:50 -0800'
  content: Simple. Set all your clocks, watches, and digital sundials to UTC time.
    Then, use a post-it note to write down your timezone (UTC -7). Change the post-it
    twice a year. Hack you cell phone clock or ignore it.
---
<p>I do a lot of UTC conversions, more than most, and I am dismayed that after perhaps a year of relatively frequent mental UTC conversions it's still no faster than firing up a terminal and typing <code>date -u</code>. Even with <a href="http://docs.blacktree.com/quicksilver/what_is_quicksilver">Quicksilver</a> and fleet fingers my mind should win that race every time.</p>

<p>No one step is difficult, but there are too many steps. First you have to load in the reference time (might be a UTC time or local time) then maybe convert it to 24-hour time then remember whether DST is in effect or not and whether that means -7 or -6, then figure out whether to add or subtract that 7 or 6 hours, then do the actual subtraction, then wonder if you did that right and possibly wonder whether that's the same date as today or not… Clearly the brute force method is not the way to go.</p>

<p>If Richard Feynman can calculate square roots in his head instantly, I'm sure I can convert time zones. Anyone have any suggestions on how to gain this skill? I think I'll add <a href="http://www.amazon.com/exec/obidos/ASIN/1560275103/thefug-20">Mental Math for Pilots</a> to my wishlist.</p>
