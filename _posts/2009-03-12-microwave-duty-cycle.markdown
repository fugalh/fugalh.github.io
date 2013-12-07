---
layout: post
status: publish
published: true
title: Microwave Duty Cycle
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1118
wordpress_url: http://hans.fugal.net/blog/?p=1118
date: 2009-03-12 03:33:01.000000000 -07:00
tags:
- food
- cooking
- power
- microwave
- duty
- cycle
- period
- seconds
- level
comments:
- id: 1901
  author: eggyknap
  author_email: ''
  author_url: http://eggyknap.blogspot.com
  date: '2009-03-12 15:33:54 -0700'
  date_gmt: '2009-03-12 15:33:54 -0700'
  content: But can you prove *my* microwave is *also* linear? Sounds like there's
    more work to be done here... :)
- id: 1902
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-03-12 15:40:20 -0700'
  date_gmt: '2009-03-12 15:40:20 -0700'
  content: Not my problem. ;-)
- id: 1904
  author: Alex
  author_email: alex.esplin@gmail.com
  author_url: ''
  date: '2009-03-13 03:16:38 -0700'
  date_gmt: '2009-03-13 03:16:38 -0700'
  content: totally awesome.  Now I'm gonna have to do that with my microwave...
- id: 1915
  author: Ryan Byrd
  author_email: ryanbyrd@gmail.com
  author_url: http://www.ryanbyrd.net
  date: '2009-03-24 17:49:25 -0700'
  date_gmt: '2009-03-24 17:49:25 -0700'
  content: you are probably the biggest nerd I've ever met. :)
- id: 1916
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-03-24 17:57:18 -0700'
  date_gmt: '2009-03-24 17:57:18 -0700'
  content: But do you mean that figuratively or literally? Or both?
- id: 1924
  author: Ryan Byrd&#8217;s Ramblings &raquo; nerds like us
  author_email: ''
  author_url: http://www.ryanbyrd.net/rambleon/2009/03/31/nerds-like-us/
  date: '2009-03-31 22:04:16 -0700'
  date_gmt: '2009-03-31 22:04:16 -0700'
  content: '[...] But one day, perhaps while waiting for a delicious TV dinner to
    thaw, he began thinking about magnetrons. The magnetron, you might know, is the
    device that zaps your food and warms it up by making the [...]'
- id: 1927
  author: Sometimes you run into something on the web&#8230; | MrBlog
  author_email: ''
  author_url: http://mrblog.nl/2009/04/03/sometimes-you-run-into-something-on-the-web.html
  date: '2009-04-03 10:53:07 -0700'
  date_gmt: '2009-04-03 10:53:07 -0700'
  content: '[...] Microwave Duty Cycle | The Fugue [...]'
---
As you may know, when you change the power setting on most microwaves, it doesn't change the power output of the magnetron. It changes the duty cycle, i.e. when the magnetron is on and when it is off.

In a bout of curiousity I sat down with my microwave today and figured out exactly what those duty cycles are (you can hear when the magnetron switches on and off). My microwave apparently has a cycle period of 32 seconds. High is power level 100 and the magnetron is on all the time. Power level 50 is on 18 seconds and off 14 seconds. Power level 40 is on 16 and off 16 (which I would have guessed would be the case for power level 50). Power level 10 (the lowest setting) is on for 6 seconds and off for 26 seconds. Here's a graph with all 10 settings:

<a href="/images/microwave.pdf"><img src="/images/microwave.png" alt="Microwave Duty Cycle" /></a>

As you can see it's more or less linear, which is nice because it makes mental visualization easy.

Now you know.
