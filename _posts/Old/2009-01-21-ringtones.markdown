---
layout: post
status: publish
published: true
title: Ringtones
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1062
wordpress_url: http://hans.fugal.net/blog/?p=1062
date: '2009-01-21 19:25:02.000000000 -08:00'
tags:
- audio
- ringtone
- ring
- cell
- phone
- sound
- frequency
- audacity
comments:
- id: 1807
  author: Log-frequency Spectrograms | The Fugue
  author_email: ''
  author_url: http://hans.fugal.net/blog/2009/01/21/log-frequency-spectrograms
  date: '2009-01-21 23:01:20 -0800'
  date_gmt: '2009-01-21 23:01:20 -0800'
  content: '[...] asked me how I made my graphs in my ringtones post. I&#8217;d like
    to blather on about the graphs and why they&#8217;re cool and how you can make
    [...]'
- id: 1867
  author: sweet
  author_email: sweet@prince-of-ringtones.com
  author_url: 'http:'
  date: '2009-02-20 19:01:06 -0800'
  date_gmt: '2009-02-20 19:01:06 -0800'
  content: wow.  this is way more technical than I will ever get.  But thanks. :)
- id: 2155
  author: Jessica @ Ringtone downloads
  author_email: tom@backbonesolutions.com
  author_url: http://www.ringtones.co.za
  date: '2009-11-30 03:34:34 -0800'
  date_gmt: '2009-11-30 03:34:34 -0800'
  content: A nice look at the science of ringtones! I find single beeps or a series
    of beeps to be the most audible, but with a different frequency to normal so you
    can identify it as yours.
- id: 2241
  author: marvin
  author_email: none@none.com
  author_url: ''
  date: '2010-04-20 16:48:54 -0700'
  date_gmt: '2010-04-20 16:48:54 -0700'
  content: "Where do the echos above the main chrip-line come from? I would be glad
    if you loose some words about this...\r\n\r\nThanks for the great but simple idea!"
- id: 2242
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2010-04-20 16:56:03 -0700'
  date_gmt: '2010-04-20 16:56:03 -0700'
  content: Are you referring to the faint parallel lines to the chirp in the rerecordings?
    Those are probably resonances, e.g. resonances of the speakers or the microphone
    or the room or the desk or whatever. Or all of the above.
- id: 2243
  author: marvin
  author_email: none@none.com
  author_url: ''
  date: '2010-04-21 13:57:42 -0700'
  date_gmt: '2010-04-21 13:57:42 -0700'
  content: ok, thanks. So getting more resonances, means my specific mikrophone/speaker-combination
    is getting more resonances from somewhere (up to four faint lines in my case).
    Resonances are not good...
- id: 2244
  author: Hans
  author_email: ''
  author_url: ''
  date: '2010-04-27 16:23:56 -0700'
  date_gmt: '2010-04-27 16:23:56 -0700'
  content: It depends on what you are doing. If you're just investigating the frequency
    response of your cell phone, they're not hurting anything.
---
<p>This new phone is unique in all the cell phones I've owned or played with in that it isn't actually difficult to mp3s onto it and use them for ringtones. It's a <a href="http://www.motorola.com/motoinfo/product/details.jsp?globalObjectId=143">Motorola V195</a>. It supports Bluetooth (which is how I get the mp3s on it), but it also has a regular old USB port through which it charges and I take it allows transfer of files (if you don't have Bluetooth)—though I haven't confirmed that.</p>

<p>There must be an unwritten rule among cell phone companies that included ringtones must sound like they were written by a drunk adolescent pelican. So we want to put an mp3 ringtone on, but let's make it a good one. There are good mp3 ringtones and there are really bad mp3 ringtones, and there's very little middle ground.</p>

<p>Before I give you my criteria for a good ringtone, let's cover some background theory. Cell phone speakers are little and cheap. They've improved some over the years, but they're still a far cry from a good pair of desktop speakers let alone audiophile gear. So your mp3 will sound different on the phone than it does on your computer or even your headphones. How will it sound? That depends on the <em>frequency response</em> of the speaker in the cell phone. Since that's not likely included in your cell phone manual, let's see how we can measure it.</p>

