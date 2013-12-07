---
layout: post
status: publish
published: true
title: Purging devfs
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 62
wordpress_url: urn:uuid:7c8cd077-9d13-42c2-b5ab-0399bb25526d
date: 2005-09-03 23:38:29.000000000 -07:00
tags:
- linux
comments: []
---
<p>When devfs first came out, it was cool and neat, and I liked the idea of not
having to wade through 1000+ entries in <code>/dev</code> so much that I jumped on the
bandwagon. Then udev came around and devfs bashing became the popular thing to
do. Eventually I was convinced of the technical merits of udev, and so
converted to udev.</p>

<p>Or so I thought. It turns out I had never quite done that on my desktop,
although I had deluded myself into thinking that I had. So when kernel 2.6.13
came around and ripped devfs out from underneath my feet, I fell flat on my
back. It turns out I had not only been running devfs all along up through
2.6.12, but somewhere along the line I had lost the real, static <code>/dev</code>. The
error I was getting was something along the lines of "Unable to open initial
console." </p>

<p>After some head scratching, googling, and false starts, it turns out the best
thing to do was to boot a rescue disk, mount the root partition, and copy over
<code>/dev</code>. (I did <code>rsync -a /dev/ /mnt/tmp/dev</code>).</p>

<p>One of my false starts was <code>MAKEDEV std hda hdb hdc hdd</code>.  In retrospect this
should have worked, but my delusion was so complete that I thought udevd was
being started at boot when indeed it was not, and only those devices were not
quite enough to get me booted. At that point I lost interest in just how
minimal a set of devices I needed, and copied them all over.</p>
