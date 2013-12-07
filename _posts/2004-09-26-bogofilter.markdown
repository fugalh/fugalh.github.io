---
layout: post
status: publish
published: true
title: Bogofilter, procmail, and mutt, oh my!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 41
wordpress_url: urn:uuid:5a39b385-614a-40f9-a0ab-e18814ae485c
date: '2004-09-26 18:11:26.000000000 -07:00'
tags:
- linux
comments: []
---
<p>Spam is not a problem for me. I indiscriminately use my email address when
shopping online, when subscribing to email lists, and when posting to usenet. I
get a lot of spam, but I see almost none of it. I imagine I get just about
every flavor of spam you can imagine, and my spam filtering system does a great
job of correctly filtering it.</p>

<p>I use fetchmail to fetch my mail from various accounts to my home machine. When
it arrives here on falcon, it gets processed by these two procmail rules:</p>

<pre><code>:0fw
| bogofilter -l -e -p


# if bogofilter failed, return the mail to the queue, the MTA will
# retry to deliver it later
# 75 is the value for EX_TEMPFAIL in /usr/include/sysexits.h

:0e
{ EXITCODE=75 HOST }
</code></pre>

<p>Then, it gets processed by other procmail stuff, e.g. to filter out the lists
by the List-Id header. If it makes it through that gauntlet, it hits these
procmail rules:</p>

<pre><code>:0
* ^X-Bogosity: Yes
spam/

:0
* ^X-Bogosity: Unsure
unsure/
</code></pre>

<p>I read my email in mutt. The following is my bogofilter-related mutt
configuration:</p>

<pre><code># &lt;f9&gt; spam, &lt;f10&gt; ham

macro index &lt;f9&gt; "&lt;enter-command&gt;unset wait_key\n\
&lt;pipe-entry&gt;bogofilter -l -s\n\
&lt;enter-command&gt;set wait_key\n\
&lt;save-message&gt;=spam\n" "learn as spam, and save to spambox"

macro index &lt;f10&gt; "&lt;enter-command&gt;unset wait_key\n\
&lt;pipe-entry&gt;bogofilter -l -n\n\
&lt;enter-command&gt;set wait_key\n" "learn as non-spam"

color index yellow default '~h X-Bogosity:\ Yes'
color index green default '~h X-Bogosity:\ Unsure'
</code></pre>

<p>Non-spam (ham) is the normal color, and spam is "yellow" (really more like
brown). If I notice a misclassification, e.g. a mailing list message that's
brown, or a ham in the spam mailbox, I press <code>F9</code> or <code>F10</code> to learn as spam or
ham respectively.</p>

<p>I used to have bogofilter auto-learn, i.e. train itself with its decisions.
This self-reinforcement was interesting, but one day something broke with my
mutt bindings (I don't remember what) and I was too busy to fix it. Soon my
spam filter was completely off-kilter and I just had to disable it altogether.
The next time around I decided to use a minimalistic approach. I decided to
only train bogofilter when it made a mistake. It only took a few days for it to
be quite accurate, and now I rarely notice a mistake. I do still vgrep my spam
occasionally (once or twice a week) to check for false positives. I
occasionally get a false positive, but usually it is related to an online order
or ebay, or something else that I am expecting.</p>

<p>I have been meaning to use the logs to calculate how accurate it is, but I just
haven't got the time. I currently have trained 111 spams and 71 hams, in about
3 months time. I get from 50-100 spams per day, (averaged over the stastically
exhaustive period of the last two days) and a heckuvalot more hams, mostly in
the form of email lists like plug, lad, etc. You can do the math, but it boils
down to being fairly accurate. And even better, it takes almost zero of my time
to maintain.</p>
