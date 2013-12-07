---
layout: post
status: publish
published: true
title: Lessons Learned From a Fight With Procmail
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 874
wordpress_url: urn:uuid:7e553e44-4bb2-471b-860f-03cee4e0d174
date: 2007-09-19 12:38:00.000000000 -07:00
tags:
- procmail
- sunos
- solaris
comments: []
---
<p>What should have been a simple procmail autoreply:</p>

<pre><code>:0hc
* ^TO_hfugal\+cs110
* ^Subject: *lab +[0-9]+ +submission
| (formail -rt -I"Reply-To: hfugal+cs110@cs.nmsu.edu"; \
   echo "Submission Received") | $SENDMAIL -t
</code></pre>

<p>became a morning-long wrestling match. I made a few mistakes (forgot to escape the + in the first condition), but mostly it was utter stubbornness on th epart of SunOS. So here are the lessons I learned:</p>

<ul>
<li>Use <code>VERBOSE=yes</code> from the very beginning.</li>
<li><code>LOG=`formail -v`</code> and the like makes for a great debugging trick when you don't have shell access.</li>
<li><code>SunOS mail 5.10 Generic_125100-10 sun4v sparc SUNW,Sun-Fire-T1000</code> doesn't have formail.</li>
<li>Even if you build formail and put it in your <code>PATH</code>, it doesn't seem to work (but <code>! hans@example.com</code> does, so sending mail from that box <em>should</em> work)</li>
<li>It's easier to just forward it to a more friendly email server and do the heavy lifting there.</li>
</ul>

<p>So on the Solaris server:</p>

<pre><code>:0c
* ^TO_hfugal\+cs110
* ^Subject: *lab +[0-9]+ +submission
! hans@fugal.net
</code></pre>

<p>On my own sane Linux server:</p>

<pre><code>:0h
* ^TO_hfugal\+cs110
| (formail -rt -I'Reply-To: hfugal+cs110@cs.nmsu.edu'; \
   echo "Submission Received") | $SENDMAIL -t
</code></pre>
