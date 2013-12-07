---
layout: post
status: publish
published: true
title: Convergent Rounding
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 109
wordpress_url: urn:uuid:0affdba0-1541-4f3c-8f86-01c9d1a7eecc
date: 2006-04-06 20:37:00.000000000 -07:00
tags:
- audio
- cs
- round
- convergent
- dsp
- fixed-point
comments: []
---
<p>The rounding they taught you in elementary school has an eventual bias. i.e.
over time you find that you've rounded up more often than you've rounded down.
Bias is a bad thing, especially in DSP and other numerically-intensive computing. </p>

<p>Convergent rounding is one good way to eliminate this bias. It works the same
as regular rounding except that instead of rounding 0.5 up, you round 0.5 to
the nearest even number. So 1.5 goes to 2.0, 2.5 goes to 2.0, etc.</p>

<p>A quick tutorial on short fixed-point programming in C. The decimal point is
between bits 15 and 14, and bit 15 is your sign bit. So, you have a range of
1-2^-15 to -1. So 0.5 is 0x4000, and -0.5 is 0xC000 (two's complement). Now,
when you multiply two numbers together you get twice as many bits of precision,
so multiplying two shorts gives you an int, and in that int the decimal point
is between bits 30 and 29, and bits 30 and 31 are sign bits. We want to round
at bit 15 so we can fit the result back into a short. Clear as mud?</p>

<p>The point of this post is to get this C code out there, because as simple as it
seems it was a devil to debug:</p>

<pre><code>int cround(int a)
{
    if (a &amp; 0x3fff)
        a += 0x4000;              // normal rounding
    else
        a += (a&gt;&gt;1) &amp; 0x4000;     // convergent rounding

    return a &amp; 0xffff8000;
}
</code></pre>

<p>If you don't see why this works (I didn't when I first read the "add half of
the lsb uf the upper part" algorithm), then fill out this truth table as an
excercise:</p>

<pre><code>0.00
0.01
0.10
0.11
1.00
1.01
1.10
1.11
</code></pre>

<p>Here's an example of the function in use:</p>

<pre><code>short x,y;
int a;
x = 0x7ffd;     // x = almost 1
y = 0x4000;     // y = 1/2
a = x*y;        // a = 0x1fff4000
a = cround(a);  // a = 0x1fff0000
x = a&gt;&gt;15;      // x = 0x3ffe
</code></pre>
