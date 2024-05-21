---
layout: post
status: publish
published: true
title: Decent Spaces
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 896
wordpress_url: urn:uuid:d6c78283-7294-48de-a539-6201f43f4e6b
date: '2007-11-06 12:30:35.000000000 -08:00'
tags:
- mac
- firefox
- leopard
comments:
- id: 1638
  author: Alex Esplin
  author_email: ''
  author_url: ''
  date: '2007-11-06 14:51:43 -0800'
  date_gmt: ''
  content: <p>It's good to know that the focus on switching spaces problem is a Firefox
    bug.  I've been rather irritated by that myself.  I have a friend who works at
    Apple, and I'll ask him if he can put a bug in someone's ear about that Vim keybindings
    for switching spaces.  All in all, Spaces is also one of my favorite features
    of Leopard too.</p>
- id: 1639
  author: Geektronica
  author_email: justin.baeder@gmail.com
  author_url: http://geektronica.com
  date: '2008-05-04 16:22:59 -0700'
  date_gmt: ''
  content: |-
    <p>Right there with you on the Firefox window focus issue - buggy.</p>

    <p>To "move me and this window to the () space" you can click and hold the title bar of the window, then hit ctrl+# (where # is the number of the space you want to move to).</p>
---
<p>One of the more drool-inducing features of Leopard (for geeks, anyway) is Spaces, Apple's virtual desktop implementation. I'm a big virtual desktop fan, and I'm glad to see it working its way into the mainstream. And all things considered, Spaces is a decent (and beautiful) implementation.</p>

<p>But there are some bugs. I hope that we will see them worked out. Some of the bugs are in Spaces itself, some are probably with 3rd party applications. The most notable, and annoying, problem is buggy application switching. When you cmd-tab to switch applications, you are taken to the space with that application. This is good, but it must have given the Apple developers heartburn because in some ways it flies in the face of the "Apple Way", which thinks of an application as a whole not as independent windows. That's why the menu bar is at the top, and it's behind the design of the dock. But what happens when there's a Terminal window on this Space, and on that Space? The natural thing <em>should</em> be, switch to the terminal window in this Space. If that's not what the user wanted, well you can't be expected to read minds. But when I cmd-tab to Terminal, I am always taken to what Leopard apparently thinks is the master Terminal Space, regardless of whether I have a Terminal window in this space, which Terminal window I last used, etc. Bad news. As a workaround, I just put Terminal on all spaces and thank my lucky stars it has tabs now. This affects most multi-window applications to some degree, but it's most annoying with Terminal and Adium.</p>

<p>On a related note, I'd expect cmd-` to switch between windows of the same app on different Spaces, but it only switches between windows on the current space.</p>

<p>Some applications, especially Firefox and to a lesser extent Thunderbird, have focus bugs that may be related to spaces. Sometimes when I switch to Firefox (with cmd-tab), the window is not in focus and is not brought to the foreground. The menu bar reflects that I'm in Firefox, and I may have moved spaces to get there, but it's in the background. I have to switch to it with cmd-` (or, horror of horrors, with the mouse). I imagine this is the sort of thing that Apple and/or Mozilla will hammer out soon. There are other Firefox irritations but they're for another post—if they haven't been fixed by then.</p>

<p>So far, nothing too surprising. Virtual desktops is hard to get perfect, and various Linux window managers have been floundering for years or even decades. Overall, I'd say they're off to a smashing start. I have two other more minor irritations. First, I'd like the current application to stay the current application when I switch spaces with the keyboard, instead of switching to the topmost application in the new space. This is because I often want to choose an application (by cmd-tabbing to it), then navigate to another space where I want to open a new window (e.g. Terminal). This is a design decision, of course, and one that people tend to fall on either side with about 50% probability. The second is keybindings. I'd like to switch spaces with cmd-ctrl-hjkl (Vim keybindings). Maybe we'll find a way. I'd also like to have more keyboard operations, especially "move me and this window to the {left,right,up,down} space".</p>
