---
layout: post
status: publish
published: true
title: PulseAudio as a JACK Client
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 972
wordpress_url: urn:uuid:11dfb1dc-995c-458f-852a-ff6d1991cc7d
date: '2008-06-04 11:29:38.000000000 -07:00'
tags:
- audio
- linux
- jack
- pulseaudio
comments:
- id: 2117
  author: Roger
  author_email: roger.robertson.jr@gmail.com
  author_url: ''
  date: '2009-09-13 20:59:06 -0700'
  date_gmt: '2009-09-13 20:59:06 -0700'
  content: "Hello Hans, \r\n\r\nI am trying my best to get your instructions to work,
    but I think they're a little to cryptic for me. I tried the instructions you linked
    to, but pulseaudio starts with an error \"unable to load module-jack-sink\". If
    it's not too much trouble, could you give me a step by step account of how to
    get pulseaudio working with jack? I've read three of your posts on the matter
    and have had no success. Feel free to email me if you have any questions.\r\n-Roger"
---
<p>I spoke too soon about not being able to get PulseAudio working as a JACK client. I found <a href="https://tango.0pointer.de/pipermail/pulseaudio-discuss/2007-March/000330.html">this post</a> that tells you how to do it.</p>

<p>The key I think is <code>chmod -s `which pulseaudio`</code>. I didn't have to start the JACK transport rolling, so that may be antiquated information. I did have to build some packages from source, though:</p>

<pre><code>sudo apt-get build-dep pulseaudio
sudo apt-get install libjack-dev
fakeroot apt-get source -b pulseaudio
</code></pre>

<p>This creates a bunch of <code>.deb</code>s, including <code>pulseaudio-module-jack*.deb</code>. I just installed them all, but you can probably just install the jack module deb. Make the changes permanent by putting them in <code>~/.pulse/default.pa</code> or in <code>/etc/pulse/default.pa</code> and you're in business.</p>
