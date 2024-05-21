---
layout: post
status: publish
published: true
title: Calipers and Science
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1275
wordpress_url: http://hans.fugal.net/blog/?p=1275
date: '2012-04-28 20:56:04.000000000 -07:00'
tags:
- bmi
- fat
- measurement
- body
- data
- science
- jackson
- pollock.skinfold
- caliper
- accumeasure
- measure
comments: []
---
Just for kicks I dug up the original Jackson/Pollock paper for skinfold measurements for determining body fat percentage. Turns out there's also a 7-point equation that also takes circumference of waist and forearm into account.

Here's a snapshot of the equations for men from the paper ("Generalized equations for predicting body density of men" by A.S. Jackson and M.L. Pollock, 1978. I couldn't find the PDF for the women paper online).
<img src="http://hans.fugal.net/jp7.png" alt="Generalized body density equations" width='100%'/>

Important notes: skinfolds are in millimeters, circumferences are in meters, and log is the natural log (ln in most computer languages). I plugged my values from two weeks back into a spreadsheet and got the following results:

<table>
<tr><th>JP Equation</th><th>Density</th><th>%BF</th></tr>
<tr><th colspan=3>Sum of seven skinfolds</th></tr>
<tr><td>S, S^2, age	 </td><td>1.0518</td><td>20.62%</td></tr>
<tr><td>S, S^2, age,C	 </td><td>1.0476</td><td>22.51%</td></tr>
<tr><td>log S, age	 </td><td>1.0506</td><td>21.15%</td></tr>
<tr><td>log S, age, C	 </td><td>1.0482</td><td>22.25%</td></tr>
<tr><th colspan=3>Sum of three skinfolds</th></tr>
<tr><td>S, S^2, age (5)	 </td><td>1.0607</td><td>16.69%</td></tr>
<tr><td>S, S^2, age,C (6)	 </td><td>1.0549</td><td>19.24%</td></tr>
<tr><td>log S, age (7)	 </td><td>1.0578</td><td>17.95%</td></tr>
<tr><td>log S, age, C (8)</td><td>1.0574</td><td>18.14%</td></tr>
</table>

The most interesting thing here is that there's a large difference between 7 and 3 site measurements, and the 3 site range is significantly larger. Also very interesting to note is that the <a href="http://www.accumeasurefitness.com/charts.html">one-site (suprailiac) AccuMeasure chart</a> is, for me, in line with the 7-site measurement (22.1%). Given other measurements I've taken and just general guesswork based on what I see in the mirror, I think that is a decent estimate.

It's also curious that there are two sets of equations given, one using logs and one using squares. 

Moral of the story: more data is better, sometimes not-enough more data is worse than a simpler estimate, and interesting things can be learned when you go to the original source. (This is just a quick note, but the paper is very interesting and reading it will be an interesting exercise that sets proper expectations for, and understanding of, the JP7 skinfold method).
