---
layout: post
status: publish
published: true
title: Authoring DVDs
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 772
wordpress_url: urn:uuid:fcb6c6ce-88d0-4f7d-84fa-2f9930fe9e80
date: '2006-12-24 00:45:56.000000000 -08:00'
tags:
- linux
- mplayer
- dvd
- ffmpeg
- mpeg2enc
- dvdauthor
comments: []
---
<p>Scenario: you have a bunch of avi files (or whatever) that you want to make into a DVD. They may be episodes of your favorite comedy that you recorded with MythTV and want to keep around but not on your hard disk. They may be home videos. Whatever.</p>

<p>There are commercial programs to do this, and they are either expensive or inflexible and for any of a million reasons they don't meet your need. What do you do? There's a lot of good information about the details out there, with the exception of how to transcode your video, so I will give the overview, some links, and details on how to transcode.</p>

<p>First, what a DVD is. It's an ISO9660 filesystem following a certain convention. That convention is that stuff has certain names in a certain filesystem layout, and that stuff is encoded in certain ways. But it's just a regular filesystem underneath. If you look at a DVD in the shell you can see what I mean.</p>

<p>Assuming you want to play video DVD on your Wal-Mart-purchased consumer electronics, you need to get your video into an MPEG-2 video with AC3 or PCM audio at 48khz, with the appropriate frame rate for your TV and the correct size and aspect ratio. The <a href="http://www.mplayerhq.hu/DOCS/HTML/en/menc-feat-vcd-dvd.html">mencoder docs</a> have a nifty table showing what you need to decide. Once you've decided, use <code>ffmpeg</code> to transcode. It's not hard: <code>ffmpeg -i in.avi -target ntsc-dvd -acodec ac3 out.mpg</code>. You can change the bitrate with the <code>-b</code> option (see the myriad bitrate calculators online if you're trying to squeeze things. I've found the bitrate calculator in ffmpegX to be the best to use, if you have OS X). You can change the audio bitrate, e.g. <code>-ab 192</code>. You can change the size from "full DVD" to "half DVD" with <code>-s 352x480</code>. You could play with lots of options. What's important is that you see something like this:</p>

<pre><code>Output #0, dvd, to 'out.mpg':
Stream #0.0: Video: mpeg2video, yuv420p, 352x480, q=2-31, 1703 kb/s, 29.97 fps(c)
Stream #0.1: Audio: ac3, 48000 Hz, stereo, 256 kb/s
</code></pre>

<p>If it doesn't look right, it's time to double check the options and the <em>order</em> of the options. That one bit me, but it's right there in the manpage: </p>

<pre><code>ffmpeg [[infile options][-i infile]]... {[outfile options] outfile}...
</code></pre>

<p>If it looks right, but mplayer doesn't seem to grok the output, then get a new ffmpeg. I had one (ffmpeg from darwinports) that would seem to do everything right but somehow leave out or corrupt the audio, so my transcoded videos had no audio. So I compiled my own from SVN.</p>

<p>Once you have transcoded the videos, it's time to use dvdauthor to make menus and create the DVD filesystem. It'll take a little work and XMLing, but it's well-documented online. Then you need to burn your image to a DVD.</p>

<p>But before you burn, try it out in-place with your favorite DVD watching program. Pointing it at the <code>VIDEO_TS</code> directory or perhaps <code>VIDEO_TS/..</code> should do the trick. If it loads and plays, you're probably good to go. Burn and test. Get out that sharpie and decorate. Enjoy your newfound sense of accomplishment!</p>
