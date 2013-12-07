---
layout: post
status: publish
published: true
title: VMware Server
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 685
wordpress_url: urn:uuid:76aa668a-fa39-47e2-a156-b5dd307069ae
date: 2006-07-28 21:08:17.000000000 -07:00
tags:
- vmware
- free
- virtualization
comments:
- id: 1504
  author: Gabriel Gunderson
  author_email: gabe@gundy.org
  author_url: http://gundy.org
  date: '2006-07-28 23:39:01 -0700'
  date_gmt: ''
  content: |-
    <p>I too dig vmware.  I'm a <em>paying</em> customer.  It's the only way I'll run windows.  I make two base images.  One fresh install and another with any applications that I may need.  Rather then reinstall Windows when it gets messed up beyond repair, I just go back to that clean state.  I really only use Windows to test interoperability with Linux any more.</p>

    <p>Anyway, when going virtual with Linux on Linux, nothing beats Xen.  It's everything that you like about Linux applied to virtualization.  You get clean command-line tools, transparency, script-ability, total control and it's Open Source.  Your guilt serves you well ;)</p>

    <p>P.S:
    gundy.org/2006/01/05/vmware-gets-my-money/</p>
---
<p>In the process of moving apartments, I decided to do a little rearranging of
computers too. As part of that process, I decided to try and get rid of the
dual boot by running Windows in virtual machine. Not long ago I had heard that
VMware had a free product, so I went on over to their site and checked out
<a href="http://www.vmware.com/products/server/">VMware Server</a>.</p>

<p>I ran the installation script in the tarball and answered a bazillion questions
with the defaults (except I replaced <code>/usr/bin</code> with <code>/usr/local/bin</code>) and
fired it up. This is one slick program. I installed Windows 2000 Professional
and did the standard after-install stuff. (Firefox, Thunderbird, AVG free,
Cygwin, 7-Zip) I can suspend and resume my windows box at will. I can run it
full screen or in a window. Nothing is broken. I have a bridged network
connection, no fancy networking tricks (although you do have that option). It's
fast, completely usable (although it might not play bzflag well, of course). In
short, it's like dual booting without the hassle. I highly recommend checking
it out. It's also going to come in handy when I get a chance to repackage
Csound for Debian, as a pure clean Debian sid VM.</p>

<p>Imagine my surprise when I read on LWN that VMware Server is a <a href="http://www.vmware.com/news/releases/server.html">brand new free
offering</a>. Imagine that, I
just tried it out at the perfect time to review it. So there you have it, my
shining positive review. </p>

<p>Part of me is slightly guilty that I didn't even try Xen, but VMware has a
reputation even among people like me who've never tried it, and I wanted to see
for myself. Having been through the process of VMware, I must say Xen would
have to be very much more polished indeed than it was when I saw it presented
at PLUG to hold a pragmatic candle to VMware Server. But I do hope they keep at
it.</p>
