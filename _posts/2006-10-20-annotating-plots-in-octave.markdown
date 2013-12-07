---
layout: post
status: publish
published: true
title: Annotating Plots in Octave
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 739
wordpress_url: urn:uuid:e39540dd-3230-4738-ae4c-a7785e8aacff
date: 2006-10-20 15:46:00.000000000 -07:00
tags:
- osx
- octave
- matlab
- figure
- plot
comments: []
---
<p>In MATLAB, you can do this:</p>

<pre><code>x = 2*pi*[0:100]/100;
figure(1); plot(sin(x));
figure(2); plot(cos(x));
% ...
figure(1); title('sin(x)');
figure(2); title('cos(x)');
</code></pre>

<p>In Octave on OS X, I was having trouble. There were two problems. First, the version of Octave I had (2.1.73) had a bug where it would not just add the title "sin(x)", but replot the current plot (the cosine) and give it the title "sin(x)". Not what I wanted. I upgraded to 2.9.9 and it now works properly provided you solve the other problem.</p>

<p>The other problem is more a misdocumentation. The docs for <code>figure.m</code> read: </p>

<blockquote>
    <p>Set the current plot window to plot window N.  This function
    currently requires X11 and a version of gnuplot that supports
    multiple frames.  If N is not specified, the next available window
    number is chosen.</p>

    <p>figure is the user-defined function from the file
    <code>/usr/local/share/octave/2.9.9/m/plot/figure.m</code></p>
</blockquote>

<p>But if you look at the source it's obvious that it works with AquaTerm as well,
but only if the environment <code>GNUTERM</code> is set to <code>aqua</code>. So put this in your
<code>~/.bashrc</code>:</p>

<pre><code>export GNUTERM=aqua
</code></pre>

<p>On Linux, running a version of Octave without the bug mentioned above would be
sufficient, as you're obviously running X11. I have gnuplot version 4.0.</p>
