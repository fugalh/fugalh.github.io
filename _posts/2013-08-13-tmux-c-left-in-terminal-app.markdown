---
layout: post
status: publish
published: true
title: tmux C-Left in Terminal.app
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1314
wordpress_url: http://hans.fugal.net/blog/?p=1314
date: '2013-08-13 01:10:06.000000000 -07:00'
tags:
- linux
- osx
- control
- xterm
- TERM
- screen
- tmux
- xterm-256colors
- terminfo
- termcap
- arrow
- screen-256color
- Terminal.app
- escape
- ctrl
comments: []
---
I use Terminal.app on OS X, and I want to bind ctrl-left/right to cycle through tmux windows (<a href="http://hans.fugal.net/blog/2009/02/05/pimping-screen/" title="Pimping Screen">like I did with screen</a>).

The tmux incantation is easy to find online:

<code>bind-key -n C-Left prev
bind-key -n C-Right next</code>

This doesn't work though, because Terminal.app is sending <code>^[[5D</code> for left instead of what tmux expects. In my case, with <code>TERM=xterm-256color</code>, tmux is expecting <code>^[[1;5D</code> for C-Left and <code>^[[1;5C</code> for C-Right. You can change this in the Terminal.app settings. Ideally Terminal.app would magically send the right values based on the <code>TERM</code> setting, if there is such a thing as the right values in the world of terminfo and modified arrow keys.

I would prefer to tell tmux to accept <code>^[[5D</code> instead of <code>^[[1;5D</code>, which is what I did in my screen config, but I can't see any way to tell tmux to take a raw escape sequence instead of logical keys. I prefer that so that I don't have to remember (or research) magical incantations to configure Terminal.app the next time I start from scratch on OS X. So if you know how, let me know.
