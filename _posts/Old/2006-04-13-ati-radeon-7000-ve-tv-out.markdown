---
layout: post
status: publish
published: true
title: ATI Radeon 7000 VE TV Out
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 115
wordpress_url: urn:uuid:8f69adda-b18a-4d8b-81b4-5d7fe1c92ae4
date: '2006-04-13 08:57:00.000000000 -07:00'
tags:
- linux
- ati
- radeon
- tv
- mplayer
- xorg
comments:
- id: 1456
  author: Hans
  author_email: ''
  author_url: ''
  date: '2006-07-03 18:39:53 -0700'
  date_gmt: ''
  content: |-
    <p>Another update. You <em>can</em> do tvout in X, if you use the vesa driver. Choose a 4:3 video mode (800x600 works fine, so should larger resolutions) with the vesa driver and you'll see tvout. You can use whatever X11-based <code>-vo</code> option for mplayer you want, but I recommend xvidix. </p>

    <p>If you need/want 3D acceleration on your normal desktop, then you can set up another X session on VT 8, and while you're at it run freevo too. If you're really geeky, set up lirc to switch between 7 and 8 when you press the power button on your remote.</p>
- id: 1457
  author: lukemacklem@yahoo.com
  author_email: ''
  author_url: ''
  date: '2007-03-25 12:20:21 -0700'
  date_gmt: ''
  content: <p>My previous computer hard drive crashed and i had to get a new one and
    start fresh. Only problem is is that the box and manual and driver cd for the
    video card are long since lost. Windows xp has configured a driver for the card
    but I cannot access the tv out functions and I do not believe that the card is
    working at its full potential which leaves me to believe that although the driver
    designated for this card is sufficient enough for windows I do not believe it
    is the right driver. I have searched online for drivers but turn up nothing that
    seems to be a better fit. I was wondering if maybe you would know where I could
    find the right driver? If so I would greatly appreciate your help. I have been
    having "withdrawls" from my Counterstrike game. PLaying alone is nothing like
    playing online, and at the moment the game doesnt run well enough to play online
    due to the fact that when I set it to "3d acceleration" it say my video card does
    not support this mode, and I know it can, with the right driver of course.</p>
- id: 1458
  author: Colin Barrett
  author_email: theyikes@eircom.net
  author_url: ''
  date: '2007-08-03 07:53:35 -0700'
  date_gmt: ''
  content: |-
    <p>Hi Hans interesting stuff! I have an ATI Excalibur Radeon 7000 card and i don't know where to begin with getting t.v out up and running. </p>

    <p>I don't suppose you could enlighten me?</p>

    <p>I'm running Slackware 11 for what it's worth!</p>

    <p>Thanks Colin</p>
- id: 2369
  author: Jeff
  author_email: forums112@gmail.com
  author_url: http://www.u88yifa.com
  date: '2011-03-15 01:22:48 -0700'
  date_gmt: '2011-03-15 01:22:48 -0700'
  content: "Hi there,  Well I just wanted to say how helpfull I found your post. It
    is not that often you find very usefull information and explaination about the
    Radeon 7000. You have saved me hours of trying to work it out.\r\n\r\nThanks again
    Jeff"
---
<p>Once upon a time, I was a cheapskate without a 3D-accelerated video card. I
couldn't play BZFlag, Scorched Earth, or Flightgear. I was deprived. Then one
day I broke down and bought a 3D-accelerated card. I got a Radeon 7000 VE which
was anything but top of the line, but it has perfectly sufficed my needs. It
also has TV out, a fact I don't remember knowing until a couple of months ago
when I was crawling around behind my desk.</p>

<p>We don't watch TV. We don't have dish or cable, and the reception is almost as
bad as the programming. But we do like to watch a few choice shows, e.g. Good
Eats, Smallville, Doctor Who (old and new), and whatever other interesting
things turn up online, like the <a href="http://www.cablestogo.com/product.asp?cat%5Fid=2012&amp;sku=27993">Pancake
Mountain</a> theme
or <a href="http://whytheluckystiff.net/">_why</a>'s
<a href="http://whytheluckystiff.net/starry/">FOSCON</a> and other conference videos.
We also like to get movies from the library or Blockbuster, but that's beside
the point.</p>

