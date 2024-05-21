---
layout: post
status: publish
published: true
title: Pre-announcing Clog
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 42
wordpress_url: urn:uuid:8c65ffed-f304-402b-ba37-30c936b4dd14
date: '2005-03-18 17:09:46.000000000 -08:00'
tags:
- linux
comments: []
---
<p>Log files are big boring tangles of spaghetti that are about as much fun to
review in their raw format as it is to go to the dentist. Yet, not reviewing
your logs is one sure-fire way to be negligent, especially when you're a
<em>System Administrator</em>.</p>

<p>I surveyed the options. Logwatch came out on top but it is not as easy to
customize as it should be. So I wrote clog. </p>

<p>This isn't that hard, after all. In
the spirit of "release early, release often" I am "pre-announcing" it. I'm not
declaring a release, and it's bound to change drastically over the next week or
two, but it works and it's ready to go to work for you. If my as of yet small
collection of agents isn't good enough for you, then write your own (it's easy,
especially if you know ruby already; just subclass
<a href="http://hans.fugal.net/src/clog/doc/classes/Clog/Agent.html">Clog::Agent</a>) and
send them to me to be included.</p>

<p><a href="http://hans.fugal.net/src/clog">Browse the code online</a>, or use
<a href="http://abridgegame.org/darcs/">darcs</a>:
    darcs get http://hans.fugal.net/src/clog</p>
