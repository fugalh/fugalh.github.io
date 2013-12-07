---
layout: post
status: publish
published: true
title: The Hacker's Diet
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 880
wordpress_url: urn:uuid:c92e7f04-b96b-41b4-927f-c626bf984050
date: 2007-10-16 14:24:38.000000000 -07:00
tags:
- diet
- health
- fat
comments:
- id: 2800
  author: Chris
  author_email: bigonroad@gmail.com
  author_url: http://allaboutchris.org
  date: '2013-07-19 08:31:38 -0700'
  date_gmt: '2013-07-19 08:31:38 -0700'
  content: "A calorie IS a calorie. Recent meta analysis of 10 different diets showed
    that number of calories was the overriding factor in weight loss.\r\n\r\nOne guys
    just did a diet purely on chocolate and lost weight -http://articles.latimes.com/2010/dec/06/health/la-he-fitness-twinkie-diet-20101206"
- id: 2801
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2013-07-19 16:55:15 -0700'
  date_gmt: '2013-07-19 16:55:15 -0700'
  content: "You're quite wrong, but I doubt I'll change your mind here. I certainly
    don't blame you for not believing it from this post, but there is plenty of evidence
    out there if you're willing to read it. Basically, the human body is a complex
    system and unsurprisingly it reacts differently depending on a lot of factors.
    Not only is a calorie not just a calorie, but it's a different calorie depending
    on when you eat it and other factors.\r\n\r\nAnd I don't doubt some guy lost weight
    eating only chocolate. Complex system.\r\n\r\nIncidentally, the Shangri-La thing
    is ridiculous, so thanks a bunch for reminding me I once gave it the time of day.
    :-P"
---
<p>I came across <a href="http://www.stdlib.net/~colmmacc/2005/12/25/losing-weight-with-gnuplot/">this blog post</a> while googling an unrelated gnuplot problem, of all things. The post talks about <a href="http://www.fourmilab.ch/hackdiet/">The Hacker's Diet</a>. Duly intrigued, I whipped out <a href="http://catb.org/jargon/html/Y/yak-shaving.html">my razor</a> and plowed through the book. I like it.</p>

<p>The book is well-written, doesn't take itself too seriously, takes the subject matter seriously, and takes the audience seriously, i.e. you aren't expected to be Superman—the program is very down-to-earth and achievable. It is slightly aged (he mentions at one point that you need a color monitor to really appreciate the color graphs), but this isn't a problem.</p>

<p>The best part about the book (besides being free) is that he takes the problem of weight loss and attacks it as an engineering problem. He comes up with an understanding and a plan and implements it, and loses some 70 pounds. This book definitely appeals to every inner geek. </p>

<p>The worst part about the book is that his solution involves calorie counting. That makes me sick on so many levels, but I'll just rant on two of them. First of all, a calorie is not a calorie. I don't know if this is new knowledge or not, but we see it in all the latest fad diets. Atkins, <acronym title="Glycemic Index">GI</acronym>, etc. are all based on the fact that a calorie is not a calorie. Second, I am <em>not</em> going to spend my life counting calories, thank you very much. I'd rather drink oil.</p>

<p>Speaking of drinking oil, this book has a very interesting parallel to the Shangri-La diet. They both use the thermostat analogy, but Shangri-La aims to adjust your off-kilter internal thermostat and this book aims to replace your broken thermostat with record keeping and conscious decision. Certainly, one could apply both at the same time.</p>

<p>In spite of me not wanting to count calories, I do intend to put a modified version of this plan into practice. Since I don't want to count calories, I am going to have to rely on some other feedback. Since most of us eat a relatively manageable variety of foods, we should be able to get an instinctive feel for "how much" we are consuming on a meal-by-meal and/or day-by-day basis. Indeed, he talks about getting to this point, by accident. I intend to get there much sooner, on purpose. By keeping a food log and comparing it to weight loss/gain over the period of a month or two or three, and studying it in hindsight, I should be able to get a feel for three "thermostat settings": lose weight, maintain weight, gain weight. It may be a bang-bang approach, but there's also the minute automatic adjustments and body's metabolism adjustment working in your favor while trying to stay stable.</p>

<p>I have adjusted my <a href="http://hans.fugal.net/images/mg.svg">weight graph</a> to include a trend plot as described in the book. While I was at it, I added the plot for measured body fat percentage (which I need to start doing more frequently). BMI is a linear relationship with weight, so the kg on the left correspond with the BMI on the right. So, by graphing measured body fat percentage you can see whether I am above/below the BMI for my given weight, plus see that otherwise invisble chasm between losing fat and losing weight. If you'd like to set up your own such graphs, I'm happy to share my code with you. Just drop me a line.</p>
