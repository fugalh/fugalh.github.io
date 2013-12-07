---
layout: post
status: publish
published: true
title: JACK on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 770
wordpress_url: urn:uuid:e455505f-d62d-4821-9808-53c486a748c7
date: 2006-12-21 08:34:54.000000000 -08:00
tags:
- audio
- mac
- jack
comments: []
---
<blockquote>
    <p><a href="http://jackaudio.org/">JACK</a> is a low-latency audio server, written for POSIX conformant operating systems such as GNU/Linux and Apple's OS X.</p>
</blockquote>

<p>If you're doing serious audio work, JACK is a beautiful thing indeed. I had a problem getting it going on the MacBook. I didn't have any trouble with it on the iBook, so either JACK changed, or a recent OS X update changed things, or just the fact that the MacBook has both a line in and a microphone canged things.</p>

<p>This is the error I was getting:</p>

<pre><code>$ jackd -d coreaudio
jackd 0.102.20
Copyright 2001-2005 Paul Davis and others.
jackd comes with ABSOLUTELY NO WARRANTY
This is free software, and you are welcome to redistribute it
under certain conditions; see the file COPYING for details

JACK compiled with POSIX SHM support.
loading driver ..
Default input and output devices are not the same !!
Cannot open default device
Cannot open the coreaudio driver
cannot load driver module coreaudio
no message buffer overruns
</code></pre>

<p>You can see the <a href="http://music.columbia.edu/pipermail/linux-audio-user/2006-December/041181.html">thread on LAU</a> for more details, but the short answer is you need to create an aggregate device in the Audio MIDI Setup panel. Open it up and go to the Audio Devices tab. Then go to the Audio menu and choose Open Aggregate Device Editor. Add ye an aggregate device with all the inputs/outputs, and JACK will just work. Not only that, but it will have access to all the available inputs and outputs.</p>
