---
layout: post
status: publish
published: true
title: Which version of glibc?
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 51
wordpress_url: urn:uuid:2edd01d3-feb1-46ed-95b7-b2c36b3af912
date: '2005-03-21 10:24:53.000000000 -08:00'
tags:
- linux
comments: []
---
<p>I get asked this ridiculous question at least once a month at work, due to the
proprietary software that we use. I'm tired of googling for the answer, which I
can never remember, so here it is:</p>

<pre><code>#include &lt;stdio.h&gt;
#include &lt;gnu/libc-version.h&gt;
int main (void) { puts (gnu_get_libc_version ()); return 0; }
</code></pre>
