---
layout: post
status: publish
published: true
title: Tailor, Mercurial, Leopard
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 914
wordpress_url: urn:uuid:4c78f99d-c1db-4664-bafb-5b3698188e08
date: '2007-12-15 09:24:00.000000000 -08:00'
tags:
- python
- hg
- mercurial
- tailor
comments: []
---
<p>I was getting this error when trying to use Tailor with Mercurial on Leopard:</p>

<pre><code>Common base for tailor exceptions: 'hg' is not a known VCS kind: No module named mercurial
</code></pre>

<p>Mercurial was installed, so the error mystified me. Turns out to be a problem
with python versions in use. Leopard's python is version 2.5.1, but mercurial
from MacPorts depends on python 2.4, and so MacPorts installs python24. So when
running tailor with python 2.5 and trying to load the mercurial module which is
installed for 2.4, not 2.5, it naturally fails. The workaround is to run tailor
with python 2.4 instead, which works fine.</p>

<pre><code>#! /bin/sh
# Save as ~/bin/tailor and chmod +x
tailor=$HOME/src/tailor/tailor
exec python2.4 $tailor
</code></pre>
