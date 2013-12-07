---
layout: post
status: publish
published: true
title: Filter stderr
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1001
wordpress_url: urn:uuid:c3410372-1053-4bcf-bdea-653aa7cc5e4e
date: 2008-08-25 22:19:36.000000000 -07:00
tags:
- bash
- pipe
- stderr
- filter
- gdc
- d
comments: []
---
<p>I've been exploring <a href="http://www.digitalmars.com/d/">D</a> the language. I really do like it, but that's another post. There are a couple of D compilers, but the only viable option on OS X seems to be <a href="http://dgcc.sourceforge.net/">gdc</a>. I installed it via <a href="http://macports.org">MacPorts</a>. On Leopard, gdc generates assembly that makes the FSF gcc complain "<code>indirect jmp without `*'</code>" over and over. The bug is <a href="http://trac.macports.org/ticket/15075">known</a>, and other than being annoying it seems harmless.</p>

<p>So I decided what I needed was a script that would filter out these frivolous warnings without otherwise affecting stderr, and also without changing the exit status (so make can do the right thing). This turned out to be easier said than done. Finally I stumbled on the right incantation:</p>

<pre><code>#! /bin/bash
gdc=/opt/local/bin/gdc
msg="indirect jmp without"
$gdc "$@" 2&gt; &gt;(grep -v "$msg" 1&gt;&amp;2)
</code></pre>

<p>We redirect stderr to the named pipe corresponding to that subshell (see "Process Substitution" in the bash manpage), then we redirect grep's output to its stderr. Because grep is in a subshell, its exit status doesn't mess up the exit status of the script, which is the exit status of gdc, as it should be.</p>