<p>So when we got our tax money we had enough cash to throw at <a href="http://www.cablestogo.com/product.asp?cat%5Fid=2012&amp;sku=27993">an adapter
cable</a> (although
we spent half as much as that listed price). I had done a little research that
indicated it was possible but hairy to get TV out working with this card. I
enjoy a good challenge, so I ordered the cable.</p>

<p>The cable came yesterday. I got everything working peachily last night. I'm
good at wrangling Linux, but I think that it's safe to say this card is not
hard to get going. It will be even easier if you found this post.</p>

<p>First things first. Plug in the cable so you're hooked up to the TV and restart
your computer. You should see the console (boot screen, grub, etc.) on the TV.
That will give you a jolt of excitement; capture it in a cup for later.</p>

<p>Now, when you've booted, switch to virtual console 1 (i.e. get out of X) and run:</p>

<pre><code>mplayer -vo vesa:vidix /av/video/pancakemountain.mov
</code></pre>

<p>You should see a guy in a cape on both your PC screen and your TV screen. So
you see, it works great. Now, when the movie ends, or you quit, you'll have a
blank screen and not be able to see what you type. Or maybe you will be able
to. In any case, if you can't see, just switch virtual consoles, the you can
switch back.</p>

<p>Now, even I spend most of my time in X, so we want to get it working from X. X
runs at a higher resolution and probably different refresh rates than your TV,
so what you see on the TV will be just junk. No big deal, until you want to
watch something. I tried <code>xrandr -s 640x480</code> and got nothing but a messed up
gnome toolbar to show for it, so let's steer clear of switching resolution in
X. I tried to figure out how to get mplayer to switch video modes with <code>-vo
xvidix</code>, but without luck. So I tried <code>-vo vesa:vidix</code> again and it didn't work
so well. Well, it did work, although the brightness was sky-high. What didn't
work so well was getting back to X. After running <code>mplayer -vo vesa:vidix ...</code>
from X my USB keyboard stopped working, and I was stuck in limbo. Luckily you
can ssh in and do <code>sudo chvt 8</code> to get back to normal, as I found after a few
frustrating reboots.</p>

<p>To make a long story less long, I ended up writing a script to do the following</p>

<pre><code>#!/bin/sh
opts="-vo vesa:vidix -ao alsa:device=hw=0.1"
sudo chvt 1
mplayer $opts "$@"
sudo chvt 8
</code></pre>

<p>That works excellent. The <code>-ao</code> bit is to use alsa device <code>hw:0,1</code> which is my
rear output, where the audio part of the adapter cable is plugged in. If you've got sudo configured to ask you for your password, you might prefer to jump through lots of fun hoops as explained in the <a href="http://webpages.mr.net/bobz/howto/Quake-HOWTO-6.html#ss6.2">Linux Quake HOWTO</a>.</p>

<p>The only other thing I could hope for is to somehow watch something with
mplayer on the TV, and still be able to use the computer for other things. I
don't have much hope (without getting another video card, anyway) but if you
know how let me know.</p>

<h3>Update</h3>

<p>The above solution has a problem: I can't control mplayer with the keyboard. I can control mplayer from my laptop when I start it over ssh, which is why I didn't notice that before, but it's nice to be able to run it from the desktop too.</p>

<p>This is a much nicer script:</p>

<pre><code>#!/bin/sh
opts="-vo vesa:vidix -ao alsa:device=hw=0.1"
sudo openvt -sw -- mplayer $opts "$@"
</code></pre>

<p>If you don't like the idea of running mplayer as root (it's probably suid anyway), you're going to have a fun time figuring out how to get <code>"$@"</code> inside of another set of quotes for the <code>su -c</code> command. If you figure that one out I want to hear about it!</p>
