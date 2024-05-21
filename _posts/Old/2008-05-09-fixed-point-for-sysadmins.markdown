---
layout: post
status: publish
published: true
title: Fixed Point for Sysadmins
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 959
wordpress_url: urn:uuid:da9d0212-7f80-40e3-aa94-0e3f9b5dc763
date: '2008-05-09 08:31:00.000000000 -07:00'
tags:
- cs
- sysadmin
- theory
- fixed
- point
- package
- deb
- rpm
comments: []
---
<p>In CS language theory we sometimes talk about fixed points. Everyone seems to have a bit of a hard time understanding what a fixed point is at first, and I thought of an interesting analogy just now that will make sense to sysadmins.</p>

<p>When you go to install foo, with <code>apt-get install foo</code>, apt will tell you all the dependencies it will install, and it will also tell you the recommendations and suggestions, then ask for your permission. You might decide to say no and repeat the command with one or more of the suggestions added. Then it will do the same, but now with the suggestions of the suggested packages as well. You might repeat a couple of times. Finally, you will be happy with the selection of packages you're going to install. You've found the fixed point. </p>

<p>Apt itself does the same thing when resolving dependencies. If you remember rpm-based distros before apt-alikes, you used to have to find the dependencies fixed point by yourself. We called this rpm hell for good reason.</p>

<p>So when you're finding a fixed point in math, you're doing a similar thing. You're repeatedly performing the operation until further operations don't change the answer. The fixed point of a function f(x) is x<sub>0</sub> such that f(x<sub>0</sub>) = x<sub>0</sub>.</p>
