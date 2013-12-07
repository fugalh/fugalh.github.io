---
layout: post
status: publish
published: true
title: IR Receiver
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 613
wordpress_url: urn:uuid:5dc2f56e-5f56-40c4-a75c-79bda8cd09da
date: '2006-06-24 11:52:00.000000000 -07:00'
tags:
- mplayer
- hardware
- diy
- ir
- lirc
comments:
- id: 1477
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-03-31 15:11:56 -0700'
  date_gmt: ''
  content: <p>More pictures at <a href="http://foton.fugal.net/album/18" rel="nofollow">http://foton.fugal.net/album/18</a></p>
---
<p>I've always been a software guy. I'm doing good if I can keep up with what good
computer hardware is. But a combination of needing a way to control mplayer
from the couch, poverty, and a desire to learn the useful skill of soldering
drove me to create my own serial IR receiver for use with
<a href="http://lirc.org">lirc</a>.</p>

<p>I was afraid my first soldering project would be a disaster, but it really has
turned out quite nice. At least, it's nice if you don't look at the back. :-)
Check out the pictures <a href="http://flickr.com/photos/fugalh/sets/72157594175920213/">on
flickr</a>.</p>

<p><img src="http://static.flickr.com/56/173915310_fbe9801bb8_m.jpg" alt="IR Receiver"/></p>

<p>I followed the instructions from <a href="http://www.linuxjournal.com/article/8811">the Linux Journal
article</a>, with some modifications. I
didn't want it inside a DB9 case, I wanted to show off my geeky creation so I
didn't cut up the perf board. I didn't want a DB9 connector, I wanted to use
cat5 cable and an <a href="http://www.ossmann.com/5-in-1.html">RJ45 to DB9 adapter</a>
that I had made previously. I used the IR Receiver from Radio Shack, <a href="http://www.radioshack.com/product/index.jsp?productId=2049727&amp;cp=&amp;origkw=infrared&amp;kw=infrared&amp;parentPage=search">model
276-640</a>.
The electronics store didn't have the precise voltage regulator called for but
had one with the same output that could handle higher voltage so I got that
instead. </p>

<p>If I were to start fresh, I would wish I had found <a href="http://lnx.manoweb.com/lirc/?partType=section&amp;partName=introduction">these
instructions</a>
instead. The LJ instructions are good, but these ones are better. I think I'd
still use perfboard anyway, since I'm not encasing it in a DB9 hood. </p>

<p>The version of <code>lirc-modules-source</code> in Debian testing at the moment didn't
work for some reason but the version from unstable works fine. I had a hard
time finding out what model my universal remote is, but I was able to create a
<code>lircd</code> config file for my DVD remote easy enough, and <code>irw</code> recognizes it
fine. </p>

<p>I still have to configure mplayer but there should be nothing special to that.
So I declare my IR receiver a success! Many thanks to Von for teaching me to
solder, Jared for helping me in the initial research, and Erin for not putting
up too much resistance to the idea.</p>
