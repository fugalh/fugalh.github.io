---
layout: post
status: publish
published: true
title: Y Tick Labels in Octave
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1065
wordpress_url: http://hans.fugal.net/blog/?p=1065
date: 2009-01-21 21:59:37.000000000 -08:00
tags:
- audio
- cs
- octave
- matlab
- graph
- frequency
- log-frequency
- log
- logfsgram
- ytick
- yticklabel
- gca
- spectrogram
comments:
- id: 2166
  author: V. A.
  author_email: x.user1372@gmail.com
  author_url: ''
  date: '2010-02-05 20:14:28 -0800'
  date_gmt: '2010-02-05 20:14:28 -0800'
  content: Nice. This works perfectly. Thanks!
- id: 2672
  author: audiodane
  author_email: dane_walther@hotmail.com
  author_url: ''
  date: '2012-07-02 18:12:22 -0700'
  date_gmt: '2012-07-02 18:12:22 -0700'
  content: FANTASTIC. Thank you so much for posting this.
---
I struggled with this on and off for a couple of months. Finally I stumbled on the magic needed to get it working.

Dan Ellis has <a href="http://labrosa.ee.columbia.edu/matlab/sgram/">some MATLAB code</a> for log-frequency spectrograms, but in Octave the graph lacks the custom y tick marks. Here's the original code:

<pre><code>    yt = get(gca,'YTick');
    for i = 1:length(yt)
        ytl{i} = sprintf('%.0f',logffrqs(yt(i)));
    end
    set(gca,'YTickLabel',ytl);</code></pre>

This code gets the existing tick marks and labels them with the log frequency (instead of the frequency bin).
The problem is that Octave doesn't populate <code>YTick</code> <em>unless</em> it was manually set already.

Here's the working code:

<pre><code>    % octave doesn't populate YTick with its tick marks, so we have to set
    % our own. Besides, this way we get nice octave intervals.
    set(gca,'YTick',1:12:M);
    yt = get(gca,'YTick');
    for i = 1:length(yt)
        ytl{i} = sprintf('%.0f',logffrqs(yt(i)));
    end
    set(gca,'YTickLabel',ytl);</code></pre>
