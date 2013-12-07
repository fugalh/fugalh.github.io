---
layout: post
status: publish
published: true
title: Joystick Hat in X-Plane in Linux
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 843
wordpress_url: urn:uuid:494eca87-5cb1-4566-ad0c-cf41c757df90
date: 2007-06-02 23:37:00.000000000 -07:00
tags:
- linux
- xplane
- joystick
- hat
- service
comments:
- id: 1572
  author: dave@thesmithfam.org
  author_email: ''
  author_url: ''
  date: '2007-06-11 16:58:25 -0700'
  date_gmt: ''
  content: |-
    <p>Well done Hans! A delightful hack.</p>

    <p>--Dave</p>
- id: 1573
  author: Tim Miller
  author_email: timmy1865@gmail.com
  author_url: ''
  date: '2007-07-03 12:53:07 -0700'
  date_gmt: ''
  content: |-
    <p>Thanks for this bit of code, it works great, and has relieved one of my primary Linux-transition headaches.</p>

    <p>But after reading the back and forth with Austin, I think he's right. The hat really is a set of buttons, in the sense that they are discrete (on/off) rather than continuous. You mentioned that the device reports them as axes? I think maybe the ultimate solution would be to complain to CH Products (and the other manufacturers). The hat is certainly implemented as two axes, but it should probably report as buttons.</p>
- id: 1574
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-07-03 13:59:55 -0700'
  date_gmt: ''
  content: |-
    <p>They are discrete, yes, but they are not independent. You cannot press both the "left hat" and the "right hat" button at the same time. In this sense they are axes. You could say they're discrete axes. </p>

    <p>The question is not whether hats <em>should be</em> buttons or axes. The fact is the manufacturers (my count so far is at least 3 joysticks from 3 manufacturers all working the exact same way - with no reason to suspect anyone does things differently) chose to use axes, and different operating systems choose to translate that into buttons or not, as they see fit. It's not the first, last, or largest difference between operating systems. Differences are part and parcel of writing cross-platform programs.</p>

    <p>Incidentally, js_demo (from FlightGear) reports the hat as axes on OS X also, though X-Plane recognizes them as buttons. Either FlightGear or X-Plane is doing a translation here. I'm not sure which, though I'd like to find out what is natively reported by OS X's driver, if anyone knows of a quick way to find that out.</p>
- id: 1575
  author: Hayden
  author_email: ''
  author_url: ''
  date: '2007-08-20 14:02:57 -0700'
  date_gmt: ''
  content: <p>Hi, I am have the same problem as yours originally except that I am
    using a sim called flightgear. Has anyone used this hack with it successfully?</p>
- id: 1576
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-08-20 14:05:34 -0700'
  date_gmt: ''
  content: |-
    <p>Hi Hayden,</p>

    <p>I'm a FlightGear user too and I'm not familiar with any situation where this is a problem. It can probably be fixed directly by modifying the (perhaps buggy?) Joystick definition file. If you wanted to use this hack anyway, you'd need to hack the code to send whatever keyboard sequence you need to do what you want done in FG.</p>
- id: 1577
  author: Hayden
  author_email: ''
  author_url: ''
  date: '2007-08-20 14:23:24 -0700'
  date_gmt: ''
  content: <p>Sorry, I messed up I meant targetware. Big mistake right there. It is
    a cross platform flightsim like flightgear. I read your rant, and then was thinking
    about flightgear. Anyways, the problem is with targetware not flightgear. Flightgear
    worked out of the box with my logitech extreme 3d pro. I modified the paths in
    your script, but it didn't seem to change anything in the program. I even modified
    the joystick config file to have a hat, but no luck. heres the link if you arn't
    familiar with it <a href="http://targetware.net" rel="nofollow">http://targetware.net</a>
    (Its a great flightsim) :)</p>
- id: 1578
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-08-21 20:50:37 -0700'
  date_gmt: ''
  content: <p>You won't need to modify the paths, but the keys generated. Edit the
    .c file and change "Left", "Right", etc. to the keys that change view in targetware.
    Good luck.</p>
- id: 1579
  author: Tycho
  author_email: ''
  author_url: ''
  date: '2008-08-25 05:17:10 -0700'
  date_gmt: ''
  content: |-
    <p>Thanks for the program. Works like a charm with Open Source Freespace.</p>

    <p>With the directions mapped to Num1 to Num9 (without 5) it would even be possible to use e.g. top-left as a own button. But it's probably not worth the trouble because it's at least with my joystick quite hard to trigger a top-left without triggering top or left.</p>
- id: 2038
  author: Oliver
  author_email: monks700@gmail.com
  author_url: ''
  date: '2009-06-19 19:32:44 -0700'
  date_gmt: '2009-06-19 19:32:44 -0700'
  content: Thank you. I cant wait to try this out once I get back down to my Desktop
