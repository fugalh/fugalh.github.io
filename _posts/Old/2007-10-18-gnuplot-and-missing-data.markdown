---
layout: post
status: publish
published: true
title: Gnuplot and Missing Data
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 881
wordpress_url: urn:uuid:87acc013-788b-42ba-bf49-d00f06786976
date: '2007-10-18 08:41:13.000000000 -07:00'
tags:
- gnuplot
comments:
- id: 1624
  author: Philipp K Janert
  author_email: janert@mailaps.org
  author_url: http://principal-value.com
  date: '2008-03-19 21:26:56 -0700'
  date_gmt: ''
  content: |-
    <p>I see that you are a Gnuplot user, so I thought you might be interested to know that there is now a book on it: "Gnuplot in Action". You can pre-order it directly from the publisher: <a href="http://www.manning.com/janert/" rel="nofollow">Manning: Gnuplot in Action</a>.</p>

    <p>If you want to learn more about the book and the author, check out my book page at <a href="http://principal-value.com/my-book.php" rel="nofollow">Principal Value - Gnuplot in Action</a>. </p>

    <p>Let me know if you are interested in a review copy.</p>
---
<p>Let's say you have some data you want to plot with <a href="http://gnuplot.info/">gnuplot</a>:</p>

<pre><code>2007-08-16 119.02264
2007-08-17 120.20198
2007-08-18 121.29
2007-08-19 120.65557
2007-08-20 119.92982
</code></pre>

<p>Further suppose you'd like to plot both the weight (those are kilograms) and the BMI (weight/height<sup>2</sup> in kg/m<sup>2</sup>). One way to do that is this gnuplot snippet:</p>

<pre><code>set xdata time
set timefmt '%Y-%m-%d'
set datafile missing "?"
plot 'data' using 1:2 title 'Weight' with lines,\
     'data' using 1:($2/3.7249) title 'BMI' with lines
</code></pre>

<p>So far so good. Now, what if you have a missing data point? Well, in this contrived example you would leave that line out and all would be well. But let's say you have other columns with data that may not be missing, so you can have a missing data point:</p>

<pre><code>2007-08-16 119.02264
2007-08-17 120.20198
2007-08-18 ?
2007-08-19 120.65557
2007-08-20 119.92982
</code></pre>

<p>If you use the same snippet above to plot this data, you get an interesting result. The first plot (weight) is just what you'd expect. It just skips that missing data point, connecting the data from 8/17 and 8/19. But the second plot (BMI) instead leaves a gap between 8/17 and 8/19. This oddly inconsistent behavior is unexpected to mere mortals, but not to gnuplot developers. I quote from <code>help missing</code>:</p>

<blockquote>
<pre><code>   set datafile missing "?"
   set style data lines
   plot '-'
      1 10
      2 20
      3 ?
      4 40
      5 50
      e
   plot '-' using 1:2
      1 10
      2 20
      3 ?
      4 40
      5 50
      e
   plot '-' using 1:($2)
      1 10
      2 20
      3 ?
      4 40
      5 50
      e
</code></pre>

    <p>The first <code>plot</code> will recognize only the first datum in the "3 ?" line.  It
    will use the single-datum-on-a-line convention that the line number is "x"
    and the datum is "y", so the point will be plotted (in this case erroneously)
    at (2,3).</p>

    <p>The second <code>plot</code> will correctly ignore the middle line.  The plotted line
    will connect the points at (2,20) and (4,40).</p>

    <p>The third <code>plot</code> will also correctly ignore the middle line, but the plotted
    line will not connect the points at (2,20) and (4,40).</p>
</blockquote>
