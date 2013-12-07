---
layout: post
status: publish
published: true
title: DPMS Triggers
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1011
wordpress_url: urn:uuid:b45688b0-38b6-41cf-81de-5494ae816b05
date: 2008-10-12 22:20:00.000000000 -07:00
tags:
- gnome
- brightside
- xset
- dpms
- standby
- power
- screensaver
- lock
- user
- script
- disable
- enable
- timeout
comments: []
---
<p>I'm sitting here having a really hard time figuring out whether I most dislike mosquitos or GNOME's screensaver and power management.</p>

<p>All I want is:</p>

<ol>
<li>Standard screensaver/power management stuff: you know, pretty pictures and/or turn off the monitor after a certain amount of time.</li>
<li>Allow me (user and/or script) to easily disable it, so that e.g. the screensaver doesn't come on in the middle of a video.</li>
<li>Allow me (user and/or script) to easily enable the screensaver and/or power management instantly.</li>
<li><em>Don't frickin' lock the screen!!!1!!</em></li>
</ol>

<p>Having found GNOME screensaver and power management completely incapable of doing the latter 3, even after installing and configuring Brightside, and digging through <code>gconf-edit</code> for the lock settings (hint: they're there but don't seem to work), I decided to resort to disabling them and using trusty old xset.</p>

<p>Now, Brightside will try to use GNOME's power management and/or screensaver, so if you want to avoid locking as I do you have to bypass that by using custom actions. The custom action for instant DPMS standby is <code>xset dpms force standby</code>. The custom action for DPMS disable is <code>xset -dpms</code> and then when leaving that corner do <code>xset dpms 600 1800 3600</code>. xset, or some GNOME monster, has a bug where <code>xset +dpms</code> doesn't work. It appears to work, i.e. <code>xset q</code> reports that DPMS was enabled, but it doesn't actually come on unless you explicitly set them (or force standby mode).</p>

<p>Now, you'll also want to run that same command at the beginning of your session, so what you probably want to do is script that (so you only have to change the timeouts in one place) and call that script from Brightside as well as put it in your session startup.</p>

<p>Being paranoid as I am, I took gnome power management out of my session (couldn't find gnome-screensaver in the session—maybe it's launched by the power manager?). But just telling them to never come on, and bypassing them in Brightside, should be sufficient.</p>