- id: 2043
  author: cancon
  author_email: dadaism@gmail.com
  author_url: ''
  date: '2009-06-28 09:27:56 -0700'
  date_gmt: '2009-06-28 09:27:56 -0700'
  content: Beautiful, simple solution. Thanks.
- id: 2254
  author: Getfuzzed
  author_email: dgwaldo71@hotmail.com
  author_url: ''
  date: '2010-05-21 02:04:13 -0700'
  date_gmt: '2010-05-21 02:04:13 -0700'
  content: Thank you!!!  The only reason I bought Xplane is because it was supported
    on Linux, I have left Microsoft behind, and it sad to hear that the Xplane developer
    is not fully into Linux support...
- id: 2298
  author: Alberto
  author_email: ingsalvi@tiscalinet.it
  author_url: ''
  date: '2010-08-31 07:10:00 -0700'
  date_gmt: '2010-08-31 07:10:00 -0700'
  content: "Thank you for this. I recompiled \"my\" version in order to generate \"Q,W,E,S\"
    keys (W was reassigned, in X-Plane, so to \"look up\" instead of \"look front\").
    This way both external and 3d cockpit view do work\r\n\r\nWorks like magic."
- id: 2321
  author: mungewell
  author_email: simon@mungewell.org
  author_url: ''
  date: '2010-11-17 07:04:09 -0800'
  date_gmt: '2010-11-17 07:04:09 -0800'
  content: "There is actually a subtle difference between a D-PAD and a HAT. D-PADs
    are described as switches, whilst a HAT is more like a dial with a null state.\r\n\r\nFor
    the controller I have, the HAT is reported on the USB bus as degrees (with 8 possible
    positions) which Linux converts into an X-Y axis.\r\n--\r\n        Logical Maximum
    (7),\r\n        Physical Maximum (315),\r\n        Report Size (4),\r\n        Report
    Count (1),\r\n        Unit (Degrees),\r\n        Usage (Hat Switch),             ;
    Hat switch (39h, dynamic value)\r\n        Input (Variable, Null State),\r\n        Unit,\r\n--\r\n\r\nYou
    can grab and decode the USB HID descriptor using DIGImend (http://digimend.sourceforge.net/)"
- id: 2322
  author: Hans
  author_email: ''
  author_url: ''
  date: '2010-11-17 16:13:07 -0800'
  date_gmt: '2010-11-17 16:13:07 -0800'
  content: Interesting detail which helps explain the different interpretations. Thanks
- id: 2338
  author: Mike
  author_email: cbr9nmr2001@yahoo.com
  author_url: ''
  date: '2011-01-13 23:01:02 -0800'
  date_gmt: '2011-01-13 23:01:02 -0800'
  content: "Lost Linux newb here,\r\n Does this make the hat report as key press and
    you edit jhat.c to say which keys are sent or does it make the hat show up as
    buttons in X-Plane where you can define them?\r\n  In the README I used the Synaptic
    Package Manager to Install xautomation.  I don't know what to edit in the script,
    how to \"make\" or where and how to install.  I did a couple of Google searches
    for jhat help and installation but didn't find anything."
- id: 2391
  author: Configuring a game pad in xbmc &laquo; &laquo; Memory Dump Memory Dump
  author_email: ''
  author_url: http://www.betasix.net/configuring-a-game-pad-in-xbmc/
  date: '2011-04-30 15:54:26 -0700'
  date_gmt: '2011-04-30 15:54:26 -0700'
  content: '[...] http://hans.fugal.net/blog/2007/06/02/joystick-hat-in-x-plane-in-linux/
    [...]'
- id: 2409
  author: Miro
  author_email: miro.bogner@gmail.com
  author_url: ''
  date: '2011-07-28 16:51:04 -0700'
  date_gmt: '2011-07-28 16:51:04 -0700'
  content: "Hallo,\r\nthanks for that patch!!\r\nStill I'm having some problems with
    it and it would be nice to get some help when you have the time.\r\nI'm able to
    run the script when I change the grep line to:\r\n\"if grep -q \"$name\" $d/device/name
    2&gt;/dev/null; then\"\r\nIn that case the right device is used for my joystick!
    Still the hat is considert as 2 axis and not as 4 buttons. \r\n\r\nrunning arch
    linux 64bit, lastest  xautomation is installed from aur.\r\n\r\nThanks!"
- id: 2410
  author: Miro
  author_email: miro.bogner@gmail.com
  author_url: ''
  date: '2011-07-28 17:17:28 -0700'
  date_gmt: '2011-07-28 17:17:28 -0700'
  content: "Ok, the problem was, that I still had the axes assigned to look around
    in the cockpit with was interfering with your hack..\r\nIt's workig now. Is it
    possible to assign other buttions to the hat? I think I would be better to have
    the \"head move\" buttons (q and e, s..) to the hat, so it's not just scrolling
    left/right/up/down, but look out of the different windows.."
- id: 2411
  author: Hans
  author_email: ''
  author_url: ''
  date: '2011-07-28 17:23:39 -0700'
  date_gmt: '2011-07-28 17:23:39 -0700'
  content: You can change the key names in the calls to keydown() in jhat.c, to whatever
    you like. e.g. instead of "keydown(xte_fd, "Left", &amp;w);" you might say "keydown(xte_fd,
    "q", &amp;w);"
- id: 2412
  author: Miro
  author_email: miro.bogner@gmail.com
  author_url: ''
  date: '2011-07-28 17:33:31 -0700'
  date_gmt: '2011-07-28 17:33:31 -0700'
  content: Ok, got that also, had to use key "w" as "look pan up" and than replace
    "LEFT" with "q", RIGHT with "e", "UP" with "w" and "DOWN" with "s" in jhat.c,
    compile new and it works like a charm!
- id: 2429
  author: Mike
  author_email: cbr9nmr2001@yahoo.com
  author_url: ''
  date: '2011-10-11 22:08:45 -0700'
  date_gmt: '2011-10-11 22:08:45 -0700'
  content: How would one input function keys in the keyup and keydown lines?
- id: 2430
  author: Mike
  author_email: cbr9nmr2001@yahoo.com
  author_url: ''
  date: '2011-10-11 22:17:09 -0700'
  date_gmt: '2011-10-11 22:17:09 -0700'
  content: I'm guessing it is "{F1}"  2,3,4 etc.  I suppose I should experiment and
    find out.
- id: 2518
  author: Best Flight Simulator 2011
  author_email: Apt872@rocketmail.com
  author_url: http://www.delicious.com/url/9c61d490af074f97c43a874862cfc555
  date: '2012-02-27 12:31:10 -0800'
  date_gmt: '2012-02-27 12:31:10 -0800'
  content: whoah this blog is magnificent i love reading your articles. Keep up the
    great work! You know, a lot of people are looking around for this information,
    you can help them greatly.
- id: 2759
  author: kaktuli
  author_email: kaktuli@op.pl
  author_url: ''
  date: '2013-04-26 20:43:27 -0700'
  date_gmt: '2013-04-26 20:43:27 -0700'
  content: "Well, considering that the whole X-Plane's UI looks like one big hack,
    I'm not surprised that adding some 'options' to the UI is a pain in the ass. Experienced
    programmers do things correctly, unexperienced write code that's hard to maintain
    or change.\r\n\r\nI don't want to bash the author, but I'm a programmer, and this
    situation when adding some simple UI seems so hard is ridiculous. Overall I enjoy
    Flightgear's UI more, but I still love the physics of X-Plane. Maybe he is more
    of a physicist than a programmer, after all…"
---
<p>Preface: this is a long rant. If you just want your joystick hat to work in X-Plane, download <a href="http://hans.fugal.net/src/jhat.tar.gz">jhat</a> and follow the instructions in the README. </p>

<p>Linux reports joystick hats as axes, because that's what the device reports
them as. Windows drivers often put up a façade where the directional hat is
translated into 4 buttons. X-Plane is Windows-centric and therefore directional
hats don't work in X-Plane in Linux.</p>

<p>I submitted a bug report, and was told</p>

<blockquote>
    <p>i cant do that<br/>
    i have to use what is reported<br/>
    but you can assign an AXIS to look around.. it is one of the joystick axis options... </p>
</blockquote>

<p>Actually, you can't use the "look around" axis, because the joystick hat is not
analog, but tristate. It's either left, middle, or right (or up, middle, or
down for the vertical axis). So you are either looking behind you, in front of
you, or behind you - not the most useful combination. I informed him of the
situation, and provided him with some pseudocode for handling the axes. I'm
always amused when developers try to delude the user and themselves into
thinking some bug or feature is impossible to fix or implement. Human nature is
a funny thing. Sometimes we even believe it ourselves. His reply to my information and pseudocode:</p>

