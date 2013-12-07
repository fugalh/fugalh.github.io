---
layout: post
status: publish
published: true
title: Cr&#232;me Rappel v2
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 935
wordpress_url: urn:uuid:ac1b5ad7-9d75-4d0b-9126-1b8319c7f3b7
date: 2008-02-21 22:19:19.000000000 -08:00
tags:
- mac
- ruby
- bash
- growl
- at
- launchd
- reminder
- creme
- rappel
- cron
comments:
- id: 1716
  author: Alicia
  author_email: benitez_benitezz@yahoo.com
  author_url: http://www.conservativemusings.org
  date: '2008-02-22 06:05:34 -0800'
  date_gmt: ''
  content: <p>Thanks for the step by step. I am trying this out just now and Im quite
    new at exploring this.</p>
---
<p>In the spirit of release early, rewrite often, I have released Crème Rappel      version 2. Version 1 was a shell script that combined Growl and at. Then Apple  released 10.5.2 not half a week later and broke at altogether. Sick of          fighting with launchd and other Apple superiority complexes, I set about to     nurture my own superiority complex and rewrite Crème Rappel to be completely    independent of at.</p>

<p>Of course, that's getting too heavy for a shell script, so I moved to Ruby. One  thing I didn't want was to require a daemon to be running. Daemons can fail or
 forget to start up, and that means I couldn't really truly trust the tool. The  recent at debacle is just another case in point. So, instead I wrote Crème to   fork a process that sleeps until the moment of truth, then fires off the        reminder. It turns out the obvious function for the job, <code>sleep()</code>, is a poor   choice here. In fact, every timer I tried had the same problem, including one   I thought would not: <code>setitimer()</code>. When you suspend the laptop, it appears     you also suspend time. If you don't believe me, try this simple experiment:</p>

<pre><code>date; sleep 30; date
</code></pre>

<p>Put the laptop to sleep during the sleep for a substantial time, then notice     that when you resume you still have to wait for the full 30 seconds to tick by
 even though it has actually been a minute plus since you issued the command.    So I sleep for one second intervals instead, checking the time every time.</p>

<p>This is not just a backpedaling rewrite, though. It also adds more flexible and  easy-to-type timespecs, and a <a href="http://hans.fugal.net/src/creme/">spiffy website</a>.
If you give it a try and it doesn't work, or you struggle with the               documentation, please do drop me a line so I can fix it. I want it to be worth
 every bit of bandwidth that you paid for it.</p>
