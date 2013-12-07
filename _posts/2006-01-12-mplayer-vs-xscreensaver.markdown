---
layout: post
status: publish
published: true
title: MPlayer vs. XScreensaver
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 59
wordpress_url: urn:uuid:c786bfb6-6c7d-4293-b722-244b5807c12a
date: '2006-01-12 19:29:56.000000000 -08:00'
tags:
- linux
comments: []
---
<p>Are you sick of the screensaver kicking in at all the wrong times while
watching a video with mplayer in full screen? The mouse doesn't work. The
now-not-fullscreen window is all distorted. Sometimes the keyboard is
unresponsive until you type the magic incantation (hint: alt-tab). Well I'd had
enough.</p>

<p>Just to show how lazy I was, the answer is right in the manpage. You just need
to specify the <code>-stop-xscreensaver</code> option. But that's a pain, so what you
really want to do is this:</p>

<pre><code>mkdir -p ~/.mplayer
echo "stop-xscreensaver=yes" &gt;&gt; ~/.mplayer/config
</code></pre>
