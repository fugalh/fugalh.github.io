---
layout: post
status: publish
published: true
title: MacBook Takes Flight
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 768
wordpress_url: urn:uuid:01b9f76f-6bdd-49ff-980e-b68088ad2f1c
date: '2006-12-13 22:19:50.000000000 -08:00'
tags:
- macbook
- flightgear
comments: []
---
<p>I sincerely hope that I didn't lead anyone astray with my recent posts knocking the Intel GMA 950 display adapter in the MacBook, based on my experience with FlightGear. While it's a given that the display adapter is a low-end integrated chip, it's not anywhere near as bad as I made it out to be.</p>

<p>I was uneasy with the conclusions I had drawn. Part of it was optimism and part
of it was probably instinct. It just didn't add up.</p>

<p>The version of FlightGear I had was 0.9.9 as linked to by the <a href="http://flightgear.org/Downloads/binary.shtml#mac">FlightGear Homepage</a>. 0.9.9 was old, and I was on a quest to get version 0.9.10. I was in the process of trying to get it compiled and ended up at <a href="http://macflightgear.sf.net">http://macflightgear.sf.net</a>. I had visited this site back a month or so ago and it hadn't been updated in a while. It must have been before November 16. Today I saw that things were hopping there again. And then I saw it. "FlightGear 0.9.10 universal binary pre-release 2 [released] 2006-11-24". The full realization of my stupidity gushed forth. I was only getting 7-15 fps because I was running it as  PPC binary through Rosetta. </p>

<p>Eagerly I downloaded the .dmg and gave it a try. It didn't open. A closer read of the webpage indicated I needed <a href="http://rubycocoa.sourceforge.net/doc/">RubyCocoa</a>. Uh oh, I tried to play with that once and installing it was a pain. Not so now, they have a no-nonsense installer now. Good work RubyCocoa team! The qtruby guys could learn a thing or two from you. I might have to explore RubyCocoa again in the future now that it's übereasy to install.</p>

<p>Now the launcher fired up. It has thumbnails of the planes, very nice touch. I tried to run FlightGear and got an error appeared in my logs. There was an exception in Options.rb on line 104. I looked at the file (<code>FlightGear.app/Contents/Resources/Options.rb</code>) and I couldn't tell what line 104 was supposed to be doing. It looked like it wouldn't hurt to comment it out, and that's just what I did. Now it works like a charm.</p>

<p>What is the difference between a universal binary and a PPC binary in emulation?  About a 3x speedup in FlightGear fps, that's what. I did a circuit from KSFO at night with all the rendering options in the View menu checked (except shadows) and an empty <code>.fgfsrc</code>. 21fps on average, often higher, only occasionally lower. I did a circuit from KLRU switching between day and night. 50fps or better. That's more like it.</p>

<p>I have a few ideas for the launcher (aside from the bug I mentioned above). I have my own launcher in qtruby that reads your <code>.fgfsrc</code> and even saves back to your <code>.fgfsrc</code> on request (without losing your comments). There's a few more default options I'd like to see. I should be able to merge in my work into his launcher without much difficulty, when I get a chance. (That's the catch, as always.)</p>
