---
layout: post
status: publish
published: true
title: We're All Volunteers Here
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 816
wordpress_url: urn:uuid:9f079538-0e84-4026-8b69-b543c40374ba
date: 2007-03-07 10:02:37.000000000 -08:00
tags:
- support
- open source
comments:
- id: 1566
  author: Joseph Hall
  author_email: joseph@thatworks.com
  author_url: http://blog.josephhall.com/
  date: '2007-03-07 10:23:54 -0800'
  date_gmt: ''
  content: |-
    <p>It really is too bad that people have to behave so poorly towards software testers. This person not only had an opportunity to help notify everyone of a bug, but also had the opportunity to research the bug more completely with the person who found it, to accurately reproduce and diagnose it. Instead, they decided to treat the bug reporter as a nuissance.</p>

    <p>I'm going to guess that this project was an open source project. This makes me even more sad. The reluctance of open source developers to dutifully pursue bug reports in an attempt to resolve said bugs can lead to buggy open source software. This doesn't just weaken that project, it weakens the entire open source community.</p>

    <p>In my tech support days, people with <code>The_Tick</code>'s behavior were likely to be fired within their first week. It's a shame that <code>The_Tick</code> can't meet the quality standards of an international computer manufacturer so awful, they died out years ago.</p>
- id: 1567
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-03-07 10:26:57 -0800'
  date_gmt: ''
  content: <p>Ah yes, I thought it was clear - this is an open source project. A fairly
    large one, but not on the scale of Apache or Linux.</p>
---
<p>I had an unpleasant exchange on IRC today when trying to report a bug. I've edited the below in order to anonymize the project and cut out extraneous conversations.</p>

<pre>
09:24 < elg> hi, I tried to register so I can post a bug and trac gave me an
             errr and traceback
09:24 < elg> File "/usr/local/lib/python2.4/site-packages/trac/web/main.py",
             line 387, in dispatch_request dispatcher.dispatch(req)
09:24 < elg> ... "input() already active"
09:25 < The_Tick> yea, known issue
09:25 < The_Tick> can't do anything about it atm
09:26 < The_Tick> http://paste.lisp.org/display/37720 is the proposed fix for it
09:26 < The_Tick> but I'm kinda iffy on doing anything like that
09:26 < elg> ok.. so I can't submit the bug. I can put the leaks file up on the
             web if you like?
09:26 < The_Tick> make a forum post
09:26 < The_Tick> and link to it in the forum post
09:28 < elg> I'm really not keen on joining yet another forum
09:28 < elg> http://hans.fugal.net/tmp/foo.leaks
09:28 < The_Tick> it's just going to get lost in irc
09:29 < elg> perhaps you could post it to the forum then
09:29 < The_Tick> elg: or you could make a forum post
09:29 < The_Tick> elg: look, if this is just you running "leaks foo"
09:29 < The_Tick> we can all do that
09:29 < elg> does it use up 80MB of real memory and a gig of VM for you too?
09:29 < The_Tick> if this is you giving us a patch, then you should be making
                  the post
09:29 < elg> if so, then I can just stay out of it
09:30 < The_Tick> elg: you've been given the option for how to post this
                  correctly
09:30 < The_Tick> trac registration is down, so use the alternative
09:30 < The_Tick> #foo-devl is not a support channel, and #foo is not
                  official support
09:31 < elg> either you're interested in the feedback or not. I'm not interested
             in joining a forum
09:31 < The_Tick> I'm not interested in helping people who will not help
                  themselves
09:31 < elg> i'm not helping myself. I'm trying to help you
09:31 < The_Tick> no
09:31 < The_Tick> you're helping yourself
09:31 < The_Tick> half the bugs we get
09:31 < The_Tick> none of us can reproduce
09:31 < elg> which is the whole point of leaks, right?
09:32 < The_Tick> elg: the point is
09:32 < The_Tick> if I posted this
09:32 < The_Tick> and then someone needed you to run something
09:32 < The_Tick> then I'd have to go find you
09:32 < The_Tick> or
09:32 < elg> i'm happy to give you my email to post there
09:32 < The_Tick> you could just reply since you'd be notified of your own thread
09:32 < The_Tick> wtf
09:32 < The_Tick> you were about to register for trac
09:32 < elg> i will not be following the forum, so it would be impossible for
             them to contact me that way
09:32 < The_Tick> but you won't register for the forums
09:32 < elg> yeah. trac is pushing it
09:33 < The_Tick> then go away
</pre>

<p>Ok, so I <em>was</em> being a little stubborn about not joining a stupid forum just to post a bug to an open source project. But I feel strongly about two issues here. The first is that web forums are stupid and I hate spreading out usernames and passwords to every other site on the web that I visit. The second is that I think, as a developer and user, that we should make it <em>easy</em> for users to give feedback. </p>

<p>Requiring a login on Trac was pushing the easy envelope, but I was willing to do it. I was willing to play the game. When the game broke, they gave me a different game to play instead of just accomodating me because it was their fault that their Trac isn't working in the first place. </p>

<p>I don't care whether people buy your product or just download it. If you want your product to improve, you have to take pride in it. You have to <em>want</em> those bug reports. Almost every open source project I am aware of salivates at the very thought of useful bug reports. On the other hand, users that want their problems fixed need to be intelligent and detail-oriented, gathering as much useful information as they can. I did this for 3 whole days in preparing this report. I read the guidelines on posting bugs on their website. I followed everything to the T. Then they treated me like a pest, instead of a source for valuable information about how their product leaks memory like crazy. </p>

<p>I post this not to vent (I did that on IRC) or to get revenge. I sanitized the project name, it's not important. In fact it's one of my favorite programs and I will continue to use it. I will probably even try again to post this bug when Trac is fixed. I post this so that <em>you</em> will think a little bit about how you treat <em>your</em> volunteer testers/bug reporters (aka users). Take the slightest effort to treat them with respect and accomodate them when your system doesn't work as advertised. It will be worth it.</p>
