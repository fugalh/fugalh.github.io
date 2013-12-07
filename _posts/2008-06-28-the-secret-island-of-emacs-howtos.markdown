---
layout: post
status: publish
published: true
title: The secret island of emacs howtos
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 981
wordpress_url: urn:uuid:5659c386-78be-4f2e-8891-01acf97b63a9
date: '2008-06-28 19:24:37.000000000 -07:00'
tags:
- emacs
- clojure
- lisp
- repl
comments:
- id: 1757
  author: Levi
  author_email: levipearson@gmail.com
  author_url: ''
  date: '2008-06-28 22:50:46 -0700'
  date_gmt: ''
  content: <p>I'll investigate this if you don't get any other responses, but not
    tonight.</p>
- id: 1758
  author: Noah Tye
  author_email: ''
  author_url: http://noah.tyes.us
  date: '2008-06-29 14:08:29 -0700'
  date_gmt: ''
  content: |-
    <p>Put these into your .emacs file:</p>

    <p>; paren matching:
    (show-paren-mode 1)
    ; syntax hilighting:
    (global-font-lock-mode 1)</p>

    <p>Emacs+Lisp is usually handled with SLIME, but I don't know if that works with Clojure (it's not listed on the SLIME page).</p>
- id: 1759
  author: Noah Tye
  author_email: ''
  author_url: http://noah.tyes.us
  date: '2008-06-29 14:09:24 -0700'
  date_gmt: ''
  content: |-
    <p>Suppose I should have used the preview button:</p>

    <pre>; paren matching:
    (show-paren-mode 1)
    ; syntax hilighting:
    (global-font-lock-mode 1)</pre>
---
<p>Word on the street is emacs is teh hotness for lisp hacking. I'm taking a serious look at <a href="http://clojure.org">clojure</a>, which is a lisp that incorporates a lot of what I like about erlang and runs on the JVM. So naturally, I want to see if emacs is all that hype.</p>

<p>I'm having a problem though. I can't find the secret island of emacs howtos, where someone has written a nice one-page article on how to do clojure (or any lisp) hacking in emacs and take advantage of the most awesome good parts. I realize that covering all the cool things would probably take a few hundred pages. I don't have time to learn all the cool things anyway. I just need the <em>most cool</em> things. The gateway drugs if you will.</p>

<p>In specific, I'm looking for:</p>

<ol>
<li>Syntax highlighting</li>
<li>Automatic indentation</li>
<li>Paren matching</li>
<li>Have a REPL window</li>
<li>Evaluate this thing under the cursor</li>
</ol>

<p>And it should all be automatic. I shouldn't have to remember and type 80 characters. The syntax highlighting/indentation should be automagic, and the REPL should be a few memorable keystrokes or in a menu (I don't want to type M-X up up down down left right left right B A every time I want a REPL).</p>

<p>I'll bake a loaf of sourdough for anyone that writes an article for the emacs+clojure newbie.</p>
