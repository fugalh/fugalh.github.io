---
layout: post
status: publish
published: true
title: echo "~lart launchd" | at now
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 926
wordpress_url: urn:uuid:a7f5676a-978b-4a0b-9db1-5760f07cbfad
date: 2008-02-13 10:57:00.000000000 -08:00
tags:
- atd
- atrun
- at
- launchd
comments:
- id: 1695
  author: Viktor
  author_email: neri_neraa@yahoo.com
  author_url: http://www.cleancorpse.org
  date: '2008-02-14 04:36:45 -0800'
  date_gmt: ''
  content: <p>Surprisingly, there is less support for leopard than the tiger. I have
    bee having trouble configuring some of the tools with unix.</p>
- id: 1696
  author: Alex
  author_email: alex.esplin@gmail.com
  author_url: ''
  date: '2008-03-13 01:12:00 -0700'
  date_gmt: ''
  content: <p>Did you ever notice any major battery issues with this?</p>
- id: 1697
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-03-13 09:21:28 -0700'
  date_gmt: ''
  content: <p>I never had a chance to find out. 10.5.2 came out a few days later and
    utterly broke at.</p>
---
<p>If you're an old UNIX die-hard using Leopard (and I think Tiger as well) you may have noticed that <code>at</code> doesn't seem to work. That's because launchd (How do I hate thee? Let me count the ways…) has subsumed <code>atd</code> as well as all the other useful scheduling things like <code>cron</code> and friends. <code>at</code>'s manpage doesn't tell you there is no atd, and implies that cron calls atrun every five minutes (incidentally, atrun's manpage says every ten minutes). Apparently in Tiger the manpage was more helpful, telling you how to enable at jobs with launchd, but no more.</p>

<p>If you do want to enable at functionality, this is the trick:</p>

<pre><code>launchctl load -w /System/Library/LaunchDaemons/com.apple.atrun.plist
</code></pre>

<p>Be warned that it's apparently disabled by default due to power management concerns, so it might not be laptop-friendly. I'm going to see if it makes a noticeable difference to my laptop usage and/or battery life over the next few days and if it does I'll blog it.</p>

<p>Launchd runs atrun every 30 seconds. This is configurable by hacking the plist file mentioned above.</p>
