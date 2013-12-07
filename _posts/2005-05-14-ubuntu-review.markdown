---
layout: post
status: publish
published: true
title: Ubuntu on the iBook
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 89
wordpress_url: urn:uuid:f8735ab6-f506-4f10-b165-40bed500112e
date: 2005-05-14 10:30:41.000000000 -07:00
tags:
- mac
comments: []
---
<p>I've done it&mdash;I've installed, configured, and used Ubuntu linux on my
iBook. (gandalf) I made a checklist of things that I feel are important and
will tell you how Ubuntu did out of the box, (which is the primary advantage of
one distro over another), and whether I was able to get it working with effort
(or saw the light in the tunnel).</p>

<p>The first category is power management. Decent power management, especially
sleep, is essential for any laptop. First the good news: thermal control and
battery/AC reporting work great out of the box with Ubuntu. So does cpufreq,
although I haven't decided yet if it needs to be tweaked. The fan comes on more
often than in OS X, but I've heard complaints of overheating in OS X so maybe
it's doing the Right Thing&trade;. </p>

<p>Now the bad news: sleep is out. It goes to sleep just fine, but it's more like
a coma than sleep. When you go to wake it, it makes hard disk sounds and the
caps lock light works, but there is no screen activity and apparently the
kernel locks up. I hear rumors that this might work later, and that it does
work now for some people. Sacrificing 3D acceleration is one thing people say
works. I tried leaving X altogether and it still behaved the same.</p>

<p>The next category is network support. The ethernet card works out of the box. I
haven't tried the modem. The @#!% Broadcom wireless card does not work, of
course. There are affordable USB wireless adapters that work great though, so
this is more an inconvenience, and one I was aware of when I bought the laptop.</p>

<p>Caps lock must be remapped to control. I've had no luck with that in linux yet,
unhappily. (No, xmodmap doesn't work, although you can <em>disable</em> caps lock with
xmodmap.) It must be possible though, because it works in OS X (even built into
the preferences in Tiger), so eventually it will work in linux as well.</p>

<p>Sound support is decent. The ALSA mixer is a little confused about capture
devices, but capture does work. Playback of course works, but there's only one
channel (I've been spoiled in this area before). I fired up JACK and used the
XMMS JACK plugin for a few songs&mdash;no xruns. That doesn't exactly comprise
a stress test, but it is much better than some environments I've been in, so
that's a good sign.</p>

<p>Video works out the box. No futzing with the X config. I assume there's 2D
acceleration, and there definitely is 3D acceleration. This brings us to one of
the most important reasons for me to dual-boot linux on my iBook:
<a href="http://www.flightgear.org/">FlightGear</a>. I just don't have the RAM (256MB) to
run both FlightGear and OS X. FlightGear runs very well in linux, even with
GNOME. </p>

<p>Video out didn't work when I plugged another monitor in. I think this is
possible, but I haven't done the research on it. I was slightly disappointed
that I didn't get mirror out of the box. I'm slightly excited about the
supposed possibility for Xinerama.</p>

<p>DVD support works, although Totem player (the default GNOME action when you
insert a DVD) does some very strange things indeed, none of which is actually
play the DVD. It confuses the battery meter, which decides to tell me I have
less than 5% battery life, when in reality the battery is at 85%. It causes the
mouse to stutter, and in fact once killed the mouse altogether&mdash;I had to
reboot to get it back. So that's a lose for Ubuntu. I installed ogle and it
works well, although DVD playback isn't smooth like in OS X for some reason.
All in all, when I watch DVDs I'll probably do it in OS X.</p>

<p>And now for the miscellany. HFS+, check (after loading the hfsplus module).
USB, check. CDROM and CD writing, check. </p>

<p>Overall, support for the iBook in linux is great. As far as I can tell, the
only component with a dismal outlook is the Airport Extreme, which is easily
worked around. There's still a bit of fiddling that needs to take place to
bring linux up to snuff with OS X, but it looks like it's all doable.</p>
