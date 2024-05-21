---
layout: post
status: publish
published: true
title: Linux on the MacBook
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 969
wordpress_url: urn:uuid:dfca3669-bfc5-4fdf-ad2e-14b49ed7c290
date: '2008-06-02 09:44:55.000000000 -07:00'
tags:
- linux
- mac
- macbook
- mactel
- boot camp
comments:
- id: 1746
  author: vontrapp
  author_email: ''
  author_url: http://von.fugal.net/blog
  date: '2008-06-02 12:32:51 -0700'
  date_gmt: ''
  content: <p>That's good to hear! Welcome back to the fold :) So does multifinger
    scrolling work, too? or just multifinger tap?</p>
- id: 1747
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-06-02 19:16:28 -0700'
  date_gmt: ''
  content: <p>Subject of another post, but in short yes I can do vertical and horizontal
    scrolling just fine, and the best documentation for it is <code>man synaptics</code>.</p>
---
<p>So now that I'm done with comps, it's time to start doing real research. In my case, that means playing with audio and MIDI.</p>

<p>Specifically, I'm going to be generating preliminary data by recording chromatic scales and musical works on <a href="http://www.kokkinizita.net/linuxaudio/aeolus/index.html">Aeolus</a>, an absolutely fantastic pipe organ synthesizer. I did get it ported to OS X (feel free to contact me about that, or just wait until the next release, he is integrating my patches), and <a href="http://ardour.org/">Ardour</a> works in OS X as well. But realizing that I wanted to record the same things with many different registrations (stop choices), I needed a MIDI sequencer, like <a href="http://www.rosegardenmusic.com/">Rosegarden</a>. Frankly, there just doesn't seem to be anything even close available on OS X that doesn't cost an arm and a leg (at least from a student's perspective). Combined with the fact that the OS X driver for my <a href="http://www.m-audio.com/images/global/manuals/Radium-series_Manual.pdf">Radium 61</a> seems to be buggy, I decided I need to go Linux.</p>

<p>OS X is supposedly the darling of multimedia types, but in my experience there is nothing like the wealth of interesting software available, for free, on the Linux Audio scene. And when it comes to audio stability and low-latency performance, there is nothing like a well-tuned Linux box. In short, I can't imagine doing serious audio work in anything but Linux.</p>

<p>So there are many guides out there for installing Linux on a MacBook, and I won't try to duplicate that information here. What I would like to do is detail what I had to do, and which choices I made.</p>

<p>The first choice is that of partitioning. In the end I decided to share the internal hard drive, giving 10G to linux. It looked like the easiest way to do that was with Boot Camp, although it appears possible without it. But Boot Camp Assistant just would not resize my OS X volume. It would either complain about files that couldn't be moved, or running out of disk space. I thought it might be running programs, so I shut them down. I thought it might be swap space so I rebooted. I thought it might work if I did it from the installation DVD. I thought maybe it needed more free space to do the shuffle. None of these fixed it. So I googled around and found that it might be possible for a file to be locked in position. So I needed to figure out what files were entrenched at the end of my HDD and see if I couldn't do something about that. I came across a not-free defragmenter, <a href="http://www.coriolis-systems.com/iDefrag.php">iDefrag</a> and fired up the demo. It processed the disk and eventually showed me a map of the sectors of the drive, and mousing over them I was able to see the files using those sectors. Near the end of the drive there were a lot of red sectors that all belonged to Google Desktop. I assumed red sectors probably meant stuff that couldn't be moved, but I couldn't be bothered to look it up. Google Desktop seemed like a logical lead, though. So I uninstalled it and gave the repartitioning a try, and it worked like a charm. Incidentally I like Google Desktop, as also Quicksilver and Spotlight (I use all three, depending on what I want to do), so I'll probably reinstall it. Oh, and I didn't defragment with iDefrag since the demo only defragments drives smaller than 100M. But just try finding that information on their website or in the README.</p>

<p>I then installed <a href="http://refit.sourceforge.net/">rEFIt</a>, which although not necessary is a nice way to bootload a dual-boot system.</p>

<p>I rebooted and chose to boot from CD in rEFIt. Odd, I just get a blank screen and no activity. I know this Ubuntu CD works on this very laptop because I had already tried it. So I rebooted and held down alt, which gave me the Apple boot chooser, and I chose the CD, and it worked fine. </p>

<p>I installed Ubuntu in the usual way. I manually partitioned, formatting the partition Boot Camp made for Windows as ext3 and not bothering with swap (I <a href="http://www.redhat.com/docs/manuals/linux/RHL-8.0-Manual/custom-guide/s1-swap-adding.html">made a swapfile</a> after installation). I told it to install the bootloader (GRUB) on the partition instead of the disk (the partition is <code>sda3</code>).</p>

<p>When I rebooted, I did the <code>gptsync</code> thing using the rEFIt "Partitioning Tool", which synchronized the legacy <acronym title="Master Boot Record">MBR</acronym> with the newfangled <acronym title="GUID Partition Table">GPT</acronym>. Then I tried to boot into Linux, and again rEFIt gave me a blank screen. I booted into OS X and googled it, finally stumbling across something that said that happened once or twice and then stopped happening. So I rebooted and sure enough, it worked the second time. That's odd, and not the end of booting troubles. Sometimes when booting Linux you get a kernel panic talking about APIC. I remembered this from early experiments last year, so I didn't panic. You just try try again until it works.</p>

<p>I will adorn this blog with a flurry of posts on the rest of my adventures soon, but for now suffice it to say I had Linux installed, and it has come a long way. Ubuntu 8.04 had wireless, multi-finger trackpad tapping (though I prefer two fingers to be the right button not the middle button), basic sound, video acceleration, and even suspend working out of the box. It's beginning to look like I could not only do my research in Linux, but maybe even make it the primary OS on my laptop the rest of the time too.</p>