<p>I whipped up this <a href="http://hans.fugal.net/sounds/logchirp.wav">chirp</a> in <a href="http://audacity.sf.net">Audacity</a>. It goes from 20 Hz to 20 kHz (the audible range) with a second of white noise on either side so you know when the thing starts and ends (since 20 Hz and 20 kHz are both out of the hearing range of most people). Its log-frequency spectrogram looks like this: (ignore the bleed at the low frequencies, it's an artifact of the log-frequency analysis)</p>

<p><a href="http://hans.fugal.net/images/logchirp.pdf"> <img src="http://hans.fugal.net/images/logchirp.jpg" alt="logchirp.wav" title="" /> </a></p>

<p>The astute among you will have realized that encoding this as an mp3 may change the spectrum. (I use the default settings to <a href="http://lame.sourceforge.net/">lame</a> throughout this post.)</p>

<p><a href="http://hans.fugal.net/images/logchirp-mp3.pdf"> <img src="http://hans.fugal.net/images/logchirp-mp3.jpg" alt="logchirp.mp3" title="" /> </a></p>

<p>It looks like the only relevant change is that encoding to mp3 cuts off the frequencies above about 17 kHz, which most people <a href="http://www.freemosquitoringtones.org/">don't hear well or at all</a>. So the experiment is still a go.</p>

<p>Now I put the chirp on my phone and played it back, recording it into Audacity on my laptop. The astute among you will again realize that the frequency response of my microphone makes a difference. Luckily my microphone has a <a href="http://www.mxlmics.com/manuals/900_series/MXL990Manual.pdf">decent frequency response</a> from 30 Hz to 20 kHz. Even if it didn't though, as long as the mic has a better frequency range than your phone you can still glean some important information. Here's the result:</p>

<p><a href="http://hans.fugal.net/images/v195.pdf"> <img src="http://hans.fugal.net/images/v195.jpg" alt="Motorola V195" title="" /> </a></p>

<p>Notice that there's basically nothing below about 250 Hz. To give you some perspective, 262 Hz is middle C (each tic mark on the Y axis is an octave, and the scale is logarithmic). So anything below middle C is severely attenuated, and the octave between middle C and high C is moderately attenuated.</p>

<p>For comparison, here is the chirp recorded on my desktop speakers.</p>

<p><a href="http://hans.fugal.net/images/speakers.pdf"> <img src="http://hans.fugal.net/images/speakers.jpg" alt="Speakers" title="" /> </a></p>

<p>See how it goes lower and also how it is flatter. There's not an appreciable peak at 8 kHz like there is with the cell phone. That means your high frequencies are going to stick out on a cell phone too.</p>

<p>Ok, so what does this mean for picking ringtones? It means steer clear of things that rely on low frequencies to sound good. Less obviously, it also means to try to steer clear of wide-band sounds that rely on lots of frequencies including low ones to sound good. That means drums! You also want something that is intelligible even across the room or in your pocket, and that means simplicity. Look for fun riffs on one or two instruments at the beginnings of songs, steer clear of human voices, bass, and thick mixes. If you want an approximate preview of what it would sound like on your phone, run it through a high-pass filter in Audacity and set the cutoff about 400 Hz. (Of course your phone may have a slightly different frequency response than mine, but the principles apply for almost all phones).</p>

<p>I won't go into a lot of detail about how to make a ringtone in Audacity, but I'll give you some general pointers. First, the length should be about 20–30 seconds (after trimming silence). If you want, time the time it takes to go to voicemail. Second, you should normalize the sound to peak at -3 dB (this might actually attenuate some overloud music). If the clip has a lot of dynamic range (louds and softs) you may want to run it through a compressor before normalizing, otherwise the soft will be lost on the bad speakers and noisy world. Penultimately, mix it down to 1 channel—your phone doesn't ring in stereo and while stereo files will probably work just fine it's just a waste of space. Finally, pick a medium quality encoding, too high a bitrate will probably be rejected by the phone and you don't need it.</p>

