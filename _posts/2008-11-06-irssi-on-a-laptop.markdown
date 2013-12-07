---
layout: post
status: publish
published: true
title: Irssi on a Laptop
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1018
wordpress_url: urn:uuid:430e4174-113e-4e1b-8a5e-87acd1c542bc
date: 2008-11-06 08:42:00.000000000 -08:00
tags:
- mac
- chat
- irc
- irssi
- colloquy
- x
comments:
- id: 1788
  author: madmax
  author_email: madmax.ptz@gmail.com
  author_url: ''
  date: '2008-11-25 12:06:10 -0800'
  date_gmt: ''
  content: |-
    <p>Just a notice, you <em>can</em> use Growl with irssi, I use it for hilights :-)</p>

    <p>Not sure the steps I took to make it work, but look around, here for instance: <a href="http://plungeintomac.com/blog/hooking-up-irssi-to-growl/" rel="nofollow">http://plungeintomac.com/blog/hooking-up-irssi-to-growl/</a></p>
- id: 1896
  author: Leo
  author_email: leo@con.ca
  author_url: ''
  date: '2009-03-06 01:35:27 -0800'
  date_gmt: '2009-03-06 01:35:27 -0800'
  content: I used to use MacIrssi, which seems to be one of those irssi wrapped in
    Cocoa type of applications. I eventually settled for running irssi on my server
    and using Terminal.app to access it (re-attach screen and off we go). My goal
    now is to find a theme that's good to the eyes and that works with Terminal.app.
    My favourite theme, hv.theme, doesn't work properly in Terminal.app but will work
    elsewhere on other platforms or programs. Go figure.
---
<p>I love <a href="http://irssi.org/">irssi</a>, but it has laptop issues. It's really unintelligent about network disconnects and waking up from sleep. It usually either takes forever to time out and try to reconnect, or tries to reconnect immediately upon wake before the wireless connection is established and then takes forever to time out and try to reconnect. So I tried it in <a href="http://www.gnu.org/software/screen/">screen</a> on my server, and that works fine, but it lacks some usability features. Plus, it lacks some niceties that I've come to <em>need</em> on OS X from chat clients. I need my chat client to use <a href="http://growl.info/">growl</a> to tell me when someone talks to me (directly to me, in the case of IRC). Then I can read the message quickly and decide whether I need to stop what I'm doing right then to respond, or if it can wait a few seconds while I complete my thought, or if it can wait a few minutes while I complete my thought. Plus, with the right theme, growl notifications can be easy to tune out as well (but your mind still registers that <em>something</em> happened and wants your attention, when you can give it).  Second, it's really nice to have IRC in a different application, so it can be hidden without affecting the rest of the Terminal.app windows. I use the terminal too heavily for productive work for IRC to insert itself on a terminal tab or in a terminal window. But, I could work with this by starting irssi in its own window and getting used to minimizing IRC. Not a deal-breaker.</p>

<p>I've been using <a href="http://colloquy.info/">Colloquy</a>, and before that <a href="http://xchataqua.sourceforge.net/twiki/bin/view/Main/WebHome">X-Chat Aqua</a>, and while both meet the essential needs listed above (smart reconnect after sleep and growl), the both have the same problem: they're not irssi (plus they don't get much attention from the developers, and X-Chat Aqua is all but officially abandoned). Colloquy in particular crashes more frequently than a demolition derby car. So I find myself yearning for irssi. There are a couple wrap-irssi-in-cocoa apps, but they are also abandoned and incomplete.</p>

<p>In one last stab of hope, has anyone discovered a way for irssi to be intelligent about reconnecting? This is just as applicable in linux as in osx, and I know a lot of you linux users have laptops and use irssi—do you all just punt and use it in screen on a server? Has anyone found/written an irssi plugin for growl? (I assume someone probably has, or that it would be easy to whip up, but I haven't bothered to look because I haven't found the solution to the first problem yet.) Or, has anyone found an IRC client that actually comes close to being as awesome as irssi, reconnects intelligently, uses growl, and doesn't crash frequently?</p>
