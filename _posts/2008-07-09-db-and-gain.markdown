---
layout: post
status: publish
published: true
title: dB and Gain
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 987
wordpress_url: urn:uuid:1c9a21e1-2fd8-4d09-ae14-33e7763e91d7
date: '2008-07-09 12:35:00.000000000 -07:00'
tags:
- audio
- decibel
- db
- meter
- loudness
- peak
- ppm
- vu
- dpm
comments:
- id: 1764
  author: gabriel gunderson
  author_email: gabe@gunyd.org
  author_url: http://gundy.org
  date: '2008-07-09 17:05:05 -0700'
  date_gmt: ''
  content: <p>Great post.  I've been working on some recording myself and your post
    has cleared up a few things for this newcomer to audio.</p>
- id: 2436
  author: Hans
  author_email: ''
  author_url: ''
  date: '2011-11-04 00:20:34 -0700'
  date_gmt: '2011-11-04 00:20:34 -0700'
  content: http://www.murraypro.com/ppm_wfm.htm
---
<p>I've been studying up on audio recording on the web, so that I can make decent
recordings for <a href="http://hans.fugal.net/phd">my research</a>. Making good recordings is a lot more
involved than you might think. One of the perhaps needlessly overinvolved
aspects is understanding gain.</p>

<p>A microphone detects sound and produces a faint electrical signal, usually too
faint for practical use. So, the signal is amplified. But if you amplify the
signal too much, you get distortion. Once the signal passes from the analog to
the digital domain, you have forever lost some information, so the natural
thing is to get as much gain as you can before the A/D conversion.</p>

<p>So how do you know how much gain is enough but not too much? A good indicator is a peak meter. Here's a picture of an analog peak meter (called a PPM):</p>

<p><a href="http://www.murraypro.com/PPM.htm"><img alt='PPM' src='http://www.murraypro.com/PPM1.jpg' width='300'/></a></p>

<p>In the digital world, the practical equivalent looks something like this:</p>

<p><a href="http://ardour.org"><img src="/images/ardour-dpm.png" alt="DPM"/></a></p>

<p>We'll ignore the wacky scale on that analog meter for now. Notice the scale on
the DPM—it goes from 0dB at the top to about -70dB at the bottom. Now, decibel
(dB) is a <em>ratio</em>, meaning it has no meaning without some reference point. In
this case it's actually dBFS (dB full scale), calculated as dBFS =
20log<sub>10</sub>(|x|/1.0) when representing samples as floating point numbers
between -1.0 and 1.0. Whatever you divide by inside the logarithm is your
reference. You would divide by the maximum sample value if you were using fixed
point or some other representation. So our reference is 1.0, aka full scale.
Since we can't go over full scale, all dBFS numbers will be less than or equal
to zero.</p>

<p>So, if you record such that you are just below 0dBFS, you are using every bit
of quantization to its fullest. The trick is that you often don't know just how
high the maximum peak will be (unless perhaps you're recording something
repeatable, like playing back a tape). So, you need to leave a little
<em>headroom</em> in case you have some peaks that are larger than average. How much
headroom to use is hotly debated, but really it is just a function of the kind
of thing you're recording (and the environment in which it is being recorded).
There is no substitute for experience here. Here's a hint: record stuff with
plenty of headroom, find out what the maximum peak, and calculate how much
extra headroom you have. Do that a bunch, and you will begin to get an idea of
how much headroom you need.</p>

<p>Or, don't record that stuff, just watch a meter. Good digital meters will have
a resettable maximum peak indicator. </p>

