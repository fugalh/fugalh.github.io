---
layout: post
status: publish
published: true
title: JACK on the MacBook
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 971
wordpress_url: urn:uuid:4e0d75a8-b25e-408a-807a-dc844020cd2e
date: '2008-06-04 08:05:00.000000000 -07:00'
tags:
- linux
- mac
- macbook
- intel
- jack
- snd
- hda
comments:
- id: 1748
  author: Peter
  author_email: pashultz@gmail.com
  author_url: ''
  date: '2008-06-05 11:31:36 -0700'
  date_gmt: ''
  content: <p>Wow, thanks so much! I'm still fairly baffled by Linux audio, but your
    explanations made a lot of sense. Best of all, this solution works great on my
    1st-gen Macbook (Core Duo). Would it be all right if I posted a link to this from
    the Ubuntu Forums?</p>
- id: 1749
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-06-06 09:28:45 -0700'
  date_gmt: ''
  content: <p>Sure, go ahead.</p>
---
<p>I spent the better part of two days fine tuning my linux audio setup on my MacBook, so maybe I can save anothe MacBook user some time with this post.</p>

<p>The sound card in this thing is an Intel <acronym title="High Definition Audio">HDA</acronym> Controller, driven by the kernel module <code>snd-hda-intel</code>. Intel HDA cards (usually onboard cards) are looked down upon and generally derided, and I can testify with good reason. Like all sorry excuses for an audio card, it has only one subdevice which means only one application can use the card at a time. (If you want to know if your audio card is cheap, this is a good indicator&mdash;just look in <code>/proc/asound/card0/pcm0p/info</code> for <code>subdevices_count</code>)</p>

<p>Luckily in these modern times, the default ALSA device does software mixing
(dmix), so even on a cheap card you can usually hear more than one application
just fine. No, no, you <em>do not</em> need <a href="http://pulseaudio.org">PulseAudio</a> for this. In fact, PulseAudio
<em>steals the audio card</em> in its default configuration (at least on Ubuntu 8.04).
So if PulseAudio is running, applications that aren't PulseAudio aware (or ESD
aware) will simply not be able to make sound. There are other misbehaved kids
on the block, but they're fairly rare. The difference is that a well-behaved
application will grab the <code>default</code> ALSA device, instead of the first audio
card in the system explicitly, <code>hw:0</code>. PulseAudio in fact advises the use of
this trick, to set PulseAudio as the default ALSA device, which I suppose
explains why PulseAudio grabs <code>hw:0</code> by default. Unfortunately Ubuntu is only
halfhearted here&mdash;it enables PulseAudio but does not set up the default
ALSA device to point to it. So in Ubuntu you need to either set up the default
ALSA device with an <code>~/.asoundrc</code> that looks like <a href="http://www.pulseaudio.org/wiki/PerfectSetup">this</a></p>

<pre><code>pcm.!default {
    type pulse
}
ctl.!default {
    type pulse
}
</code></pre>

<p>or you need to configure PulseAudio to use the <code>default</code> device instead of <code>hw:0</code>. If you are going to be using JACK too (and you want to hear other applications outside the JACK pipeline when JACK is running), I recommend the latter, though if you're twisted enough you might try JACK as a PulseAudio client.</p>

<p><a href="http://jackaudio.org">JACK</a> also by default grabs <code>hw:0</code>, because JACK is all
about low latency and high performance and going through dmix adds a layer of
overhead. If you're using JACK, you may be enough of a snob that you're ok with
leaving those non-JACK applications out in the cold while JACK is running. In
fact you may not want to hear Pidgin sounds (for example) at all while you're
doing audio work. Semisnobs like myself, though, might want a compromise.
Setting up my studio just the way I want is enough of a pain, I really don't
want to quit all my JACK applications just so I can listen to <a href="http://www.last.fm/">Last.fm</a> or watch
<a href="http://www.homestarrunner.com/sbemail.html">sb_email</a>.</p>

<p>Now at this point I would be remiss if I didn't mention the very cool <a href="http://alsa.opensrc.org/index.php/Jack_(plugin%29">JACK
plugin for ALSA</a>. It allows
you to make well-behaved ALSA applications (the ones that use the default
device or allow you to configure which device is used) go through JACK. I modified my <code>.asoundrc</code> in a manner slightly different from the example given:</p>

<pre><code>pcm.jack {
        type plug
        slave {
                pcm {
                        type jack
                        playback_ports {
                                0 alsa_pcm:playback_1
                                1 alsa_pcm:playback_2
                        }
                        capture_ports {
                                0 alsa_pcm:capture_1
                                1 alsa_pcm:capture_2
                        }
                }
                rate 48000
        }
}
</code></pre>

<p>Then if you want to make the JACK plugin the default, you add</p>

<pre><code>pcm.!default {
    type plug
    slave.pcm "jack"
}
</code></pre>

<p>I tried configuring PulseAudio to use the JACK plugin, but it would crash on startup. Last.fm's client also had issues&mdash;it will play fine for one song and then crash <code>jackd</code> when the second song starts. So unfortunately it doesn't look like the JACK plugin for ALSA is quite ready for prime time, but you can certainly use it from time to time in applications that let you choose the ALSA device.</p>

<p>Unfortunately, the JACK plugin isn't found in Ubuntu's <code>libasound2-plugins</code> package where it belongs. It's an easy remedy, however, just install <code>libjack-dev</code> and <code>fakeroot</code>, then build the package from source (you don't even have to patch it):</p>

<pre><code>apt-get install libjack-dev fakeroot
apt-get build-dep libasound2-plugins
fakeroot apt-get source -b libasound2-plugins
sudo dpkg -i libasound2-plugins*.deb
</code></pre>

