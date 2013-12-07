---
layout: post
status: publish
published: true
title: Markdown Makefile Idiom
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 977
wordpress_url: urn:uuid:7030e3df-10ab-4f0c-b8a3-de8016404765
date: 2008-06-16 15:35:09.000000000 -07:00
tags:
- make
- markdown
- makefile
- patsubst
- wildcard
comments: []
---
<p>I can never remember this, and I use it frequently, so I thought I'd put it here where I can find it faster.</p>

<pre><code>all: $(patsubst %.txt,%.html,$(wildcard *.txt))
%.html: %.txt header.html footer.html
    cat header.html &gt; $@
    markdown $&lt; &gt;&gt; $@
    cat footer.html &gt;&gt; $@
</code></pre>
