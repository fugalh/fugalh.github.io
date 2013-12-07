---
layout: post
status: publish
published: true
title: Pasting Panacea
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 645
wordpress_url: urn:uuid:1e2b6cb3-fee9-4fc2-ab2d-3f5ae31eb7bc
date: 2006-06-29 12:02:23.000000000 -07:00
tags:
- osx
- automation
- paste
comments: []
---
<p><a href="http://pastie.caboo.se/">Pastie</a> is the paste site I've been waiting for.
Simple, elegant, useful, fast. Now, I've gone a step further and
(<a href="http://pastie.caboo.se/paste/584">re</a>)written a shell script to paste from
stdin and give you the URL:</p>

<pre><code>#!/bin/sh
curl http://pastie.caboo.se/pastes/create \
-H "Expect:" \
-F "paste[parser]=plaintext" \
-F "paste[body]=&lt;-" \
-s -L -o /dev/null -w "%{url_effective}")
</code></pre>

<p>But that wasn't far enough. I went one step further and made an OS X Automator
workflow to take what's on the clipboard, paste it to pastie, and put the
resulting URL on the clipboard. Throw
<a href="http://hans.fugal.net/src/Pastie.dmg"><code>Pastie.app</code></a> in <code>~/Applications</code> and
you can use <a href="http://quicksilver.blacktree.com/">Quicksilver</a> for the perfect
instant pasting panacea.</p>
