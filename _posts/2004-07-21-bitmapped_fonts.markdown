---
layout: post
status: publish
published: true
title: Terminus in GTK2 Applications
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 40
wordpress_url: urn:uuid:1dadbbc7-2819-4551-901c-d19162b90ca0
date: 2004-07-21 10:12:26.000000000 -07:00
tags:
- linux
comments: []
---
<p>I'm a big fan of the <a href="http://www.is-vn.bg/hamster/jimmy-en.html">Terminus
font</a>, and an even bigger fan of
<a href="http://www.vim.org/">Vim</a>. Recent versions of Vim Debian packages are built
with GTK2 instead of GTK1. GTK2 apps use TrueType fonts and in general make
fonts in X even more complicated than they already were. I must have my
terminus while in gvim, and it just wasn't there by default. Here's the trick:</p>

<pre><code>$ dpkg-reconfigure fontconfig  # answer yes to "Use Bitmapped fonts by default"
</code></pre>
