---
layout: post
status: publish
published: true
title: 64-bit Transcoding
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 957
wordpress_url: urn:uuid:774b7210-22c2-485f-b425-216fb96e8717
date: '2008-04-20 10:38:24.000000000 -07:00'
tags:
- linux
- video
- ffmpeg
- '64'
- amd64
- i386
- transcoding
- bit
- '32'
comments:
- id: 2246
  author: Manish
  author_email: manish@manishbahl.com
  author_url: http://manishbahl.com
  date: '2010-05-11 16:40:02 -0700'
  date_gmt: '2010-05-11 16:40:02 -0700'
  content: "Hello,\r\nHave you looked any further into 64 bit transcoding?  I am look
    at options for transcoding and wanted to get some insight from others. Will 64bit
    make a significant difference?"
---
<p>I have a 64-bit desktop machine, that has rarely been run as a 64-bit machine. The hassle was too great and I couldn't really see a reason to put up with it.</p>

<p>I think that 64-bit support has come a long way in the meantime, and it may be time to try it out. It sounds like a livable situation. So with the pending release of the next Ubuntu version I'm thinking of wiping and going 64-bit.</p>

<p>One of the primary motivators is that 64-bit holds some promise for transcoding video, and now that I have an HDHomeRun to capture over-the-air HDTV signals, I will be doing quite a bit of video transcoding for MythTV (to save disk space—a full-quality HDTV program is about 9 gigabytes per hour).</p>

<p>But before taking the plunge, I thought I'd do an empirical test and see if there would be any real savings. I captured a couple of minutes of HD content from PBS, then transcoded 60 seconds using ffmpeg and mencoder. Then I did the same with the Ubuntu 64-bit live CD. The 64-bit execution difference was statistically significant.</p>

<p>ffmpeg was about 1.12 times as fast—a savings of about 10 seconds per minute, or 10 minutes per hour.</p>

<p>mencoder was about 1.08 times as fast—similar savings.</p>

<p>I didn't test mythtranscode itself, since getting it installed in a live CD environment would be too much work. I also must point out some other possible confounding variables. I used the Ubuntu 7.10 versions of ffmpeg and mencoder in 32-bit, and the Ubuntu 8.04 versions in 64-bit. Did both projects improve their code to be about 10% faster in the meantime? Unlikely, but perhaps not unfathomable.</p>

<p>So will I make the switch? I don't know yet. 10% faster is significant, but not obviously worth it. I'll have to think about it.</p>

<p>For the curious, here's my numbers. I did at least two runs of each to check for agreement, and what you see is the average. Of course, these would not be the settings you'd necessarily use to transcode—ffmpeg has a pretty low default bitrate for example—but I think we can agree the speedup is likely to be in the same ballpark no matter what settings you're using.</p>

<pre><code># 64-bit    32-bit
# 86 s      95 s
time ffmpeg -y -t 60 -i foo.avi -acodec copy bar.avi
# 55 s      64 s
time ffmpeg -y -t 60 -i foo.avi -acodec copy -s 640x480 bar.avi
# 83 s      90 s
time mencoder foo.avi -oac copy -ovc lavc -frames $[30*60] -o baz.avi
</code></pre>
