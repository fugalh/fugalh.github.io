---
layout: post
status: publish
published: true
title: Terminal Merge Conflict Resolution
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1171
wordpress_url: http://hans.fugal.net/blog/?p=1171
date: 2009-08-24 16:50:46.000000000 -07:00
tags:
- cs
- linux
- mac
- git
- diff
- distributed
- terminal
- merge
- ssh
- conflict
- resolution
- collaboration
comments:
- id: 2089
  author: Levi
  author_email: ''
  author_url: ''
  date: '2009-08-24 21:37:03 -0700'
  date_gmt: '2009-08-24 21:37:03 -0700'
  content: See the emerge section of the emacs manual for one possible emacs solution.  There
    may be others as well, but I tend to use a GUI tool for merging, so I haven't
    done a lot of looking.
- id: 2090
  author: HarleyPig
  author_email: harleypig@gmail.com
  author_url: ''
  date: '2009-08-24 22:05:10 -0700'
  date_gmt: '2009-08-24 22:05:10 -0700'
  content: "vimdiff can handle up to 4 files for diff handling.\r\n\r\n:h vimdiff
    in the editor"
- id: 2091
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-08-25 00:52:00 -0700'
  date_gmt: '2009-08-25 00:52:00 -0700'
  content: Sure, HarleyPig, make me go back and relearn why vim isn't up to the task
    and do another post about it. Thanks. :-P
- id: 2092
  author: Dexter
  author_email: cartkev@gmail.com
  author_url: http://dexterthedragon.com
  date: '2009-08-25 01:41:12 -0700'
  date_gmt: '2009-08-25 01:41:12 -0700'
  content: I use vimdiff for 3 way merges all the time, love it.
- id: 2093
  author: ''
  author_email: ''
  author_url: ''
  date: '2009-08-25 01:55:40 -0700'
  date_gmt: '2009-08-25 01:55:40 -0700'
  content: "M-x ediff-documentation\r\n\r\nGives information on the ediff functions
    in Emacs, which are fantastic."
- id: 2096
  author: vontrapp
  author_email: von@fugal.net
  author_url: http://von.fugal.net/blog
  date: '2009-09-03 17:04:07 -0700'
  date_gmt: '2009-09-03 17:04:07 -0700'
  content: What we really need is a vim library that allows you to open up a vim pager
    window within any ncurses program. Now that would be AWESOME!
- id: 2372
  author: gravedigger
  author_email: ''
  author_url: ''
  date: '2011-03-19 03:44:05 -0700'
  date_gmt: '2011-03-19 03:44:05 -0700'
  content: imediff does curses 3-way merge. no editing though IIRC.
---
A very important tool in the toolbox of any collaborating developer is a merge conflict resolution tool. OS X has the fantastic FileMerge, there are various graphical tools for linux like kdiff3, but I have yet to hear of one for the terminal. There's vimdiff, but it is really not up to the task of merge conflict resolution (doesn't handle 3-way diffs). There's probably something in emacs, just because there's always something for emacs. Emacs users please enlighten me, I'm not above using emacs for merge-conflict resolution. Might even be the gateway drug.

It doesn't seem overly hard (at least, no harder than writing kdiff3 or FileMerge) to make an ncurses tool that will take a 3-way merge and let you efficiently choose A, B, or edit for each diff section. Can it really be that nobody has done it yet?
