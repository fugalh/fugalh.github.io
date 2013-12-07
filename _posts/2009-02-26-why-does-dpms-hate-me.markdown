---
layout: post
status: publish
published: true
title: Why does DPMS hate me?
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1113
wordpress_url: http://hans.fugal.net/blog/?p=1113
date: 2009-02-26 16:01:32.000000000 -08:00
tags:
- fail
- gnome
- xset
- dpms
- power
- gnome-screensaver
- gnome-power-manager
- bugs
comments:
- id: 1872
  author: vontrapp
  author_email: von@fugal.net
  author_url: http://von.fugal.net/blog
  date: '2009-02-26 19:05:19 -0800'
  date_gmt: '2009-02-26 19:05:19 -0800'
  content: I gave up on gnome-screensaver a long time ago. Usually I just leave it
    alone completely and let it do the default thing, which is not working. So currently
    my laptop will blank the screen after some unknown default time, then some other
    time later the screen turns off. I've never been able to get an actual screensaver
    to show using gnome, but a blank screen suits me just fine.
- id: 1970
  author: Wade Nelson
  author_email: wade.nels@gmail.com
  author_url: ''
  date: '2009-04-30 12:35:36 -0700'
  date_gmt: '2009-04-30 12:35:36 -0700'
  content: "gnome-power-manager and gnome-screensaver are just broken.  It's that
    simple.  Disable them completely and run:\r\n\r\nxset dpms StandbyTime SuspendTime
    PowerOffTime\r\n\r\nWhere the time values are in seconds.  That'll set DPMS in
    a way that works."
- id: 1974
  author: BassKozz
  author_email: basskozz@gmail.com
  author_url: http://basskozz.wordpress.com
  date: '2009-05-04 18:13:14 -0700'
  date_gmt: '2009-05-04 18:13:14 -0700'
  content: "Ditto,\r\nSee: \r\nhttps://bugs.launchpad.net/gnome-screensaver/+bug/275308\r\nhttp://bugzilla.gnome.org/show_bug.cgi?id=554247\r\nhttp://www.linuxquestions.org/questions/ubuntu-63/dual-monitors-wont-sleep-in-twinview-mode-723553/#post3529613\r\nhttp://ubuntuforums.org/showthread.php?t=930349\r\nhttp://basskozz.wordpress.com/2008/09/29/ubuntu-has-problems-with-power-saving-muti-display/\r\n\r\nI
    give up :-("
---
More specifically, why do gnome-screensaver and gnome-power-manager hate me? (But that was too long for a headline.)

I have had terrible luck with these punks doing what they're designed to do for at least 2 years now. Bugs get filed (usually someone else has filed it already), developers say "works for me" and they continue to fail to do the simple task endowed to them.

People familiar with my bashing of these two punks know that I blame it primarily on <acronym title="not-invented-here">NIH</acronym> syndrome and the twisted desire to remove all useful configurability from gnome. Plain vanilla DPMS has worked in X11 for a long time. xscreensaver got things ironed out too. Now gnome has to come along and redo everything because the user has too many options and the user might be able to get the screensaver to do what he actually wants.

I haven't complained about it publicly (i.e. here on this blog) before, because I thought I was a corner case. I have a dual screen setup where one screen is a TV, mythtv and mplayer enable and disable the screensaver regularly, etc. I figured I was just pushing it too far and it broke.

But then I set up this linux box here at school. It has one screen. I don't do anything special. I just want the screensaver to come on after N minutes and then to power off after M minutes. Even for gnome this should be an acceptable level of configuration right? And indeed the gnome-screensaver/gnome-power-manager configuration guis give me the illusion of being able to configure it this way.

But it doesn't work. At least, not all the time. I don't know what the problem is. I don't even know what the pattern of misbehavior is. Sometimes it works fine. Other times the power management never kicks in. At home, the screensaver itself often doesn't even kick in. When it does, the power management doesn't kick in half the time.

Today I woke up to find my desktop monitor at home had stayed on all night, displaying flying toasters for the cockroaches that have showed up early to the summer party. I sighed, but I wasn't surprised. Then I got to school and the desktop here was displaying the screensaver too. Double fail.

Please share your horror stories. Let's raise awareness. Let's pick a color and make ribbons. And if you happen to know how to fix these punks so that they invariably do what they're supposed to do—for the love of electrons please send a patch to the gnome developers.
