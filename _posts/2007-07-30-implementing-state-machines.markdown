---
layout: post
status: publish
published: true
title: Implementing State Machines
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 857
wordpress_url: urn:uuid:8ba083c1-4d5a-42ab-9240-7127921d596f
date: 2007-07-30 22:40:00.000000000 -07:00
tags:
- cs
- ruby
- state
- dfa
comments:
- id: 1590
  author: Levi
  author_email: levipearson@gmail.com
  author_url: http://lifeoflevi.com/blog/
  date: '2007-07-31 11:10:34 -0700'
  date_gmt: ''
  content: |-
    <p>I followed a somewhat similar approach when I had to write a bunch of automata for CS252 at BYU years ago, though I did it in Python and didn't abstract things quite as much.  This looks pretty slick, though.</p>

    <p>My favorite automata approach is given by Shriram Khrishnamurthi in a presentation he called <a href="http://technetcast.ddj.com/tnc_play_stream.html?stream_id=644" rel="nofollow">"The Swine Before Perl"</a>.  It only works well in Scheme or other languages that mandate tail-call optimization, and it's most elegant when macros are available.  In any case you should listen to the presentation and follow along with the slides, because Shriram is a highly engaging and entertaining presenter.</p>
- id: 1591
  author: JamesCField
  author_email: ''
  author_url: ''
  date: '2007-11-12 15:54:01 -0800'
  date_gmt: ''
  content: |-
    <p>Perhaps you mean to use the term "FINITE STATE MACHINE".</p>

    <p>Otherwise I don't understand what you are talking about.</p>
- id: 1592
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-11-12 16:00:51 -0800'
  date_gmt: ''
  content: <p>I think that's fairly obvious. Good clues might be common usage, DFAs,
    and the finite automata graph. Be sure to let me know next time you come across
    an infinite state machine, so I can begin to be more careful about that adjective.</p>
- id: 1593
  author: Loran
  author_email: freeloran@free.fr
  author_url: ''
  date: '2008-08-04 03:30:39 -0700'
  date_gmt: ''
  content: <p>Really a simple and nice way to implement a state machine. It helped
    me a lot.</p>
---
<p>The lowly state machine, aka finite automata, is a beautiful and useful thing,
on paper. But when it comes time to code one up, things can get ugly. You see,
any first-year CS student can code up a state machine in the naïve way—with a
state variable and a big nested while/case/if mess. It's hard to read, it's
tedious to code, and it's very easy to get yourself <acronym title="DRY: Don't
Repeat Yourself">all wet if you're not careful.</acronym> Then there's the
state transition table where you put all the state transition information in a
hardcoded table, or in a source file that you write a program to generate the
static table from, or if you're really fancy you read the source file at
runtime. These get uglier than ugly, real fast.</p>

<p>I've always known deep down that there must be a better way to write state
machines, at least in languages with the necessary niceties. I've implemented a
number of semielegant state machines, but never really felt I hit on the One
True Pattern™. Speaking of patterns, the Gang of Four have a state pattern for
overengineering state machines with the magic of object-oriented programming.
It's definitely more OO than the traditional approach. Probably one of the
better ways to do it in C++ or Java. But let me share with you what I figured
out in Ruby this evening.</p>

<p>Disclaimer: I'm probably not the first to come up with something like this, but
I didn't see anything in my feeble attempts at googling state machine
implementations. Second disclaimer: this is an agile state machine pattern; it
doesn't concern itself with being bulletproof, all-encompassing, or high
performance. But it's dead simple, very little code which is very easy to read,
very flexible, and elegant. You and I should be able to adapt it to our needs
easily many times over.</p>

<p>Here's a sample state machine, and the code for implementing it (in the code I add arbitrary final states and a transition action for demonstration purposes):</p>

<p><img src="http://hans.fugal.net/images/transducer.png" alt="Transducer"/></p>

<pre><code>  require 'dfa'

  d = DFA.new('A', ['A','C'])
  d.transition do |s,a|
    ss = case [s, a]
         when ['A', 0]: 'B'
         when ['A', 1]: 'C'
         when ['B', 0]: 'B'
         when ['B', 1]: 'C'
         when ['C', 0]: 'D'
         when ['C', 1]: 'C'
         when ['D', 0]: 'A'
         when ['D', 1]: 'C'
         else raise "Invalid transition (#{s}, #{a})"
         end
    print ss
    ss
  end

  ary = [0,0,0,1,1,1,0,1,1,1,0,0].map do |a|
    d.eat a
  end
  puts
  p ary
</code></pre>

<p>The file <a href="http://hans.fugal.net/src/dfa/dfa.rb"><code>dfa.rb</code></a> which contains the <a href="http://hans.fugal.net/src/dfa/doc">DFA class</a> is straightforward too.</p>

<p>Notice how you're free to implement the transition function however you like,
e.g. by parsing a config file or hardcoding a state transition table, or
clumping things together in an intuitive or even metaprogramming way if you
have a lot of similar transitions. Notice that you don't have to do formal
dances like defining the set of states explicitly, but the underlying theory is
sound. Notice how you can get the input any way you please, and feed it to the
state machine one piece at a time. Nothing is holding you down, you are free!
And yet none of these things is in the least bit harder than if you hadn't used
it. It's helpful but transparent. It is cuter than your cat and more loyal than
your dog. Ok, I'll stop now.</p>

<p>The basic pattern is, in case you haven't been reading the code and
documentation (ahem), abstract away the state-tracking stuff into the DFA
object; provide the transition function which aligns nicely with theory (d: S x
∑ → S), and we'll look the other way if you sneak some transitional actions in
there; and provide the input loop. All you really need in your pet language is
first-class functions. Duck typing would (as always) be nice too, because then
your states can be meaningful objects, eliminating an extra layer of
indirection. It might not turn out as pretty in your language, but it would be as flexible and DRY.</p>

<p>Extending this to nondeterministic finite state automata wouldn't be hard, either, if that's what you need.  </p>

<p>If you have a better way to do state machines (or a pretty-good way in
<code>$your_favorite_crippled_language</code>), do tell in the comments.</p>
