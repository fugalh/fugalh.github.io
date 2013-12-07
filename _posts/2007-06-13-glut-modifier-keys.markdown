---
layout: post
status: publish
published: true
title: GLUT Modifier Keys
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 846
wordpress_url: urn:uuid:114f9117-806f-4455-9f2d-f0dd82d224d2
date: 2007-06-13 15:50:00.000000000 -07:00
tags:
- flightgear
- glut
comments: []
---
<p>So, I'm hacking up a sweet joystick file. I thought, "Hey wouldn't it be nifty if I could make some buttons do different things if I'm pressing shift or control or something?" It's a known fact of life that you can never have too many joystick buttons.</p>

<p>Well, yes you can do that. But, no you can't. FlightGear itself lets you do that—you use the nasal function <code>getprop("/devices/status/keyboard/shift")</code>, for example. The only problem is that this doesn't work when FlightGear is compiled to use GLUT (vs SDL). </p>

<p>Apparently the geniuses that wrote GLUT don't believe that there is a way to get the state of a modifier key except in conjunction with another event (regular keypress, mouse event, etc.) Read <a href="http://www.nabble.com/Status-of-modifier-keys-%28shift-ctrl-alt%29-t2504316.html">the sickening truth</a> right here, where the problem is brought up on the freeglut-developer list, the "reasoning" against it is presented, there is a swift and sure rebuttal, and then silence. </p>

<p>So, I'm going to have to figure out how to get FlightGear to compile and run with SDL on OS X (so far it has eluded me, but I've got a few more tricks to try).</p>
