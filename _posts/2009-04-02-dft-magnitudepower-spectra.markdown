---
layout: post
status: publish
published: true
title: DFT Magnitude/Power Spectra
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1129
wordpress_url: http://hans.fugal.net/blog/?p=1129
date: 2009-04-02 18:52:08.000000000 -07:00
tags:
- cs
- dsp
- octave
- matlab
- power
- fft
- dft
- abs
- magnitude
- spectrum
- spectra
comments:
- id: 1943
  author: Ely
  author_email: ''
  author_url: ''
  date: '2009-04-16 13:33:16 -0700'
  date_gmt: '2009-04-16 13:33:16 -0700'
  content: "In the last bit\r\nplot(20*log10(abs(fft(x))))\r\nplot(20*log10(abs(fft(x)).^2))\r\nI
    believe these are wrong. The first one will give the the Power in dB.\r\nSecond
    one is squared twice.\r\n\r\nSee the 20 log rule in the following.\r\nhttp://en.wikipedia.org/wiki/Decibel"
- id: 1944
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-16 14:26:56 -0700'
  date_gmt: '2009-04-16 14:26:56 -0700'
  content: "That's a good point, Ely. So you're saying that the standard 20*log10
    of the magnitude gives you dB power anyway - is that right? So then I should be
    comparing 10*log10(X) to 10*log10(X.^2)? Of course that's just a linear difference
    from what I had before.\r\n\r\nIf we compare 20*log10(X) to 10*log10(X.^2) then
    of course they're the same - they're the same mathematically."
- id: 2156
  author: Josef
  author_email: ykchalacheh@gmail.com
  author_url: ''
  date: '2009-12-16 10:53:28 -0800'
  date_gmt: '2009-12-16 10:53:28 -0800'
  content: "my  friend\r\n\r\ni have signals stored in text file (each file contains
    2 signals represents the left and right hands)\r\n\r\nwhich method is better for
    me to calculate and plot the PSD for each one?\r\n\r\nyour comments is highly
    appreciated\r\nbest wishes,\r\nJosef"
---
I often get confused about the scaling of magnitude and power spectra. I think I've worked it out so I'm puttin it here for my own benefit, and maybe the benefit of someone on the internet. If I'm wrong, <em>please</em> tell me.

Let's take a unit-amplitude sinusoid at 100 Hz, and do a Fourier transform. If we look at the amplitude we'd get two components at 100 Hz and -100 Hz, each with amplitude 1/2.  Something like <a href="http://ccrma-www.stanford.edu/~jos/mdft/Sinusoid_Magnitude_Spectra.html">this</a>.

Now, if we do the same with a DFT we will get basically the same thing, except we'll see the effects of discretization of course. But depending on which variation of the DFT you're using, the magnitude of the components will be either about 1/2 or about N/2. The difference is, of course, the 1/N factor that you included or left out. In the case of the <code>fft</code> function in Octave (and I assume MATLAB), it's without the 1/N factor.
<code>max(abs(fft(x,1024)))
ans =  443.23</code>

The power spectrum is the magnitude spectrum squared. <code>abs(fft(x)).^2</code> or <code>(abs(fft(x))/N).^2</code>. Why would you want to square it? Well there are of course many reasons but the nature of audio signals makes most of the ones I know about moot. Furthermore the relative shape of the power spectrum and the magnitude spectrum is the same.

Try this. Take an audio signal (something more interesting than a single sinusoid) and plot the magnitude spectrum in dB, then plot the power spectrum also in dB, e.g.
<code>plot(20*log10(abs(fft(x))))
figure
plot(20*log10(abs(fft(x)).^2))
</code>
They have a different scale, but they have the same shape. If you were doing something like peak-picking, it wouldn't matter which you used if you're working in dB.

