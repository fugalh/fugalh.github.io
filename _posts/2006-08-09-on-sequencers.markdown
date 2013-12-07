---
layout: post
status: publish
published: true
title: On Sequencers
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 700
wordpress_url: urn:uuid:03e8dafd-de73-4f36-bc74-a725eca04b3a
date: '2006-08-09 08:11:00.000000000 -07:00'
tags:
- audio
- music
- midi
- sequencer
- usability
comments:
- id: 1508
  author: zzzirk
  author_email: ''
  author_url: ''
  date: '2006-08-09 13:56:40 -0700'
  date_gmt: ''
  content: <p>I have had limited success with any of the Linux MIDI sequencers to
    date and would agree that they all seem to lack many features that seem to me
    to be of great importance.  I've never particularly cared for the idea of step
    recording in the first place.</p>
---
<p>I get the impression that most users of MIDI sequencers step record. At least,
the writers of the sequencers pay little attention to live recording. For
evidence, I cite the abundance of tracker sequencers available for Linux, and
the three major sequencers for Linux (IMHO) which all fall short in the
relatively simple task of accomodating people like me who prefer to record
things live: Rosegarden, Muse, and Seq24.</p>

<p>Live recording is not complicated. You need a few basic features, and you need
to make them accessible from the keyboard without touching the mouse. Here's an excellent UI model (that makes me drool):</p>

<p><a href="http://frontierdesign.com/Products/TranzPort"><img src="http://frontierdesign.com/media/lr/tranzport.jpg"
width="400" alt="Frontier Design Group's Tranzport" /></a></p>

<p>And here's a list of those basic features:</p>

<ul>
<li>FF, REW, Stop, Play, Record</li>
<li>Replace and overdub modes.</li>
<li>Punch</li>
<li>Loop</li>
<li>Metronome</li>
<li>Lead-in of 2, 1, or <em>0</em> measures. My old Roland JW-50 from 1992 did a great job with this. You had the option of no lead-in but you also had the option of key-triggered recording. That is, you press record, and the thing starts recording the moment you start playing. This is <em>extremely</em> useful.</li>
<li>Track muting and solo</li>
<li>16 tracks</li>
<li>Variable speed (percent of tempo) for slow and fast recording. </li>
<li>Undo</li>
</ul>

<p>That's it. Most sequencers have some or perhaps even most of these features,
but leave out essential aspects such as no mousing, replace recording, no
lead-in, and not crashing. Rosegarden goes a step further and makes the simple
things that you take for granted difficult as well (but it does everything else
under the sun and it's hard to justify not using it).</p>

<p>Seq24 is unique in its failure because it is oriented at realtime performance.
Note that word, "performance". It could perhaps just as easily be good at
realtime recording if it tried, and then in spite of its loop and pattern-based
approach it would still be an excellent sequencer for us non-pattern junkies.
(Sequence a Bach organ fugue in a tracker, I dare you.)</p>

<p>If I have the honor of speaking to someone who is writing or improving a
sequencer, please consider the keyboardists and take my thoughts into
consideration. Believe it or not, the lack of these basics will drive a
keyboardist crazy just as fast as mousing will drive a CLI junkie crazy. Which
is quite ironic as most step-recording Linux sequencer developers are probably
CLI junkies.</p>