<p>Getting Ubuntu to not annoy you constantly about "upgrading" that package is another story.</p>

<p>Ok, so now to the meat of this post. JACK does not work well on this sound card
with its default settings. It either has an insane number of xruns, or it sounds terrible. For quite some time I chased the red herring of the
<code>position_fix</code> parameter to the <code>snd-hda-intel</code> module, and I can report with confidence that on this hardware you don't want to change it from the default (0, which is auto). However, if you are <em>only</em> concerned with JACK, you will want to change it to <code>position_fix=3</code>, which gives rock-solid JACK with the default settings on <code>hw:0</code>. However, although JACK or other direct-to-<code>hw:0</code> applications sound fine, dmix sounds crackly using <code>position_fix=3</code>. So it's probably not a good all-around solution if you're interested in more than just JACK.</p>

<p>The first order of business in good JACK performance (on any system) is to enable realtime. Edit <code>/etc/security/limits.conf</code> and add something like this:</p>

<pre><code>@audio - memlock unlimited
@audio - nice -10
@audio - rtprio 99
</code></pre>

<p>Now (after logging out and back in) you should be able to pass the <code>-R</code> option to <code>jackd</code> and get realtime.</p>

<p>If you do <code>jackd -R -d alsa</code> (unless you use <code>position_fix=3</code>) you will get lots of xruns. The best I have been able to do is <code>jackd -R -d alsa -p 512 -n 4</code>, as it seems that the trick is getting at least 3 periods (and to do that with <code>hw:0</code> you have to reduce the period size). This works well but qjackctl reports lots of xruns still. Actually, they're mysterious messages like this</p>

<pre><code>delay of 5152.000 usecs exceeds estimated spare time of 4071.000; restart ...
</code></pre>

<p>which don't actually cause an audio blip (but you will get an occasional real
xrun). I still need to try the realtime kernel (<code>linux-image-rt</code> package) to
see if that might help here. In my early tests (mostly playing with
<code>position_fix</code>) the realtime kernel was actually doing worse than the generic
kernel, but that was before I learned the number of periods should be at least
3, so I need to test again.</p>

<p>If you run <code>jackd -R -d alsa -d default</code> you will theoretically be able to use JACK and other applications at the same time via dmix/dsnoop. JACK will complain</p>

<blockquote>
    <p>You appear to be using the ALSA software "plug" layer, probably a result of using the "default" ALSA device. This is less efficient than it could be. Consider using a hardware device instead rather than using the plug layer. Usually the name of the hardware device that corresponds to the first soun</p>
</blockquote>

<p>[sic] but pay it no heed, we're doing this on purpose, and actually are able to get
better performance than the <code>hw:0</code> route (with <code>position_fix=0</code>). That command
will not actually work, though. It will crash within a minute even without any
clients. Again the fix seems to be the number of periods, but this time we can
avoid the excess delay by leaving the period size at 1024 (at the cost of some latency, of course). So, <code>jackd -R -d
alsa -d default -n 4</code>. This is rock solid. It went all night without a single
xrun. (But it wasn't doing much, though Ardour, Aeolus, and Hexter were
"running". I was able to play around with them for a half hour or so with no
xruns before I went to bed.) However, sometime down the road it will miss a
deadline and it will crash. This crashing seems to be specific to using dmix,
usually you'll just get an xrun. The workaround is to use softmode with the
<code>-s</code> switch. Now you can run JACK 24/7 with excellent performance and without
locking other applications out of the soundcard.</p>

<p>So in summary, if you don't care about dmix but only JACK (or any other application using <code>hw:0</code>, which can be all of them if you change your <code>.asoundrc</code>, but only one at a time), set <code>position_fix=3</code> for <code>snd-hda-intel</code>
e.g. in a file in <code>/etc/modprobe.d/</code> with a line like this: <code>options
snd-hda-intel position_fix=3</code>, and do <code>update-initramfs -uk all</code>. If you want a
more balanced setup, where you can have JACK running and other well-behaved ALSA applications can use the sound card, leave the module parameters alone and set up realtime and
use the following command to start JACK (or equivalent settings in QJackCtl): </p>

<pre><code>/usr/bin/jackd -R -dalsa -ddefault -r48000 -p1024 -n4 -s
</code></pre>

<p>If you want to use PulseAudio in this situation, configure it to use the <code>default</code> ALSA device instead of <code>hw:0</code>.</p>

<p>If you like PulseAudio and JACK both, the ideal situation would be PulseAudio using JACK as a backend, JACK using <code>hw:0</code> with <code>position_fix=3</code>, and the PulseAudio plugin as the default ALSA device. Unfortunately this is just a theoretical ideal, and doesn't work (yet) because of bugs.</p>

<p>And finally, if you have no or limited use for JACK, but want to use PulseAudio, just change your <code>.asoundrc</code> as above to make PulseAudio the default ALSA device, so that all applications, ESD aware or not, use PulseAudio.</p>

<p>Oh, and I almost forgot to mention the mixer. There's Master, PCM, Front, Surround, Center, LFE, Side, and various toggles. AFAICT the Front controls the internal speakers, and Surround controls the headphone volume. JACK on <code>hw:0</code> has 8 system ports. The first two correspond to the front speakers and the second two to the headphone jack. When you run JACK on <code>default</code>, it's simply stereo output, and goes to the speakers or the headphones if they're plugged in.</p>

<p>Finally, I regret to report that JACK on <code>default</code> will crash on resume (on <code>hw:0</code> it won't, at least with <code>position_fix=3</code>).</p>
