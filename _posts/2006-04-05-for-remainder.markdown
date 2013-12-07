---
layout: post
status: publish
published: true
title: '% for Remainder'
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 108
wordpress_url: urn:uuid:80b4605e-ce0e-4bd3-9d6c-69bdb7fe4032
date: '2006-04-05 13:56:47.000000000 -07:00'
tags:
- cs
- ruby
- C
- mod
- modulus
- modulo
- modular
- math
- arithmetic
- negative
comments:
- id: 1451
  author: Jacob
  author_email: lukfugl@gmail.com
  author_url: http://jacob.fugal.net/blog/
  date: '2006-04-09 21:31:44 -0700'
  date_gmt: ''
  content: |-
    <p>Boo and shame on C. I assume it's this way in C++ as well?</p>

    <p>What really gets me is the misnomers on the 'fmod' and 'remainder' functions. The behavior of 'fmod' is equivalent to the % operator, while 'remainder' does what you (and I) expected of the % operator (cf. the "coherent post").</p>

    <p>Having that inane behavior for the % operator can be forgiven by claiming it is the "remainder" operator instead of the "modulo" operator, but having 'fmod' -- whose name implies modulo -- follow suite is just wrong. Then backstepping and providing the missing correct behavior through a method named 'remainder'?! That makes it kind of hard to claim that % is the <em>remainder</em> operator.</p>

    <p>Whoever wrote the 1999 standard obviously didn't do their math homework...</p>
- id: 1452
  author: Hans Fugal
  author_email: ''
  author_url: ''
  date: '2006-04-09 21:46:49 -0700'
  date_gmt: ''
  content: <p>It's the same in C++, yes.</p>
- id: 1453
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-10-04 06:25:49 -0700'
  date_gmt: ''
  content: <p>Incidentally, looks like Java follows suit.</p>
---
<p>I had my lunch handed to me today because some C DSP code I had written was
wrong:</p>

<pre><code>/* M is the size of the buffer,
 * w is the base pointer,
 * p is the pointer into the buffer */
void wrap(short M, short *w, short **p)
{
if (*p &lt; w || *p &gt;= (w + M))
    *p = w + (*p - w) % M;
}
</code></pre>

<p>What I did not realize is that the <code>%</code> operator in C does <em>not</em> wrap negative
numbers into the positive range like you would expect if you were a
mathemtician. i.e. <code>-7 % 8 == -7</code> in C, where in mathematics -7 = 1 mod 8.</p>

<p>I can hear you now: "Didn't you test it, you fool?" Well, yes, I tested the
algorithm in Ruby, where mathematics hold true:</p>

<pre><code>rb(main):001:0&gt; -7 % 8
=&gt; 1
</code></pre>

<p>How was I to know the C version was braindead?</p>

<p>So which is right? Well you can probably guess my bias by now. But inquiring
minds want to know, and no other type reads this blog so I did some research.</p>

<p>First, the mathematics. Wolfram has <a href="http://mathworld.wolfram.com/ModularArithmetic.html">a dizzying
explanation</a>. Search for
<a href="http://www.google.com/search?client=safari&amp;rls=en&amp;q=modular+arithmetic&amp;ie=UTF-8&amp;oe=UTF-8">modular
arithmetic</a>
for any number of treatments of the subject. Too lazy for that? Fine, look at
your watch. If it's 10:05 and you go back in time 10 minutes, is it -5 past
10? Arguably so ("5 to"), but most people would agree that it's actually 9:55
by canon.</p>

<p>Now for the C argument. The 1999 ISO C Standard says:</p>

<blockquote>
    <p>If the quotient <code>a/b</code> is representable, the expression <code>(a/b)*b + a%b</code> shall
    equal <code>a</code>.</p>
</blockquote>

<p>So my compiler is fine. It's C that's broken. Before C99 the use of <code>%</code> on
negative numbers was IMPLEMENTATION DEPENDENT, which if you know anything about
C history means they didn't think it through well enough, or they made a
decision based on speed or ease of implementation. The C99 definition was
probably chosen either for ease of implementation or for the most common case.
Not exactly good enough to convince me.</p>

<p>Naturally, there's no going back now, so if you find yourself possibly needing
to do modular arithmetic on negative numbers in C, be sure to add again if
negative:</p>

<pre><code>/* M is the size of the buffer,
 * w is the base pointer,
 * p is the pointer into the buffer */
void wrap(short M, short *w, short **p)
{
if (*p &lt; w || *p &gt;= (w + M))
    *p = w + (*p - w) % M;

if (*p - w &lt; 0)
    *p += M;
}
</code></pre>

<p>Here's <a href="http://gcc.gnu.org/ml/gcc-help/2005-11/msg00141.html">a coherent post</a>
to the gcc-help list about the subject. Now, I don't want to hear anyone saying
that <code>%</code> is the modulus operator from now on. It's the <em>remainder</em> operator.</p>
