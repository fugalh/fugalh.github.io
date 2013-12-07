---
layout: post
status: publish
published: true
title: Body Density Measurement Uncertainty
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 867
wordpress_url: urn:uuid:8c24664e-f2da-4348-9f8c-591352f1a140
date: 2007-08-22 20:06:00.000000000 -07:00
tags:
- life
- weight
- bmi
- density
- health
- fat
comments:
- id: 1607
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-08-22 20:35:05 -0700'
  date_gmt: ''
  content: |-
    <p>It occurs to me to provide a version of the equation for rednecks (those of you still using nonmetric units): </p>

    <p>ρ = 1.9172228 m<sub>b</sub>/(m/ρ<sub>w</sub> - v<sub>a</sub> - v<sub>r</sub> - v<sub>c</sub>)</p>

    <p>Where ρ<sub>w</sub> = 0.520 lbs/cup and all masses are in lbs and all volumes are in cups. The result is still in kg/l.</p>
---
<p>A couple days back I posted <a href="http://hans.fugal.net/blog/articles/2007/08/20/measure-your-body-density">my idea for measuring body density and estimating
body
fat</a>.
Dad, who has a set of skinfold calipers gave it a try and gave me comparative
results, and asked the question on everbody's mind: just how accurate is it,
especially with that pretty blatant guess at residual lung volume?</p>

<p>So I took some time to learn how to account for uncertainty and take a stab at
pinning a confidence interval on the technique. First of all, I didn't realize
how complicated uncertainty propogation is. Partial derivatives, squares and
square roots, etc. Luckily, I came across some lecture or presentation notes
detailing a sequential perturbation method (instead of an analytical method). I
could have talked Jacob into walking me through the partial derivatives, but
this method is easy to code and a find in and of itself. Read about it in <a href="http://web.cecs.pdx.edu/~gerry/class/ME449/lectures/pdf/uncertaintySlides_2up.pdf">this
PDF</a>.</p>

<p>I coded up the formula and ran some test data through it. Here's the equation
again for review: ρ = m / ((m + m<sub>c</sub>)/ρ<sub>w</sub> - (v<sub>a</sub> +
v<sub>c</sub> + v<sub>r</sub>)) Here's the values and uncertainty I attribute
to each variable: </p>

<ul>
<li>m = 121.29 ±0.02 kg</li>
<li>ρ<sub>w</sub> = 0.997 ±0.001 kg/l</li>
<li>v<sub>a</sub> = 1.13 ±ٍ0.01 l</li>
<li>v<sub>r</sub> = 1.87 ±0.5 l</li>
<li>m<sub>c</sub> = 0 ±0.02 kg</li>
<li>v<sub>c</sub> = 0 ±0.01 l</li>
</ul>

<p>I didn't actually use a counterbalance, but I included the uncertainty in
measuring its mass and volume as if I had, just for completeness. As suspected,
v<sub>r</sub> has the largest uncertainty. I calculated the uncertainty if
v<sub>r</sub> were magically accurate, and found that the uncertainty was
0.0014 kg/l. This translates to about 0.65% body fat with Siri's equation
(ignoring the uncertainty inherent in that equation, which is a constant bias
accross measurements for one person on any given day). </p>

<p>Note that I give ρ<sub>w</sub> this time, instead of whisking it away with a
magical 1 kg/l. I picked an average value between 72°F and 84°F (most pools are
in this range), with an uncertainty (due to water temperature) of about 0.001
kg/l. If you use 1 kg/l instead you are introducing a bias of about 0.9% body
fat. So I was wrong about that being insignificant.</p>

<p><s>Now, I found <a href="http://www-rohan.sdsu.edu/~ens304l/uww.htm">a better estimate</a>
(why better? because it seems to come from a more reputable source than
Wikipedia) for residual lung volume: v<sub>r</sub> = RV = 0.24 VC. So I may
have overestimated my RV last time by ½ liter.</s>
(<em>Update</em>: I think that must be a typo on that page, they probably mean 24% or 28% of <em>total</em> capacity instead. This fits in much better with the rest of the literature that I have found, e.g. <a href="http://www.erj.ersjournals.com/cgi/reprint/8/3/492">Quanjer</a> and <a href="http://www.chestjournal.org/cgi/content/abstract/102/4/1209">Paoletti</a>.) That seems like a generous
uncertainty measure for RV, too. With that uncertainty factored in, we get an
uncertainty of about 2.1% body fat, or about 5% is you are on the slight side of average (the less you weigh, the more difference that 1/2 liter makes).</p>

<p>So, Dad, let's bump your score up by about 1% for the density of water and then
tack an uncertainty of 2% onto it, you have a body fat of 26.3% ±2%. I'm no
expert on using calipers, but <a href="http://bjsm.bmj.com/cgi/content/abstract/40/3/208">one paper's
abstract</a> indicates that the
skinfold method uncertainty is about 3%. I've seen 10% tossed around casually
too, but have no reliable source to back that up. That puts the two methods
within the appropriate reach of eachother, which is heartening. It's
interesting to note that BMI is overestimating Dad's fat, because he's more
lean than the average couch potato. Imagine the difference if the subject were
someone completely nuts, like a young triathlete, who has body fat of about
15%. Even better, if you are such a nut you could do the experiment and post
your results (and BMI) here as a comment for us to see.</p>
