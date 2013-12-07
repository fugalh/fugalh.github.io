---
layout: post
status: publish
published: true
title: Sound Card Indices
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 963
wordpress_url: urn:uuid:b9fdd2ae-861c-4dd1-8c7c-fb53b74bc3ba
date: '2008-05-20 23:18:21.000000000 -07:00'
tags:
- linux
- kernel
- debian
- ubuntu
- module
comments: []
---
<p>I have two soundcards in my desktop: the built-in soundcard which uses the <code>snd-via82xx</code> module, and the nice soundcard which uses the <code>snd-cs46xx</code> module. Naturally, the speakers are plugged into the nice card.</p>

<p>When I installed Ubuntu 8.04 from scratch, the VIA card started showing up as the first card, and therefore the default card. (You can tell by looking at <code>/proc/asound/cards</code>.) I created the following <code>/etc/asound.conf</code> to remedy that problem:</p>

<pre><code>pcm.!default {
  type hw
  card CS46xx
}
ctl.!default {
  type hw
  card CS46xx
}
</code></pre>

<p>Ok, so now all programs using ALSA's default device automatically go to the right soundcard. But apparently using the default device is too much to ask of some software, which apparently hardcodes <code>hw:0</code> or (even nuttier) <code>hw:0,0</code>. </p>

<p>So what I really wanted was to fix the order problem, so that the VIA card doesn't steal index 0. On Ubuntu at least, the fix is:</p>

<pre><code>echo 'options snd-via82xx index=2' &gt;&gt; /etc/modprobe.d/alsa-base
</code></pre>

<p>Now my <code>/proc/asound/cards</code> always looks like this:</p>

<pre><code>0 [CS46xx         ]: CS46xx - Sound Fusion CS46xx
                     Sound Fusion CS46xx at 0xfb122000/0xfb000000, irq 20
1 [UART           ]: MPU-401 UART - MPU-401 UART
                     MPU-401 UART at 0x330, irq 10
2 [V8237          ]: VIA8237 - VIA 8237
                     VIA 8237 with ALC655 at 0xec00, irq 21
</code></pre>
