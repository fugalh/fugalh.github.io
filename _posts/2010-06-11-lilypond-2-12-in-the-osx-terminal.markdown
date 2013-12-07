---
layout: post
status: publish
published: true
title: Lilypond 2.12 in the OSX Terminal
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1218
wordpress_url: http://hans.fugal.net/blog/?p=1218
date: 2010-06-11 17:38:13.000000000 -07:00
tags:
- osx
- terminal
- lilypond
comments: []
---
Getting this error?

<pre><code>$ /Applications/LilyPond.app/Contents/Resources/bin/lilypond
dyld: Library not loaded: @executable_path/../lib//libstdc++.6.dylib
  Referenced from: /Applications/LilyPond.app/Contents/Resources/bin/./lilypond
  Reason: image not found
Trace/BPT trap</code></pre>

I don't know why this is screwed up, but I have a workaround:

<pre><code>ln -s /usr/lib/libstdc++.6.dylib /Applications/LilyPond.app/Contents/Resources/lib</code></pre>

While I'm at it, here's my script in <code>~/bin</code>:

<pre><code>$ cat ~/bin/lilypond
#! /bin/bash
exec /Applications/LilyPond.app/Contents/Resources/bin/$(basename "$0") "$@"</code></pre>

You can symlink it to <code>midi2ly</code> or whatever other executables you want to execute. Or you could add that directory to your path, of course.
