---
layout: post
status: publish
published: true
title: FlightGear on a MacBook
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 762
wordpress_url: urn:uuid:e4de077e-9b7d-4a90-9888-c80e953ed027
date: 2006-12-12 23:14:31.000000000 -08:00
tags:
- mac
- flightgear
comments: []
---
<p>I was less than fair in my previous assessment of the MacBook's ability to run FlightGear. It is capable of running it at passable speeds if you disable some things. I went through the output of <code>fgfs -h -v</code> and disabled everything that could be disabled (almost) and I get about 20fps when I'm not looking at the KSFO terminal or something equally busy. Even then it's 14 or 15. That's flyable. Using the 2D cockpit (or no cockpit and just the HUD) will buy you a couple of frames per second. But so will using a less-complex 3D cockpit, e.g. the Piper Cherokee Warrior II or the Northrop T-38. Flying during the day will buy you a lot (something about airport lights). One nice thing is that you get basically the same frame rate with the window maximized (or full-screen) as at 640x480. It's not pixel-bound, in other words. Most of the checkboxes in View|Rendering Options make no noticeable difference, except shadows, and I don't know about the lighting options since any nighttime flying with airport lights is too slow to bother.</p>

<p>So here's the <code>~/.fgfsrc</code> that gets me 23fps average in the air away from the airport in the Piper Cherokee Warrior II. </p>

<pre><code>--disable-random-objects
#--enable-ai-models
--fog-fastest
#--disable-enhanced-lighting
#--disable-distance-attenuation
#--disable-specular-highlight
#--disable-anti-alias-hud
#--disable-hud-3d
#--disable-clouds3d
#--enable-fullscreen
--shading-flat
#--disable-skyblend
#--disable-textures
--aircraft=pa28-161
</code></pre>

<p>One of these days I'll see which of the three remaining I can trim also, but it
looks good enough for now.</p>
