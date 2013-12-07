---
layout: post
status: publish
published: true
title: Firefox Affords Not Installing
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 13
wordpress_url: urn:uuid:f583bb21-f7b5-4c64-be03-34594ce3eb5c
date: '2005-12-01 07:36:15.000000000 -08:00'
tags:
- cs
comments: []
---
<p>In usability and UI design theory there's this concept of <a href="http://www.joelonsoftware.com/uibook/chapters/fog0000000060.html">affordance</a>. We say the button affords clicking, or the metal plate on a door affords pushing. Well the latest Firefox .dmg for OS X (Firefox 1.5) strives to make the already dog-simple installation process (drag the .app into <code>/Applications</code>) even easier:</p>

<p><img src="/images/firefox_affords.png" alt="Screenshot"/></p>

<p>Doesn't that look great? It just begs you to drag it into the Applications folder. There's only one catch: <em>that's not the Applications folder!</em> That's a background image. It's completely worthless. It gums up your mind and prevents you from installing it on autopilot while you try to figure out why you can't just drag it onto that Applications folder.</p>

<p>In my case the confusion was exacerbated because I had recently come across a .dmg that used the same tactic, except they had a symlink to /Applications in there so it actually <em>was</em> dog-simple to install, instead of just <em>looking that way</em>.</p>

<p>10 points for style, -20 for stupidity.</p>
