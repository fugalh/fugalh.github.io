---
layout: post
status: publish
published: true
title: XScreensaver copout workaround
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 662
wordpress_url: urn:uuid:4e66c80a-0b5f-4d97-a9fd-aa8ec4344193
date: '2006-07-07 00:22:00.000000000 -07:00'
tags:
- linux
- xscreensaver
- bash
- trap
comments: []
---
<p><a href="http://www.jwz.org/xscreensaver/faq.html#dvd">This FAQ answer</a> is the most
moronic thing I have ever heard. </p>

<blockquote>
    <p>When you want to watch a movie, fire up xscreensaver-demo and select Mode:
    Disable Screen Saver from the option menu, which means not to blank the
    screen at all. When you're done watching the movie, re-select your previous
    mode.</p>

    <p>That's kind of lame, I know. You should ask the author of the DVD-playing
    software you are using to add explicit support for xscreensaver to their
    program. </p>
</blockquote>

<p>So let's get this straight, you want everyone who might write a program that
shouldn't be interrupted by the stupid screensaver to implement
xscreensaver-specific logic to keep the screensaver from coming on, and you
don't want to give us end users an easy way to turn it on or off in a script.
IDIOT!!</p>

<p>Oh it gets better. He then goes on to explain how developers should "add
explicit support for xscreensaver". They should set up <em>another thread</em> to
periodically make a system call, e.g.:</p>

<pre><code>if (playing &amp;&amp; !paused) {
    system ("xscreensaver-command -deactivate &gt;&amp;- 2&gt;&amp;- &amp;");
}
</code></pre>

<p>I'm utterly amazed at the idiocy. But let it not be said that I rant without
action:</p>

<pre><code>#!/bin/sh
(
while true; do
    sleep 60
    xscreensaver-command -deactivate &amp;&gt;/dev/null
done
)&amp;
trap "echo 'Reenabling XScreensaver (IDIOT!!)'; kill $!" 0

xmess nes -cart ~/games/mario.nes
</code></pre>

<p>If you're ambitious, you could write a generic wrapper program inspired by
<code>sudo</code> or <code>openvt</code>.</p>
