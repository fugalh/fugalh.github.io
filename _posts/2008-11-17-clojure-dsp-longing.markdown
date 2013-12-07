---
layout: post
status: publish
published: true
title: Clojure DSP Longing
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1023
wordpress_url: urn:uuid:1952d447-e57e-4afd-978b-ad8fdbc4d8cc
date: '2008-11-17 10:46:00.000000000 -08:00'
tags:
- audio
- cs
- ruby
- dsp
- java
- dynamic
- erlang
- clojure
- phd
- jvm
- concurrency
comments:
- id: 1800
  author: what do lispers think of clojure? - Page 2 | keyongtech
  author_email: ''
  author_url: http://www.keyongtech.com/4708142-what-do-lispers-think-of/2
  date: '2009-01-18 16:50:58 -0800'
  date_gmt: '2009-01-18 16:50:58 -0800'
  content: '[...] Re: what do lispers think of clojure?     Nice post here on the
    topic. I feel EXACTLY the same way :)  http://hans.fugal.net/blog/2008/11/1...re-dsp-longing
    [...]'
- id: 1801
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-01-18 20:34:03 -0800'
  date_gmt: '2009-01-18 20:34:03 -0800'
  content: "keyongtech visitors welcome. If I may weigh in on your discussion without
    going to the trouble of creating an account on your forum…\r\n\r\nComplex number
    support is important for a nontrivial niche, but it is nevertheless a niche. Good
    complex number support is rare, and really it's only recently that even a few
    of the more mainstream languages have gotten decent support (e.g. C99). Usually
    you can work around it, but in the case of Java it's just not worth it unless
    you have other motivations for using Java.\r\n\r\nIf Clojure could have complex
    number support with nice syntax and semantics that used Java Arrays underneath,
    it would not be blindingly fast but it would perhaps be sufficient. I don't hold
    my breath though, because it's not really Clojure's fault. Complex numbers really
    need to be supported by the math library for this to be really useful, so functions
    like `exp()` would need to support it for it to work really well. \r\n\r\nIncidentally,
    I'm using Octave for my research. MATLAB is as funky a language as you could ever
    dream up, but it has all the right stuff for DSP and a lot of other mathematics,
    which many other languages (and most GP languages) simply don't.\r\n\r\nThat said,
    it's likely that the vast majority of DSP code in the real world (which is primarily
    on embedded systems) is written in assembly and C, and have been for years."
- id: 1802
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-01-18 20:38:26 -0800'
  date_gmt: '2009-01-18 20:38:26 -0800'
  content: Oh, and I can verify that Ruby has native support for complex numbers,
    but it's no less clunky than all other things mathematical in Ruby—mathematical
    syntax is not one if its strong suits (though it scores quite well in mathematical
    semantics).
- id: 2305
  author: John Cromartie
  author_email: jcromartie@gmail.com
  author_url: ''
  date: '2010-09-24 01:48:48 -0700'
  date_gmt: '2010-09-24 01:48:48 -0700'
  content: It might be time to revisit Clojure 1.2 with its new deftype features,
    which let you define native JVM types (classes) in Clojure with full performance.
---
<p>I often find myself longing to be able to use <a href="http://clojure.org/">Clojure</a>, a very enticing lispy language that runs on the JVM.</p>

<p>I could possibly be using it right now in my dissertation research. It has the promise of dynamic languages, functional programming, almost-as-cool-as-Erlang concurrency, JVM performance, and Java library soup. It could be so awesome. A few months ago I started briefly down this road, unaware that…</p>

<p>Clojure sucks. Not generally, but it sucks for DSP. More specifically, Java and therefore Clojure has no real support for complex numbers. In order to do serious DSP, you need native syntactic, semantic, and performance support for complex numbers. Java has none of the above. Older versions of C didn't have syntactic or semantic support, but the performance of using arrays was plenty fast. Not so in Java, at least not to the extent necessary to override the lack of syntactic and semantic.</p>

<p>So someday, when I'm writing general purpose code again and not high performance DSP code, I will have an opportunity to use Clojure, and I think that will make me very happy. By then <a href="http://www.pragprog.com/titles/shcloj/programming-clojure">the book</a> will be out of beta. The community will be in full swing. There will be awesome libraries. Children will play in pristine parks with formerly-ravenous ravens. </p>

<p>In the meantime, if anyone sees the scene change, do let me know.</p>
