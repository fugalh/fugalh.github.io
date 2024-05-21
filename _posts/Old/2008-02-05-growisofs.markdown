---
layout: post
status: publish
published: true
title: growisofs
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 922
wordpress_url: urn:uuid:d156461b-7964-4726-8eb2-4651c6239f2a
date: '2008-02-05 17:57:59.000000000 -08:00'
tags:
- dvd
- wodim
- growisofs
- dual
- layer
comments:
- id: 1684
  author: Hualing
  author_email: hualing_huaa@yahoo.com
  author_url: http://www.artmonstergurl.org
  date: '2008-02-05 22:34:25 -0800'
  date_gmt: ''
  content: <p>I haven't tried a dual layer disc. Should it look like the old laser
    discs of the past? Thanks.</p>
- id: 1685
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-02-05 22:36:05 -0800'
  date_gmt: ''
  content: <p>No, they're only one-sided and the same size as a regular disc. Many
    movies on DVD, especially the ones with longer movies or more special features,
    are on dual-layer discs.</p>
---
<p>I've been burning DVDs with the aid of <a href="http://www.cdrkit.org/">genisoimage and wodim</a>. This usually looks like the following:</p>

<pre><code>genisoimage -J -r . &gt; ~/tmp/dvd.iso
wodim -v dev=/dev/dvdrw1 ~/tmp/dvd.iso
</code></pre>

<p>Today, I went to burn my first dual-layer disc, and found that wodim wasn't up to the task. I'm not sure why, but in my googling I found someone mention that wodim was having a problem burning dual-layer, gave an error message that looked a lot like mine, and said that growisofs was able to do the task just fine.</p>

<p>So I gave it a test. growisofs apparently combines both the mkisofs/genisoimage and the burning task in one. It looks like this:</p>

<pre><code>growisofs -dvd-compat -Z /dev/dvdrw1 -dvd-video ./
</code></pre>

<p>This one was a DVD-Video disc, hence the <code>-dvd-compat</code> and <code>-dvd-video</code> options. Sure enough, it burned just fine. So, someday when you try to burn a dual-layer disc, if wodim chokes on you, try growisofs.</p>
