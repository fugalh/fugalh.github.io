---
layout: post
status: publish
published: true
title: 'Extra, Extra: Nearly All Computation is Broken'
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 355
wordpress_url: urn:uuid:236b0974-545d-4e22-bf5e-622a3d9c32ce
date: 2006-06-07 09:02:00.000000000 -07:00
tags:
- cs
- overflow
comments:
- id: 1474
  author: Levi Pearson
  author_email: levi@cold.org
  author_url: http://lifeoflevi.com/blog/
  date: '2006-06-07 11:13:34 -0700'
  date_gmt: ''
  content: |-
    <p>I guess this depends on how you define 'broken'.  Certainly there was a bug in the example he gave, since he expected the sort to work on very large lists and it did not.  Similar latent bugs probably exist in a lot of places that have not yet scaled to overflow sizes.</p>

    <p>There are a couple of ways to deal with this; first would be to do as he did and change the implementation so that the arithmetic doesn't overflow until much larger numbers, or second, to use a language that can automatically convert to a more abstract implementation of arithmetic when an overflow occurs.</p>

    <p>The second approach is common in the Lisp world, where a bit of performance is traded for correctness.  It has the advantage of being able to scale far beyond the first approach, but the disadvantage of a 'hidden' border beyond which performance changes significantly.</p>
- id: 1475
  author: Hans Fugal
  author_email: ''
  author_url: ''
  date: '2006-06-07 11:19:20 -0700'
  date_gmt: ''
  content: |-
    <p>Yes it does depend on what you mean by 'broken', which was my main thrust. I assert that it's more correct that his expectations were broken than the code. If it was explicit that his code should work for well-defined boundaries that could cause overflow, then yes that's a bug. But he can't claim everyone else's mergesorts that didn't have this requirement are broken.</p>

    <p>Ruby also automatically converts to bigger number types as needed which is really nice most of the time. C-ish languages of course don't do this, at least not fully. C does cast up for multiplication or shifting, for example, but not for addition.</p>
---
<p>This monster keeps popping up and my rant switch has been flipped.</p>

<p>Google Research Blog has a post about how "nearly all binary searches and
mergesorts are broken" because this can overflow:</p>

<pre><code>int mid = (low + high) / 2;
</code></pre>

<p>Boy, have I got news for you. Computers are finite. If you put big enough
numbers in, you will have overflow problems, period. Binary search and
mergesort are no more broken than <code>a+b</code> or <code>x*y</code> or any other arithmetic
operation in every program you have ever written. </p>

<p>All we have here is the need to recognize the limits of your computation. If
you need to support big numbers, you can then deal with overflow. That might
mean using 64-bit integers, or if you have just a little bit of overflow you
can use some creative arithmetic and/or casting. The fun is endless, take it
from a DSP programmer (overflow is an omnipresent concern in DSP programming).</p>

<p>So no, everybody's binary search and merge sort implementations are <em>not</em>
broken. The algorithm is certainly not broken; theoretical discussion on
algorithms is purposefully distanced from implementation concerns like how many
bits you're working with, unless that happens to be the theoretical focus. So
the textbooks and pseudocode are also not broken. The only thing that's broken
is that some of us have forgotten that computers have limits, and we're
surprised when all of a sudden the computer does what it was designed to do when
the limits are reached.</p>
