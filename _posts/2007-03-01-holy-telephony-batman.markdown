---
layout: post
status: publish
published: true
title: Holy Telephony, Batman!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 805
wordpress_url: urn:uuid:63e36408-d1dc-451b-903c-4568cce93269
date: 2007-03-01 07:20:07.000000000 -08:00
tags:
- asterisk
- voip
- ruby
- batphone
comments:
- id: 1562
  author: Gabriel Gunderson
  author_email: gabe@gundy.org
  author_url: http://gundy.org
  date: '2007-03-01 09:11:05 -0800'
  date_gmt: ''
  content: |-
    <p>Hey, I did the same in <a href="http://gundy.org/asterisk/" rel="nofollow">C# under Mono</a>.  I too did it "for the fun of doing it."</p>

    <p>When I pick up Ruby, your code will be one of the first thing I play with :)</p>
---
<p><img src="http://hans.fugal.net/src/batphone/theme/batphone.png" alt="batphone"/></p>

<p>Does the world need yet another Ruby Asterisk Gateway Interface library? Does
the world need a guy who dresses up like a bat?</p>

<p>I was not satisfied with the complexity and learning curve of existing AGI
libraries for Ruby, so rather than spend an hour learning one of them I spent
several hours writing my own. I hope this pays off in the future when it only
takes me 5 minutes to remember/relearn how to use batphone. It was fun, anyway.
That's the point, isn't it? That's why Batman does it. Not for the citizens of
Gotham, but because it's fun.</p>

<p>Here's a synopsis:</p>

<pre><code>#!/usr/bin/ruby
require 'agi'

agi = AGI.new
agi.answer
agi.stream_file('batman_help_the_monkeys_are_everywhere', nil)
begin
  # press pound to make them stop!
  r = agi.stream_file('tt-monkeys', '#')
end while r.result != ?#
agi.stream_file('POW', nil)
agi.hangup
</code></pre>

<p>Here's the URLs: For Documentation press
<a href="http://hans.fugal.net/src/batphone/doc/">1</a>. For Download press
<a href="http://hans.fugal.net/src/batphone/batphone-0.1.0.tar.gz">2</a>. For direct
access to the batphone press <a href="http://hans.fugal.net/src/batphone">3</a>.</p>

<p>POW!</p>
