---
layout: post
status: publish
published: true
title: Functional Floundering
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 953
wordpress_url: urn:uuid:7fcb5ce8-2f68-405f-aeb8-557b50afe716
date: '2008-04-06 17:21:04.000000000 -07:00'
tags:
- cs
- functional
- erlang
- clojure
- lisp
- scheme
- programming
comments:
- id: 1737
  author: Levi
  author_email: levipearson@gmail.com
  author_url: http://lifeoflevi.com/blog/
  date: '2008-04-06 19:07:07 -0700'
  date_gmt: ''
  content: |-
    <p>Well, I still occasionally flounder with functional stuff, but I think what helped me the most when I started was working through the early exercises in The Structure and Interpretation of Computer Programs and Essentials of Programming Languages.  The former is free online, and the latter was your textbook for the undergrad class you mentioned.</p>

    <p>But really, it does come down to practice.  What works best for me is reading good code in the style I want to follow, figuring out why it's written the way it is, and then trying to write my own code.  It's a time-consuming process, so I'm cutting a lot of corners in my current Haskell learning, but it works for me.</p>

    <p>Also, here's an interesting paper called 'A Tutorial on the Universality and Expressiveness of /fold/': <a href="http://www.cs.nott.ac.uk/~gmh/fold.pdf" rel="nofollow">http://www.cs.nott.ac.uk/~gmh/fold.pdf</a></p>

    <p>It was pretty eye-opening for me, as it provided ways to think about how things can be done recursively.</p>
---
<p><a href="http://lifeoflevi.com/blog/">Levi</a> pointed me to a <a href="http://clojure.sourceforge.net/news/concurrency_talk.html">presentation</a> on <a href="http://clojure.sourceforge.net/">Clojure</a>, "a dynamic programming language for the JVM". That's actually a pretty bland description. I'd describe it at least as a dynamic functional concurrency-oriented lispy language for the JVM. The presentation was interesting, though I wish I had been able to follow the ant colony demo (it's audio-only). </p>

<p>It awakened the oft-recurring "functional floundering" feeling. I've written a semester worth of scheme in a programming languages course. I've read the Erlang book and written a little Erlang code. I recently went through a graduate course in programming languages with emphasis on denotational semantics. I <em>understand</em> the lambda calculus, functional programming, etc. But I feel completely stymied whenever I think about actually programming in a functional language.</p>

<p>I'm not sure what the root is, but I'm sure it boils down to lack of practice. That undergraduate course aside, I haven't had any practice. And since that course was very handholding (too much in retrospect), I don't feel like I took any practical skill away from it. Yet I feel that in the future functional programming for concurrency will be important, even if I'm not convinced it will be essential.</p>

<p>So I don't have time right now to really rectify the situation, but that doesn't stop me from wondering—how does one learn practical functional programming? What problem sets do you work through to get the needed practice? I suppose the question can apply to learning any new language, but there is much paradigm carry-over between imperative languages (and probably between functional languages). Are there certain problems that will aid that paradigm shift? If you feel like you've developed functional chops, in any functional language, I'd like to hear in the comments how you got there, what you'd change in retrospect, and your advice for me and others like me.</p>
