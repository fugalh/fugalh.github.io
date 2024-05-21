---
layout: post
status: publish
published: true
title: udev, hotplug, and firmware, oh my!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 69
wordpress_url: urn:uuid:c081f8c9-94ca-4aaa-bf47-821c4bffabe4
date: '2005-11-21 08:31:10.000000000 -08:00'
tags:
- linux
comments:
- id: 1441
  author: pix
  author_email: ''
  author_url: ''
  date: '2006-07-03 11:25:23 -0700'
  date_gmt: ''
  content: |-
    <p>wow, just thought i would offset all of your comment-spam by saying this was a great tip. a good crashcourse in udev in addition to being (possibly) a solution to my current problem.</p>

    <p>thanks,
    pix.</p>
- id: 1442
  author: Hans
  author_email: ''
  author_url: ''
  date: '2006-07-03 11:26:00 -0700'
  date_gmt: ''
  content: <p>Oops, didn't realize I was collecting trackback spam. Deleted, and trackbacks
    disabled. Glad it worked for you.</p>
---
<p>My MIDI controller (read keyboard) is an M-Audio Radium 61. I love it. Although
it has standard MIDI jacks, I use the USB connection for computer use. It works
great in linux, with the hotplug scripts from <a href="http://usb-midi-fw.sf.net">http://usb-midi-fw.sf.net</a>.</p>

<p>That is, it <em>did</em> work great until udev decided to replace hotplug.</p>

<p>I like udev, I really do. I liked devfs too. I like superior technical
solutions, so although I had no issues with devfs, I welcomed our new dynamic
<code>/dev</code> overlords. But udev seems bent on world domination, and
seemingly has no desire to maintain compatibility with previous configurations
or older kernels. This would only be annoying, except as a Debian user I also
have to deal with Marco d'Itri's attitude if I have a problem. <em>Sigh</em></p>

<p>udev decided that hotplug was unnecessary and that it should do hotplug's job.
That's fine with me, really, but I just wish I had a little more warning and a
little bit better instructions on migrating my configuration. There, I've
ranted, and the rest of this entry will be technical details on what I did to
get my Radium working again.</p>

<p>The problem was simple, if not simple to diagnose: the firmware wasn't getting
loaded. The solution was not so simple. There's lots of posts on the web about
loading firmware with udev, but most of them give a udev rule that looks like
this:</p>

<pre><code>ACTION=="add", SUBSYSTEM=="firmware", RUN+="/sbin/firmware_helper"
</code></pre>

<p>There's two assumptions here that will do you no good if you're trying to get
your midisport firmware loaded: udev has no reason to think this device has a
firmware to be loaded, so <code>SUBSYSTEM=="firwmare"</code> will never be matched.
Secondly, <code>/sbin/firmware_helper</code> does not get distributed by Debian (but it
wouldn't do you any good if it did).</p>

<p>Luckily we can rely on the good ol' <code>midisport_fw</code> script that we used before, we just need to make a udev rule for it. Here is the rule for _my_ keyboard:</p>

<pre><code>$ cat /etc/udev/rules.d/013_midisport.rules
ACTION=="add", SYSFS{modalias}=="usb:v0763p1014d0001dcFFdscFFdpFFic*isc*ip*", RUN+="/usr/local/sbin/midisport_fw"
</code></pre>

<p>Let's dissect this. <code>ACTION=="add"</code> means match when the device is being added.
<code>SYSFS{modalias}</code> means match when modalias, found in sysfs, matches. This will
likely be unique for your keyboard, or at least for your model of keyboard. You
can do <code>cat /sys/bus/usb/devices/1-1/1-1:1.0/modalias</code> to get this. You will
need to replace <code>1-1</code> with the appropriate identifier in your situation: watch
syslog when you plug in the keyboard to discover it. Finally, we
tell udev to run the <code>midisport_fw</code> script. </p>

<p>For the udev smarties reading this: if you use <code>idProduct</code> and <code>idVendor</code>
instead of (or in addition to) <code>modalias</code>, the script will be called thrice,
and only the middle instance is wanted. However, the other two will fail to run
and so the net effect is two more lines in syslog complaining about an unknown
product.</p>

<p>And finally, if your keyboard is recognized by the
ALSA sequencer after loading the firmware, but no MIDI is sent, and you see the
following in syslog:</p>

<pre><code>kernel: usb_submit_urb: -28
</code></pre>

<p>Try using a different USB physical configuration. e.g. unplug other things from
the hub, or bypass the hub, etc. I spent hours fighting udev (so I thought)
when in reality the problem was an overloaded USB hub. Incidentally, -28 is
-ENOSPC (No space left on device), which is why I chased firmware issues with
udev for so long. </p>

<p>And finally, here's what a normal, working plug of my keyboard looks like in
syslog:</p>

<pre><code>Nov 21 07:15:20 falcon kernel: usb 1-1: new full speed USB device using uhci_hcd and address 2
Nov 21 07:15:20 falcon /usr/local/sbin/midisport_fw: load /lib/firmware/midisport//MidiSportKS.ihx for 763/1014/1 to /proc/bus/usb/001/002
Nov 21 07:15:25 falcon kernel: usb 1-1: USB disconnect, address 2
Nov 21 07:15:26 falcon kernel: usb 1-1: new full speed USB device using uhci_hcd and address 3
Nov 21 07:15:27 falcon kernel: usbcore: registered new driver snd-usb-audio
</code></pre>
