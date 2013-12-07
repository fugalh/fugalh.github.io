---
layout: post
status: publish
published: true
title: Sourdough Calculations
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 731
wordpress_url: urn:uuid:1ddb80a9-9bbd-42a6-8bf9-a7e799a3bcf8
date: 2006-10-08 15:50:00.000000000 -07:00
tags:
- sourdough
- calculator
comments:
- id: 1513
  author: Jacob Fugal
  author_email: ''
  author_url: ''
  date: '2006-10-08 22:00:32 -0700'
  date_gmt: ''
  content: |-
    <p>Re: salt percentage</p>

    <p>Does the 0.2% really make that much of a difference in the saltiness of the bread? I just wonder, because if you use 2% instead of 1.8% you can use a simple rule of thumb:</p>

    <p>salt = flour * 0.02/6 tsp
         = (flour/100) * (1/3 tsp)</p>

    <p>=> 1/3 tsp per 100g flour</p>

    <p>So for a 500g dough with 66% hydration you have exactly 1 tsp salt. :)</p>
- id: 1514
  author: Hans
  author_email: ''
  author_url: ''
  date: '2006-10-08 22:10:05 -0700'
  date_gmt: ''
  content: |-
    <p>Excellent observation. No, I don't think the 0.2% makes a difference. At 300g flour the difference is 0.6g, which is 0.1tsp, which is within the limits of probable measurement error.</p>

    <p>The real question is how does 1tsp salt differ from 1tsp kosher salt. I think I'm going to have to measure and weigh and find out. (I'll see then if my salt is really 6 g per tsp.)</p>
---
<p>So as not to leave anyone hanging from my last post, here's what I do from
beginning to end with regards to calculations when baking sourdough bread.</p>

<p>First, I decide on quantity. I bake a loaf of whole wheat sandwich bread every
week or so (sometimes sourdough, sometimes no), and 800g is a good dough weight
for that. For a sourdough boule, I aim between 300g and 500g. For experiments
and baguettes, 250g or less. For big boules or loaves to fit the more normal
size loaf pan, to take to functions for example, I aim at 1kg. The beauty of it
all is that I can make whatever amount of bread fits my needs, with a few minor
calculations.</p>

<p>Now that we have the dough weight, we need to break it down into the various
ingredients. Most ingredients in baking are relative to the flour used, so
flour is the first calculation. I divide the total weight by one plus the
hydration baker's percentage, i.e. if I want a 66% hydration dough I do <code>flour
= dough / 1.66</code>. </p>

<p>Next we need the amount of water. <code>water = flour * hydration</code>. For our 66%
hydration bread that's <code>water = flour * 0.66</code>. 66% hydration is a really nice
number because not only does it make good bread, it has a good margin of
tolerance for measuring mistakes (you can go a little drier or wetter with no
worry), and it is easy to do in your head. That's right, 66% is two thirds.
300g flour and 200g water makes 500g dough and it's easy to remember/calculate
even without a calculator. </p>

<p>All that's left is the salt and leavening. Salt is about 2% of the flour. I
read 1.8% somewhere and it stuck so that's what I use, though I know my
measuring is nowhere near that accurate for the amount of dough I make. So
<code>300g * 0.018 = 5.4g</code>. Alas my scale measures 5g increments which is mostly
useless for measuring salt, so I asked units what to do:</p>

<pre><code>You have: 1 g
You want: tsp salt
        * 0.16666667
        / 6
</code></pre>

<p>Oh, well that's easy to remember, just divide the salt weight by 6. So <code>salt =
flour * 0.018/6</code> teaspoons. </p>

<p>With yeast you just guess. Take a similarly sized recipe and use that much.
Bread recipes all vary so much here anyway, and the different kinds of yeast do
too. Just remember, more yeast means faster rise and less desirable flavor.
Less yeast means slower rise and better flavor. </p>

<p>If you're doing sourdough, I hope you haven't mixed the flour and water yet
because there's going to be some adjustment. Decide how much start you want in
proportion to your dough. 10% or 20% is easy to do in your head. Now do the
same thing with flour and water as above, for your total start amount. Or, be
lazy and use 100% hydration start and divide by two (by weight). e.g. for our
500g loaf with 20% inoculation we want 100g start, so that's 50g flour and 50g
water (plus a little start from the fridge, about 10g will stick to the side of
your container anyway). Subtract the resulting flour and water amounts from the
calculated flour and water above (or do the start calculations first).</p>

<p>If you want to add honey, sugar, oil, butter, seeds, whatever else, just follow
what a similar-sized recipe calls for or eyeball it. Really the only things to
fret here are the flour/water ratio and the flour/salt ratio.</p>

<p>All that probably seems a little overwhelming, which is why my <a href="http://hans.fugal.net/src/sourdough">sourdough
script</a> and <a href="http://hans.fugal.net/sourdough/calculator.html">sourdough calculator webpage</a> exist. But if you're lazy/cheap and
can memorize a few unchanging equations (but can't memorize a recipe for 5
minutes to save your life), that's how you do it.</p>
