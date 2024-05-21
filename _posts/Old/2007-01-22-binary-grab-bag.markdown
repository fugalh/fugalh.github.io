---
layout: post
status: publish
published: true
title: Binary Grab Bag
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 777
wordpress_url: urn:uuid:3cffcedc-7380-4f2c-ad7e-05d58f214788
date: '2007-01-22 14:24:19.000000000 -08:00'
tags:
- binary
- grab bag
comments:
- id: 1531
  author: Dan
  author_email: ''
  author_url: ''
  date: '2007-02-06 22:02:03 -0800'
  date_gmt: ''
  content: <p>You are hilarious. This is awesome. :)</p>
---
<p>The <a href="http://uug.byu.edu/">BYU UUG</a> ha[sd] a fun little tradition. Everyone would get a number (generally by counting off) and then they'd flip a coin once for each bit to pick the number for the winner, who got to draw from a bag of (often useless) stuff. The idea is simple enough and carries over from meeting to meeting, year to year. Unfortunately there's a minor bug in the problem that can really annoy the perfectionists: what if the number of people isn't a power of 2? Sometimes people would volunteer to sit out. Sometimes you'd go through flipping the number all over. Sometimes you'd just reflip the last bit (leading to a non-uniform distribution) if necessary. </p>

<p>Well I have a better solution. It's simple, even more fun, and only requires a slight amount of forethought. Count off as before, but every time you pass a power of two have the person come to the front. So the first person, the third person, the fifth person, the ninth person, etc. Or you can just have k random people stand up front. (k is <acronym title="ceiling of log base 2">lg</acronym> n, where n is the number of people participating) Line them up and determine which side is the LSB (a short but entertaining argument about endianness ensues), then everybody flips a coin at the same time. Write up the bits on the board and figure out who wins. If it's a miss, everybody flips again. </p>

<p>There are several advantages. It's a completely uniform distribution. More people are involved, so more fun is had. People might drop coins which is always good for a laugh. Arguing over endianness is always fun. It's faster than flipping the same coin repeatedly to get the number. (The expected number of flips to get a hit is only 2.)</p>

<p>The only disadvantage is somebody has to remember to bring enough coins. But somebody already has to remember to bring the grab bag in the first place, and usually you can scrounge up k coins in an emergency anyway, so I think it's acceptable risk.</p>
