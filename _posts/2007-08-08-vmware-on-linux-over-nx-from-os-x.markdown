---
layout: post
status: publish
published: true
title: VMware on Linux over NX from OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 860
wordpress_url: urn:uuid:f2a546ae-f603-49f6-a9bb-a1e1be5ec68a
date: 2007-08-08 10:22:00.000000000 -07:00
tags:
- linux
- mac
- vmware
- nx
- fusion
comments:
- id: 1596
  author: Clint Savage
  author_email: clint@utos.org
  author_url: http://www.utos.org
  date: '2007-08-08 11:53:16 -0700'
  date_gmt: ''
  content: |-
    <p>skewampus - I wondered how you spelled that anyway.</p>

    <p>I like this article.  I like the use of VMWare, but am curious if there isn't really a better alternative out there.  Must be because Mac only has a few options.  I know of parallels, busybox, KVM, Xen and others.  Do none of these work on a Mac?</p>

    <p>Cheers,</p>

    <p>Clint</p>
- id: 1597
  author: Scott Lowe
  author_email: scott.lowe@scottlowe.org
  author_url: http://blog.scottlowe.org
  date: '2007-08-08 12:10:10 -0700'
  date_gmt: ''
  content: |-
    <p>As far as Mac virtualization goes, there aren't too many players in town right now.  Parallels (with Parallels Desktop) was the first in the game, and now VMware has Fusion.  VirtualBox (which I understand is based on QEMU) has an OS X version available as well.  Parallels and Fusion work only on Intel-based Macs; I don't know about VirtualBox but I suspect it's the same.</p>

    <p>There's also a native port of QEMU called Q, which runs on both Intel-based Macs as well as PPC-based Macs.  However, I believe that it is still not fully virtualizing the CPU and therefore takes a performance hit as a result.  PPC-based Macs can also still use VirtualPC for the Mac, from Microsoft.</p>

    <p>Hope this helps!</p>
- id: 1598
  author: chucky
  author_email: ''
  author_url: ''
  date: '2008-01-17 14:09:49 -0800'
  date_gmt: ''
  content: |-
    <p>Thanks a lot for this article! </p>

    <p>greetings from Germany </p>
- id: 1599
  author: Alex
  author_email: ''
  author_url: ''
  date: '2008-04-05 13:18:11 -0700'
  date_gmt: ''
  content: <p>Great! Saved me a lot of time...thank you very much.</p>
- id: 1600
  author: Jim Blackler
  author_email: jimblackler@gmail.com
  author_url: http://jimblackler.net
  date: '2008-04-11 04:22:23 -0700'
  date_gmt: ''
  content: |-
    <p>Excellent, this <em>appears</em> to have solved my garbled keyboard (NX on OSX -> Ubuntu) problem.</p>

    <p>One thing, I didn't have a ~/.vmware/config file, so I modded the ~/.vmware/preferences file instead.</p>
- id: 1601
  author: /-djs-/
  author_email: djsaltarelli@yahoo.com
  author_url: ''
  date: '2008-11-14 22:18:43 -0800'
  date_gmt: ''
  content: |-
    <p>Yes, thanks for posting this.  I have a MacBook Air and a Ubuntu Hardy desktop/server machine with VMware Workstation 6.5 and this was truly a weird problem.</p>

    <p>/-djs-/</p>
- id: 1969
  author: Chirayu Krishnappa
  author_email: ck@chirayuk.com
  author_url: http://www.chirayuk.com
  date: '2009-04-29 20:23:07 -0700'
  date_gmt: '2009-04-29 20:23:07 -0700'
  content: Thanks a bunch!  I just faced the same problem and your post was the first
    thing I found on google.  It fixed the keyboard issue right away.
- id: 2358
  author: Brian
  author_email: ''
  author_url: ''
  date: '2011-01-31 14:55:01 -0800'
  date_gmt: '2011-01-31 14:55:01 -0800'
  content: FINALLY!  Thank you so much!
- id: 2383
  author: Lloyd
  author_email: other@s-squared-ranch.com
  author_url: ''
  date: '2011-04-07 19:48:07 -0700'
  date_gmt: '2011-04-07 19:48:07 -0700'
  content: "YES! It appears I am not the only one using OSX to talk to a Linux box
    :) - We be a bunch of smart people :)\r\n\r\nThis solved my problem (I found it
    previously but they didn't say WHERE to put the line GRRRRRR). Thanks! I can now
    log back into my VM without the bizarre remapping."
---
<p>I was a beta tester for <a href="http://www.vmware.com/products/fusion/">VMware
Fusion</a>. Fusion is a quality product,
as I've come to expect from VMware. Unfortunately, the beta is over and a
dialog box popped up when I tried to run it the other day. "The long wait is
over!" Yeah, I've been waiting with bated breath for my beta to stop working
until I fork over $40. You read my mind!</p>

<p>$60 ($40 after the current promotion) is the most affordable virtualization
option for OS X right now, and in my opinion the most technically superior to
boot. But I'm still a cheapskate, so I decided to use <a href="http://www.vmware.com/products/server/">VMware
Server</a> on Linux over
<a href="http://nomachine.com/">NX</a> instead. NX is indistinguishable from magic. It
works great, with one problem: the keyboard mapping in the virtual machine is
completely skewampus.</p>

<p>In googling for the answer, I found a few people who had trouble with a key
here or a key there. No, I had a completely unusable keyboard. e was the
backspace key, backspace was a comma, escape was a letter, and everything else
in between was equally unreasonable.</p>

<p>So I tried it over ssh (btw, it works a lot faster if you use <code>ssh -Y</code> instead
of <code>ssh -X</code>), and it worked fine. So the gauntlet was down.</p>

<p>After some stabbing in the dark, reading, more stabbing in the dark, more
reading, finally understanding, and one last stab in the dark, I got it to
work. The theory is in <a href="http://www.vmware.com/support/ws55/doc/ws_devices_keymap_linux_longer.   html">this
article</a>.
In short, VMware tries to map key codes to emulated PC scan codes (v-codes). If
it can't do that, it maps keysym codes to v-codes. The former is apparently
foolproof but isn't always an option. The problem here is that VMware thinks it
will work, but it won't (probably because Apple's X11 isn't XFree86). So we
simply need to put this in <code>~/.vmware/config</code>:</p>

<pre><code>xkeymap.nokeycodeMap = true
</code></pre>
