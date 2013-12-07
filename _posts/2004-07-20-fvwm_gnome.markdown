---
layout: post
status: publish
published: true
title: Happy Hacking Keyboard, GNOME 2.4, and FVWM
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 49
wordpress_url: urn:uuid:66c6317a-f90a-4748-b836-66f50dcaa560
date: 2004-07-20 14:45:06.000000000 -07:00
tags:
- linux
comments: []
---
<p>I'm using GNOME at work, and got sick of the "user friendly" window non-manager
Metacity, so I started investigating other options. Despite much smoke and
mirrors to the contrary you really can use other window managers in GNOME these
days (this is 2.4). Sawmill is nice in theory but I have an aversion to lisp
syntax (although I love the language theoretically). </p>

<p>FVWM is one of my favorite WMs from the configurability standpoint. Its
weakness is as a desktop. I don't require much from a desktop: quicklaunch,
dock (panel is OK, slit is best), and do it without taking a lot of space. FVWM
can almost cover the first two with some work, but it flat out fails on the
last point. But I digress. The point is that I decided to use FVWM as my window
manager in GNOME and I am loving it.</p>

<p>One of the great things about FVWM is that it groks all the keystrokes and
modifiers. So I can use that windows key for window manager functions and leave
Alt alone, so applications that use Alt will actually work. My Happy Hacking
keyboard has cute little diamond keys that are supposed to be Meta keys. They
output the Super_[LR] keycodes. Alas, for whatever reason, mod4 wasn't getting
bound to them, as you can see here:</p>

<pre><code>fugalh@gwythaint:~$ xmodmap
xmodmap:  up to 3 keys per modifier, (keycodes in parentheses):

shift       Shift_L (0x32),  Shift_R (0x3e)
lock
control     Control_L (0x25),  Control_L (0x42),  Control_R (0x6d)
mod1        Alt_L (0x40),  Alt_R (0x71)
mod2        Num_Lock (0x4d)
mod3
mod4
mod5
</code></pre>

<p>This is the secret:</p>

<pre><code>fugalh@gwythaint:~$ cat &gt; ~/.xmodmaprc
add mod4 = Super_L Super_R
fugalh@gwythaint:~$ xmodmap ~/.xmodmaprc
</code></pre>

<p>Throw that last command in your ~/.xsession to complete the trick. Now things
like the following work in your ~/.fvwm/.fvwm2rc:</p>

<pre><code># do the alt-drag and alt-resize thing
Mouse 1 FSTW 4 Move
Mouse 3 FSTW 4 Resize
</code></pre>

<h5>Update</h5>

<p>I think I was wrong, the problem was probably GNOME in the end. Not only does
GNOME annoyingly complain about my having an ~/.xmodmaprc, but it apparently
does its own xmodmap based on the keyboard settings, which wipes out my custom
xmodmap. So the solution is to set the keyboard to Generic 104-key PC in
Keyboard Preferences.</p>

<h4>On FVWM and GNOME</h4>

<p>You probably want the following basics in your .fvwm2rc for GNOME 2.4:
    Style "gnome-panel" NoTitle, !Borders, NeverFocus
    # this emulates the default FVWM root menu. Notice the D context (see fvwm(1))
    Mouse 1 RD A Menu MenuFvwmRoot</p>

<p>Oh and by the way, you need FVWM >= 2.5.x for GNOME 2.x, or <a href="http://fvwm-ewmh.sourceforge.net/">a patch and a module</a> for FVWM 2.4.x.</p>
