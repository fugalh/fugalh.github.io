---
layout: post
status: publish
published: true
title: FFTW Wisdom
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1022
wordpress_url: urn:uuid:4cac3904-9720-49ed-9968-949d48fb9575
date: '2008-11-12 10:19:00.000000000 -08:00'
tags:
- octave
- planner
- fftw
- wisdom
- fft
- fourier
- transform
- patient
- exhaustive
- estimate
- speed
- optimize
comments: []
---
<p>The <a href="http://fftw.org/">Fastest Fourier Transform in the West</a> has some internal parameters for fine tuning exactly how it performs the FFT. For optimal results, you measure the effect of these parameters directly to find the absolutely optimal way to do that transform, but this is overhead that usually takes longer than just doing the transform the "slow" way, so it is only worth doing when you will be doing a whole bunch of similar transforms (e.g. in a spectrogram, filter, etc.).</p>

<p>So FFTW uses different planners, e.g. "patient" and "estimate", the latter being the default. No matter which planner you use, FFTW gathers "wisdom" about plans and doesn't have to recalculate them in the same session. Additionally, this wisdom can be saved to disk (in <code>/etc/fftw/wisdom</code>).</p>

<p>FFTW ships with <code>fftw-wisdom</code>, a program to generate wisdom which you can save to disk for the benefit of all FFTW-using programs. You run it something like <code>fftw-wisdom -c -v -o /etc/fftw/wisdom</code>, which takes several hours. I did this, and I found that the generated wisdom refused to be read. Oops. So I have done something almost as good (and which takes much less time).</p>

<p>In my case, I usually use FFTW within <a href="http://www.gnu.org/software/octave/">Octave</a>. I'm sure it's in use many other places (video and audio encoders/decoders, etc.) but when I care about the marginal speed gains it's usually in Octave. Octave gives you access to the wisdom and planners, so you can save the wisdom to disk. Set the planner to "patient" (or "exhaustive" even):</p>

<pre><code>octave:1&gt; fftw('planner','exhaustive');
</code></pre>

<p>Then we need to perform an FFT for each plan that we care to optimize. Octave (and MATLAB) only seem to do complex-to-complex transforms, first transforming real data to complex, so all we need to do is generate a vector and perform the FFT for the various sizes we care about. In my case (audio) this does the trick:</p>

<pre><code>octave:2&gt; x = rand(2^15,1);
octave:3&gt; for i=1:15; fft(x,2^i); end
octave:4&gt; fftw('dwisdom')
ans = (fftw-3.1.3 fftw_wisdom
...
)
</code></pre>

<p>Copy that answer string and stick it in <code>/etc/fftw/wisdom</code>. Test it by running <code>fftw-wisdom</code> from the command line. If you do transforms that aren't powers of 2, or are 2-dimensional, etc., the idea is the same. In the future, Octave will read and add to the wisdom already there, so you can build on it over time. If anyone knows a way to automatically save wisdom on exit from Octave (really, a way to automatically do arbitrary code on exit—the code to save the wisdom is simple enough), that would be a neat trick that I'd love to have.</p>

<p>Oh, and if anyone wants to write a patch for Octave to get it to use a real-to-complex transform when applicable that would be approximately a factor of 2 speedup. I might dive in someday, if the need arises.</p>
