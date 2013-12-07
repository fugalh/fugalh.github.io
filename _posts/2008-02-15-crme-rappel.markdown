---
layout: post
status: publish
published: true
title: Cr&#232;me Rappel
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 932
wordpress_url: urn:uuid:44cb7dd7-9fdc-411f-b00f-10fac453474f
date: 2008-02-15 11:15:00.000000000 -08:00
tags:
- reminder
- creme
- notification
- pester
- notify
- timer
- mumbles
- inotify
comments:
- id: 1707
  author: Eduardo
  author_email: esanzgar@terra.es
  author_url: ''
  date: '2008-07-03 15:34:45 -0700'
  date_gmt: ''
  content: |-
    <p>I like creme. Thanks</p>

    <p>I am trying to play with date and I am not able to setting up the notification.</p>

    <p>Could you give me and example of how to set up a notification for July 28th 2008 starting at 00:01?</p>

    <p>I am entering:
    0001 July 28 2008</p>

    <p>Fri Jul 04 00:01:00 -0600 2008 (1775)</p>

    <p>What I am doing wrong?
    Thanks</p>
- id: 1708
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-07-08 11:33:00 -0700'
  date_gmt: ''
  content: |-
    <p>Hi Eduardo, you need quotation marks:</p>

    <pre><code>$ creme '0001 july 28 2008' test
    Mon Jul 28 00:01:00 -0600 2008 (1756)
    </code></pre>
- id: 1709
  author: Keith
  author_email: kbeckman@mcg.edu
  author_url: http://alphahelical.com
  date: '2008-08-01 23:31:52 -0700'
  date_gmt: ''
  content: |-
    <p>in <code>at_time.rb:parse_time</code>, the regex matches are in the wrong order, resulting in being unable to match timespecs such as "noon tomorrow". Altered as per below, it works like a charm. Thanks for the great util! I use it daily…</p>

    <pre><code>elsif str =~ /^midnight/i
    </code></pre>
- id: 1710
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-08-01 23:47:53 -0700'
  date_gmt: ''
  content: |-
    <p>Thanks for the bug report. I opted to fix it like this instead:</p>

    <pre><code>elsif 'midnight' =~ /^#{str.strip[0]}/i
    </code></pre>
---
<p>People doing creative work, e.g. programmers and grad students trying to write survey papers (ahem), do their best to get into the zone. Once there, the challenge is getting <em>out</em> of the zone at the right time. I've missed more classes and busses and meals than I can count because I was in the zone.</p>

<p>Another problem is that this business of trying to remember when to get out of the zone steals precious productive energy from the brain. So much better if you can rely on something external to remind you of things to be done, so you can literally lose yourself in the work.</p>

<p>The traditional approach is to program your calendar application to bring up an annoying dialog. This has several drawbacks. The UI is cumbersome. It's calendar-centric; you have to make a calendar entry to get an alarm. I don't know about you but I'm not inerested in entering the bus I intend to catch into a calendar. Entering a random event (e.g. take the bread out of the oven) is more trouble than it's worth. It's just the wrong way to do it.</p>

<p>Another approach is to use a watch with a timer. It's a bit faster and certainly more temporary and anonymous than the calendaring app, but it's limited to one event only. Something better is needed.</p>

<p>I've tried a few reminder apps but never really been pleased with them. The closest I've come to one I like is <a href="http://web.sabi.net/nriley/software/#pester">Pester</a>. It comes really close, but I find it lacking for my needs. It's too cumbersome to enter events (although the author obviously put effort into streamlining it—I just don't need all those options). I need something lightning fast and completely keyboard-based, or I won't bother. Too many unnecessary keystrokes to enter an event in Pester. The reminders are annoying window and/or voice. Voice is ok, but too easy to miss (if away from the computer for a moment, or the music is up too loud, or if the volume is muted or too low). Annoying reminders are too annoying—I don't want an important thought in the zone interrupted by an annoying reminder that insists on being attended to before I can return to working in the window I was using. (If I tab away from the annoying reminder it will stay hidden below my windows indefinitely and won't do its job).</p>

<p>Enter Crème Rappel. The little reminder app with a silly French name. Crème combines the notification power of <a href="http://growl.info/">Growl</a>, the scheduling prowess of <code>at</code>, and a no-frills quick-entry command-line UI. <em>Voyez</em>:</p>

<p><img src="/src/creme/synopsis.png" alt="Synopsis"/></p>

<p>The growl notifications are sticky, so you have to acknowledge them before they go away. But they're not annoying; you can continue to work on that thought until you have a few cycles to spare. They won't get hidden behind other windows. You can configure Growl to play a sound whenever a Crème Rappel notification happens. What you can't hear in the screenshot above is that the text of the window is also spoken using <code>say</code>, so even if you're not looking you'll get reminded. The only thing that's missing I think is a snooze button, so it can go away and taunt you a second time. If anyone has any ideas…</p>

<p>The requirements are Growl, of course, <code>growlnotify</code> which is distributed with Growl in the Extras folder, and configuring your mac to pay attention to the <code>at</code> queue. If you need help with the latter, see my <a href="http://hans.fugal.net/blog/articles/2008/02/13/atd-on-a-mac">previous post</a> on the matter. Crème Rappel is waiting for you to <a href="/src/creme/">download it</a>. Do not disappoint.</p>

<p>Here's how I use it in my life. Every morning I have a little planning session with my own self. I look at my calendar, figure out what I need to do and where I need to be. I set up my reminders, it looks something like this:</p>

<pre><code>$ creme
1325 teach lab
job 44 at Fri Feb 15 13:25:00 2008
1642 bus
job 45 at Fri Feb 15 16:42:00 2008
^D
</code></pre>

<p>Now my mind is clear of remembering that stuff, as long as I'm by my laptop. Throughout the day, if I need to remember something say 15 minutes in the future, I do something like this:</p>

<pre><code>$ creme +15minutes stretch my legs
</code></pre>

<p>Or more likely, I enter the time directly, since that's less typing. (One day I'd like to make this a real application with much nicer time parsing than what <code>at</code> handles. I should be able to type <code>+15m</code>, not have to type <code>+15minutes</code>. But this is the simplest thing that can possibly work, so it's good enough for now.)</p>

<p>For more details on using Crème Rappel, run <code>creme -h</code>. To configure it for your own needs, just hack at the script. If you think up a really neat enhancement, please let me know.</p>

<p>Oh, and if you like the idea but you use Linux, take a look at modifying the script to use <a href="http://www.mumbles-project.org/">Mumbles</a>. Theoretically you should be able to do it easily, but I wasn't overly impressed with the manpage to the mumbles command-line event generator (in particular, I didn't see a way to make it sticky, nor to set the icon but that's just bells and whistles). Oh, and don't forget to make sure the frequency with which at jobs are run is enough for your needs. If you get something that works, please send it to me and I'll try to incorporate it into the same body of work.</p>