<blockquote>
    <p>the code would be easy, but i wont write a whole new type of axis response just for a few computers that are not working right<br/>
    it is too much confusion for too little gain<br/>
    sorry! </p>
</blockquote>

<p>Wow, this task has gone from being impossible to being easy in one short day!
Well of course it's easy. I knew that. He knew that. Now we're on the same
page. The real reason he won't do it is because he doesn't want to. It would be
easy, but it would be inconvenient. And those darned pesky Linux freaks aren't
worth the trouble. Now, at this point I'm struggling to be cordial, but I
believe it's important to remain cordial until the bitter end. I replied with
my condolences that he has so few Linux customers that he shouldn't care if his
software is broken in Linux. I also tossed out some more ideas - a different
type of axis behavior for scrolling instead of absolute positioning, etc. His
reply,</p>

<blockquote>
    <p>i have very few linux users, this is true</p>

    <p>also, it seems obvious to me that the OS should report the hardware properly... not that the app should work backwards and add more confusion for EVERYONE because ONE person did not do his job properly! </p>
</blockquote>

<p>Now he's getting defensive. The truth hurts sometimes. Let's step back and
review. The joystick reports the directional hat as 2 axes. It's a HID device,
so there is no need for special drivers. However, somewhere along the line (I
don't know the history), some joystick driver writer in Windows (probably
before HID even existed) decided that directional hats should be represented at
4 buttons. Does one make more sense than the other? I don't think so. I think
they're both valid viewpoints. I'm not surprised the engineers chose to use
axes. I'm not surprised the programmers wanted to use 4 buttons. Two valid
viewpoints. What we have, however, is a lack of standards. There is nothing to
my knowledge that says joystick hats should be buttons, it's just Windows
convention. Windows convention is fine and dandy in a Windows world, but
Windows convention doesn't stand up very well as a challenger to the
appropriateness of faithfully representing what the HID device itself reports.
This is not about a Linux developer slacking on the job. This is about the
world being a complicated place where sometimes things are implemented
differently for perfectly valid reasons. If you want to play the portability
game, you have to deal with this stuff. He knows that, I'm sure. It's just
laziness, hubris, and now a personal resolution to not give in to this pesky
Linux freak.</p>

