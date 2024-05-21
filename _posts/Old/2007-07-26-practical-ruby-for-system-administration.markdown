---
layout: post
status: publish
published: true
title: Practical Ruby for System Administration
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 854
wordpress_url: urn:uuid:cfa5edba-b2da-474b-9d27-c282f0d37e99
date: '2007-07-26 12:16:00.000000000 -07:00'
tags:
- linux
- mac
- reviews
- ruby
- review
- sysadmin
- book
comments:
- id: 1587
  author: Paul J
  author_email: ''
  author_url: ''
  date: '2008-02-27 09:51:41 -0800'
  date_gmt: ''
  content: <p>Thanks, I have been looking to incorporate Ruby into my sysadmin position.
    I have some of the same feelings that you had about writing in a program language
    that my co-workers will probably curse me for. I just figure down the road Ruby
    will enjoy further acceptance and I will be ahead of the game. I am going to pick
    up a copy of this book.</p>
---
<div style="float:right"><img src="http://www.apress.com/ApressCorporate/supplement/1/10262/bcm.gif"/></div>

<p>I love Ruby, and I use it whenever I can for all kinds of tasks. When I was
working as a professional system administrator, I put it to good use a few
times there too. But using ruby always left me feeling a little guilty, because
whoever came after me would probably curse my name for using a "nonstandard"
language. It didn't help that Ruby was rarely installed, if even available, by
the popular server distributions of the day. But all that has changed in the
past two years, and using Ruby is often acceptable even in the conservative
world of system administration.</p>

<p>You can imagine my interest then, in a book titled "<a href="http://www.apress.com/book/bookDisplay.html?bID=10262">Practical Ruby for System
Administration</a>" by André Ben Hamou. The title is telling; Ruby is known for
being recommended by <a href="http://www.pragmaticprogrammer.com/">The Pragmatic Programmers</a> because, well, it's a pragmatic
language. System administration is all about pragmatism, above all else. Doing
things right is important, but doing them <em>now</em> is more important. I knew all
along that Ruby was an excellent tool for the enlightened sysadmin; now there's
a book to back me up.</p>

<p>The book starts out with why you would want to use Ruby, and nips the
counterarguments in the bud. Hamou does a good job on both counts, though as I
already know Ruby I can't say whether the language introduction is sufficient
of its own accord to get started with actually writing Ruby, or whether you'll
need to refer to other sources (which are available online).</p>

<p>In chapter 2 he discusses one-liners. One-liners are the staple of many
sysadmins, but I never fell for them. I'd rather write a throwaway script than
try to cram it all on one line, or if it can really be done well on one line it
can probably be done even more concisely with shell script and UNIX tools.
However, the chapter does discuss a lot of fascinating switches that the <code>ruby</code>
executable takes. I can see myself using many of these, and I was ignorant of
most of them. You might learn the same from a careful study of the man page,
but Hamou presents it in an easier-to-digest format. It's not always easy to
inject humor into a book while maintaining concise brevity, but Hamou does a
decent job of that. I found myself laughing aloud more than once, and yet I
feel that the book is concise enough to serve as a reference, and that the
jokes won't get annoying after a few readings of a section.</p>

<p>This book is not only a great book for the sysadmin hoping to use Ruby, but also an excellent book for any sysadmin who may not even be interested in Ruby. Although not even pretending to be a book on system administration best practices, there are many gems in here that will leave you saying "Why didn't I think of that?" and "I really need to implement that. It will be so helpful and it's astoundingly simple to do with Ruby!"</p>

<p>Chapter 3 gives you not only a quantitative feel for the speed of Ruby versus other performance-oriented languages (i.e. C), but it teaches you when to be concerned with execution speed, when to be concerned with implementation speed, and makes you think twice about your own feelings about performance. "Ruby is slow" is one of the favorite counterarguments against Ruby, but it's rarely a good one. This is even more true in system administration, where the sysadmin's time is much more important than whether the script runs in 1/10 second or 3 seconds.</p>

<p>Chapter 4 discusses "metaprogramming". I found myself at odds with Hamou most in this chapter, but it was all academic differences in terminology. He's fairly sloppy with the term metaprogramming and other terms (e.g. "macros") in this chapter, but the content is nonetheless a useful and vital part of making the most out of Ruby. I even learned a thing or two. He discusses domain-specific languages (DSLs) in Ruby, but mostly at the level of recognizing one when you see one. I think the world needs a paper or book on rapidly making your own DSLs, something sysadmins could really leverage if it were truly easy to do. I've written a DSL in Ruby, and while easier than I could possibly have imagined it's still not at the level of "easy and completely generic" that I feel DSLs can one day reach. </p>

<p>Chapter 5 is where the fun really begins. With the basics of the language under our belts we can really look at specific examples. This is where the book really shines, both as a tool for applying Ruby and as a minefield of good sysadmin practice. We learn to read and write files, with examples for the most common ones. I don't mean we discuss <code>IO.open</code> and <code>IO.close</code> in detail, I mean we talk about the concepts that apply across all kinds of file reading/parsing and generation, including issues of locking.</p>

<p>In chapter 6 we explore the storage and retreival of data, in a variety of approaches including <code>inspect</code>, marshalling, YAML, and ActiveRecord. Most interesting to me was the section on memcached. I think he ought to also have introduced SQLite (perhaps in the context of ActiveRecord) and DRb.</p>

<p>Chapter 7 is dedicated to dealing with "enterprise data". You know that of which we speak. XML, CSVs, protocols like XML-RPC, SOAP. Most valuable to me in this chapter was a coherent discussion of what REST is (finally!) and how to do it in Ruby.</p>

<p>Chapter 8 discusses network, including writing simple clients and servers. One tendency Hamou has in this book is to use pure Ruby and steer clear of system and backticks. This tendency sticks out in this chapter, where much time is spent discussing that which could be acheived better with a shell script, or at least a Ruby script with judicious use of <code>system</code> or backticks. The general argument for doing things in pure Ruby is portability, and to a lesser extent performance. Neither of these is the first concern of a sysadmin, who is generally not going to write a script that must work on more than one platform (even if it runs on several different Linux/UNIX distributions, which have the same GNU tools).</p>

<p>Chapter 9 deals with that task which we all hate: network and log monitoring. He has some gems of wisdom herein, but all in all we're left feeling about the same as when we went in: we can do it (now we can do it with Ruby) but it's a pain. The gains are not as great here as they are in other areas. This isn't Ruby's fault, nor Hamou's, it's just that nobody's really come up with a good and general way to attack this problem yet.</p>

<p>Chapter 10 discusses RubyGems. I think it's fitting that such a chapter be at the end of the book, and that's all I have to say about that today.</p>

<p>Chapter 11 discusses testing. You should do it in some form and he discusses a few forms. Nothing earth-shattering here, from where I sit. Chapter 12 talks about the future of Ruby, and will probably cause you to salivate.</p>

<p>All in all, an excellent book on using Ruby as a sysadmin. Go ahead, come out of the closet. Ruby is not only OK, it's often the best choice.</p>