<p>But there's more. The peak isn't a good indicator of how loud it is. Loudness
is perceived more closely to the average signal amplitude. The most common way
to calculate this is Root Mean Square (RMS): <code>sqrt(sum(x)/length(x))</code>. A common
meter which measures loudness (although it doesn't measure RMS, exactly) is the
VU meter. You may have seen it:</p>

<p><img alt='VU meter' src='http://upload.wikimedia.org/wikipedia/commons/f/f2/VU_Meter.jpg' width='300'/></p>

<p>The VU meter <em>does not measure peaks</em>, but it does measure loudness. But
there's a trick. 0 dB is not 0 dBFS, but rather 0 dBu, which in turn is usually
4dBV. Those are electrical voltage references for the analog world. In this
world, you aim for 0dB to be "forte", and it's ok if the meter <em>occasionally</em>
goes higher than 0dB. Remember the wacky scale on the analog PPM meter? It
reads dBV, i.e. 4 on the PPM is 0 dBu (but the marks are usually 4 dB increments, so 5 on a PPM would be +4 dBu).</p>

<p>So how do we relate these to the digital world? Well that depends on your ADC.
In practice there will be some variation in how the same strength (dBu) signal
is converted to digital, although the variation is probably not too great. The
important thing is to use the proper meter. When you're doing a digital
recording, the proper scale is dBFS and it's irrelevant what analog signal you
need to get the dBFS you need. Not entirely irrelevant—you want to make your
signal hotter earlier because that reduces the noise introduced by each
component in the system, but ultimately how much gain you apply (early in the
system) is governed by your digital meter.</p>

<p>But wait, aren't most digital meters peak meters? Yes, but there are loudness
meters if you look for them. On Linux and OS X with JACK, look at
<a href="http://www.kokkinizita.net/linuxaudio/downloads/index.html">jmeters</a> (a
derivative of the neglected <a href="http://plugin.org.uk/meterbridge/">meterbridge</a>).
At the time of this writing they it has VU and PPM meters, though you will have
to play with them to get the hang of their reference points. Or I could walk
you through it.</p>

<p>Go grab some <a href="http://www.abluesky.com/asp/catalogue/catalogue.asp?linkid=143">calibration
tones</a>.
Included in the zip available there are 1kHz sine wave at -20 dBFS RMS and
various pink noise tones (different bandwidths) at -20 dbFS RMS. But wait,
what's this?</p>

<pre><code>octave:1&gt; [x,sr] = wavread('1khz sine wave -20 dBFS.wav');
octave:2&gt; 20*log10(sqrt(sum(x.^2)/length(x)))
ans = -23.322
octave:3&gt; [x,sr] = wavread('PINK NOISE FULL bw -20 dBFS.wav');
octave:4&gt; 20*log10(sqrt(sum(x.^2)/length(x)))
ans = -22.908
</code></pre>

<p>Gee, looks like those are -23 dBFS RMS doesn't it? Well, technically they are.
But here's the rub: the smart people at the Audio Engineering Society declared
that in the analog world we should measure a sine wave with -20dB peak as -20dB
RMS, i.e. a sine wave has the same measurement on a peak and AES-17 RMS meter.
Whether they originated this or it came from history I don't know, but probably
the latter. So, since a sine wave has about 3dB crest factor, these test tones
have -23 dBFS true RMS, but -20 dBFS AES-17 RMS. Confused yet?</p>

<p>So we fire up <code>jmeters -t vu x</code> and <code>jmeters -t ppm x</code>, then hook up the JACK
connections and play the sine wave. The VU meter settles nicely on -10 VU and
the PPM reads 2. So it would seem that Fons has decided that 0 VU should be -10
dBFS, which gives 10 dB headroom. The gain is adjustable if you don't like that
choice, by the way.</p>

<p>Ok, so now you know enough about meters to be a little dangerous. Now let me
throw another wrench in things. Let's talk about <em>mastering</em>. After you record
all the tracks, you need to mix them together into songs and then finally
master the album. Mastering is (to oversimplify) all about loudness. You want
the songs to all fit together when you play the whole album. You don't want
some songs to sound too loud relative to others. Ideally, you'd want all albums
to have similar loudness. But you and I know that isn't usually the case. This
is the result of the "loudness war". Over the past 20+ years, albums have been
getting louder and louder and louder. Everyone wants the loudest-sounding
album. Everyone wants to be the baddest.</p>

<p>And bad they are. audio engineers have always mastered to take full advantage
of the medium. You can count on the highest peak usually being right up to the
clipping/distortion threshold. It's only right. But then how do things get
louder? Dynamic range compression. I won't go into the technical details of how
it works, and I exhort you to read up on it. Just Google <a href="http://www.google.com/search?q=loudness+war">loudness
war</a>. Suffice it to say
compression brings the peaks (and valleys) closer to the RMS. The loudness war
is a crying shame. So much music that could sound so good sounds so terrible
because the life has been compressed out of it. </p>

<p>So what does this have to do with metering? Well, the whole point of this post
is to inform you of the K-System meters. A smart audio engineer by the name of
Bob Katz (author of the newest book on my wishlist, <a href="http://www.amazon.com/exec/obidos/ASIN/0240808371/thefug-20">Mastering Audio</a>) proposes this system which borrows from history and other industries
that have standards which have protected them from the loudness wars. He
proposes 3 meters, the K-20, K-14, and K-12 meters. The number is the amount of
headroom above 0 dB, so a K-20 meter will set 0dB equal to -20 dBFS, and 0 dB
again means "forte". Then, you calibrate your studio monitors such that pink
noise that reads 0 dB RMS gives 83 dB SPL (sound pressure level) to your ears.
You need fancy equipment to do that, but unless you're mastering in a studio
(in which case you have the fancy equipment) it doesn't really matter. The CD
has dB FS, not dB SPL. If everyone did this, even if everone calibrated "forte"
to -20 dBFS, all the CDs would sound about the same loudness, there would be
plenty of dynamic range to make the music come alive, and the world would be a
happy place.</p>

<p>I have talked to Fons and he has been working on a K-20 meter for jmeters. I've
also been writing one with a simple <code>printf</code> display, which I will make
available once I get it working properly. The take-home lesson is to record
such that your highest peak is as close to 0 dBFS as you can get without
clipping, and master to forte (83 dB SPL) at -20 dBFS RMS.</p>

<p>But there's still that question of headroom. Why not just adjust the gain so
that forte is -20 dBFS RMS and be done with it? I'm not implying you wouldn't
have to master to get a professional-sounding recording (mastering is more than
just adjusting gain), but that it should give you a nice volume with enough
headroom. I think it's a great idea. I'm glad I thought of it (though I'm sure
I'm not the first). But make sure you're using as many bits as possible for
quantization, preferably 24 bits, since you are potentially sacrificing
bits for extra headroom.</p>

<p>I hope this little treatise was interesting and/or useful. To learn much more, I recommend starting at Bob Katz' articles on <a href="http://www.digido.com/bob-katz/level-practices-part-1.html">level practices</a>.</p>
