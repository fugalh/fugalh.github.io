---
layout: post
status: publish
published: true
title: My favorite bash idiom
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1207
wordpress_url: http://hans.fugal.net/blog/?p=1207
date: 2010-03-09 21:30:08.000000000 -08:00
tags:
- bash
- shell
- ffmpeg
- sh
- find
- while
- read
- newline
- print0
- stdin
- xargs
comments:
- id: 2306
  author: gerry
  author_email: jabjuix0@gmail.com
  author_url: ''
  date: '2010-10-08 05:26:31 -0700'
  date_gmt: '2010-10-08 05:26:31 -0700'
  content: "Okay I stoop to idioms myself in zsh\r\n\r\nfor a in **/*.mp3\r\n   ffmpeg
    -i \"$a\" \"$a:r.m4a\"\r\n\r\nand spaces and newlines just work\r\n\r\nzsh means
    you don't usually need find:\r\nAll zero length files -- recursively\r\nls **/*(L0)\r\n\r\nAll
    files modified in the last 3 hours:\r\nls -d **/*(ch-3)\r\n\r\nAll files not directories
    in reverse time order:\r\nls -lrt **/*(^/)\r\n\r\nGrrrr. dump bash.\r\n[grin]"
---
Stuart and I came up with a refinement to my favorite bash idiom today. It was:

<code>find ... | while read FOO; do ...; done</code>

as demonstrated in:

<pre><code>find . -name '*.mp3' -type f | while read MP3; do
    ffmpeg -i $MP3 ${MP3%.mp3}.m4a
done</code></pre>

This handles whitespace (except newlines) in filenames. Except that ffmpeg is sharing stdin with while, which can cause some very funky problems. This is safer:

<pre><code>find ... | while read FOO; do echo | (
    ...
); done</code></pre>

and while you're at it, you might as well take into account the unlikely-but-possible corner case of a filename containing a newline:

<pre><code>find ... -print0 | while read -d $'\0' FOO; do echo | (
    ...
); done</code></pre>
