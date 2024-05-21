---
layout: post
status: publish
published: true
title: On Calculators
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 730
wordpress_url: urn:uuid:7b0d3cec-44c4-40b4-a22e-1b30c6a6b069
date: '2006-10-08 15:15:00.000000000 -07:00'
tags:
- calculator
- rpn
comments:
- id: 2363
  author: vontrapp
  author_email: von@fugal.net
  author_url: http://von.fugal.net/blog
  date: '2011-02-06 17:01:19 -0800'
  date_gmt: '2011-02-06 17:01:19 -0800'
  content: Do you not like orpie?
---
<p>I have the {sourdough,} bread formulas that I use memorized now, so I rarely use my little script anymore, instead opting for a calculator and my logbook. As a result I've been taking my precious HP 48GX (or sometimes even my laptop) into the kitchen, which always makes me uneasy, especially since the 48GX is nigh unto irreplaceable.  So I bought a calculator yesterday.</p>

<p>I had no delusions that there would be a $5-$15 <acronym title="Reverse Polish Notation">RPN</acronym> calculator, so I picked up the most fitting $10 calculator from Target, which happens to be a TI-30XA. It's a little scientific calculator with way more features than I expected to find for $10. HP makes a model in this range too, the 9s I think. I honestly don't know if it was even on the rack at target. The TI-30XA was closer to my eye level and maybe a dollar or two cheaper, if there were any comparable HPs. </p>

<p>My point is this: cheap calculators is a cutthroat commodity business. There may not be a big market for RPN, not enough to justify an RPN model perhaps, but if someone out there made a $10 calculator that was RPN, even if it was only 4-function or reduced functionality scientific, that would differentiate that calculator in a measurable way. No, it's not going to corner the calculator market, but it couldn't hurt, could it? I'm a programmer, and I've written toy calculator programs in various languages including assembly. It's a <em>lot</em> easier to add RPN functionality than this algebraic entry stuff or plethora of fancy trigonometry and biology (I kid you not) features. I have a dream that someday some company will get their act together and offer a calculator similar to the TI-30XA that is RPN (or can do RPN). If that someone happens to be wandering by this blog, consider yourself spurred on.</p>

<p>Speaking or RPN, if you like RPN and weren't aware of the <code>dc</code> calculator
available in most UNIX environments, consider yourself enlightened. Although
honestly I use <code>bc</code> more than <code>dc</code> because <code>dc</code>'s interface is a bit arcane.
Like not printing the top of the stack automatically, and that you have to use
<code>_</code> for negative numbers instead of <code>-</code>. <code>bc</code> is not RPN, but that's less
annoying (but still annoying) when you have a full keyboard and screen, and
readline support. I've occasionally seen other RPN calculators both in terminal
and GUI. As far as GUI goes, as you may have read here before I'm partial to
Apple's Calculator included in OS X. Its only flaw is not being able to see
more of the stack at a time. I've not yet come across a terminal one to replace
<code>bc</code>, which is what I'd prefer. Let me know if you've come across one. Someday
I may hack one up. If I do I'll include unit conversions (with
<a href="http://www.gnu.org/software/units/units.html"><code>units</code></a> in the background) and
math functions with the same names as the C math library.</p>