<p>One more cordial reply from me, stating that both can be right, and a terse
reply from him:</p>

<blockquote>
    <p>no, i think linux is wrong here<br/>
    a button is a button, not an axis </p>
</blockquote>

<p>I didn't reply anymore, it would serve no purpose. I <em>could</em> say, "an axis is
an axis, not a button", because it is an axis after all. But I see I'm not
going to change his mind or convince him. So I took a different tack. I visited
the <a href="http://forums.x-plane.org/lofiversion/index.php?t15720.html">old forum thread</a>  with the not-really-feasible <code>joydev.c</code> patch that others
came up with and encouraged them to encourage the author to consider treating
us Linux customers to a simple bug fix.</p>

<p>But the gauntlet was down. I can't just leave a technical problem like this,
that should be so easy, in eternal limbo. I have to see if it can be solved. I
read through <code>joydev.c</code> in the kernel and thought about what it would take to
make a robust patch that wouldn't have problems with plugging things in in
different orders and wouldn't ruin other joysticks' behavior. I thought of a
way, but I didn't implement it. I decided there had to be a better way. An
easier way. A userspace way. And so there was.</p>

<p>I knew it was easy to read the joystick events in user space. I figured there
just had to be a way to synthesize the fake joystick events that I needed. I
tried to grok the input core and event subsystems. I read articles in Linux
Journal. I groped through kernel changelogs and looked high and low for what
this weird <code>uevent</code> file in sysfs was (completely unrelated—it's a buffer to
aid hotplug in managing coldplug events). I exhausted poor Dr. Google. And then
I stumbled upon <a href="http://docsrv.sco.com/cgi-bin/man/man?XTEST+X3xext">a manpage for the XTest X extension</a>. In a flood the blinds were
lifted and I realized that what I needed was not to synthesize joystick events
(hard), but to synthesize the keyboard events (easier). Not only that, but I
didn't have to synthesize them at the kernel level, I could synthesize them in
X (easy). </p>

<p>An hour or two later I had finished the task. It's a beautiful thing, to be
able to look around in X-Plane. I call it jhat because I was feeling pretty unimaginative at the time. It uses <a href="http://hoopajoo.net/projects/xautomation.html">xautomation</a> to do the XTest stuff because I was feeling pretty lazy at the time. Grab <a href="http://hans.fugal.net/src/jhat.tar.gz">the tarball</a>.Now I have two flight simulators that I can
stand to fly. I prefer FlightGear for many reasons, not the least of which is
this whole fiasco (I could have submitted a patch in the first place and nobody
would have gotten hurt). But I do like X-Plane because some of the planes that
are available I do so enjoy flying, like the Mooney M20K.</p>

<p>So, as a follow up to my earlier post on respecting your bug reporters, let
this be a lesson to you developers out there: every user matters. Especially
paying users. If you don't want to support Linux, then by all means don't
support Linux. You're not fooling anyone when you do a half-baked job of
supporting his platform. </p>
