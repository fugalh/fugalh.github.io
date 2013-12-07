---
layout: post
status: publish
published: true
title: Duck Typing Defended
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 664
wordpress_url: urn:uuid:39ee7b00-5c6d-40cd-8f28-f0d3f7ab15c0
date: 2006-07-08 18:21:00.000000000 -07:00
tags:
- cs
- ruby
- C
- python
- java
- static
- dynamic
comments:
- id: 1488
  author: Bruce Eckel
  author_email: ''
  author_url: ''
  date: '2006-07-13 06:47:25 -0700'
  date_gmt: ''
  content: |-
    <p>Ah, but you <em>can</em> do duck typing with C++. Read this:
    <a href="http://mindview.net/WebLog/log-0052" rel="nofollow">http://mindview.net/WebLog/log-0052</a></p>
- id: 1489
  author: star_at_sky_2010@yahoo.com
  author_email: ''
  author_url: ''
  date: '2006-12-22 15:55:04 -0800'
  date_gmt: ''
  content: |-
    <p>hi all </p>

    <p>i wanna  help from you </p>

    <p>i have to do assingment on c++ that the out but can be like duck drawing </p>

    <p>i really i dunt know who to star doing like that ....</p>

    <p>i wish can find help from all of you </p>

    <p>with my best regards </p>
---
<p>Ever since I discovered ruby I've loved dynamic typing. I never paid much heed
to people who got their knickers in a knot over how dynamic typing is "unsafe". </p>

<p>While working on <a href="http://ardour.org/">Ardour</a> <a href="http://ardour.org/node/237">this
summer</a>, I've literally been wrestling with C++,
all because it is statically typed. The code I've been writing over the past
month could have been done in one week with half my brain tied behind my back
(which is the usual situation, by the way), if only C++ were dynamically typed.</p>

<p>In other ways static typing hasn't exactly got in my way, it just causes me to
jump through hoops that seem silly, unnecessary, and inelegant. A simple
concrete example will help. I'm doing undo serialization, and of course Ardour
already serializes other things in order to save sessions. In C++ this means
lots and lots of otherwise unrelated things all inherit from a common
serializable base class. This is why multiple inheritance is necessary in C++.
In Java you can use interfaces, which is better than multiple inheritance but
not by much. In dynamic languages, you don't even have to give it a second
thought. You just make sure everything that needs to be serialized responds to
a serialize method, et voil&aacute;!</p>

<p>So as I've been wrestling I've had this nagging feeling that it's *me* that's
broken, not C++. Have I become so spoiled by dynamic languages that I can't
program efficiently in a static language anymore? Are the static people right
and one day my whole world will come crashing in and all my ducks will keel
over? Feelings of self doubt are part of being human, and these were some of
mine this summer. Then I read a blog post by Bruce Eckel on <a href="http://www.mindview.net/WebLog/log-0025">Strong Typing vs.
Strong Testing</a> and my mind was put at
ease. The thrust is, dynamic typing is good, and testing is necessary. I think
this quote about Robert Martin (a C++ guru) sums things up nicely:</p>

<blockquote>
    <p>Robert came to more or less the same conclusion I have, but he did so by
    becoming "test infected" first, then realizing that the compiler was just one
    (incomplete) form of testing, then understanding that a weakly-typed language
    could be much more productive but create programs that are just as robust as
    those written in strongly-typed languages, by providing adequate testing.</p>
</blockquote>

<p>I have a thought along these lines. Let's say you've got duck typing in full
swing as in his examples. Now in the real world it sometimes happens that you
choose a common ambiguous word for the duck method, like "run" perhaps, but
more often than not you have methods that are named fairly specifically, like
"speak" or "jump". The static argument is that you might accidentally call the
method on something that won't do what you anticipate because it's not of the
right type. But really now, how many of your objects that implement "jump" are
going to be the wrong kind of objects in your application? Often the answer is
none. So you jump through hoops for no reason.</p>

<p>Do read the article, it's fun and well-written. Even if you come out still
clinging to your beliefs that static typing is Good and Wholesome, at least
you'll see that us dynamic people aren't necessarily lazy, stupid heathens.</p>
