---
layout: post
status: publish
published: true
title: gvim on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 796
wordpress_url: urn:uuid:088bd92b-459f-47b4-ae94-46e259790961
date: 2007-02-18 18:18:00.000000000 -08:00
tags:
- mac
- osx
- vim
- gvim
- fonts
comments:
- id: 1560
  author: Kenyon Ralph
  author_email: ''
  author_url: http://kenyonralph.com/
  date: '2008-12-11 16:46:41 -0800'
  date_gmt: ''
  content: '<p>This macvim is much better: <a href="http://code.google.com/p/macvim/"
    rel="nofollow">http://code.google.com/p/macvim/</a></p>'
- id: 1561
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-12-12 08:39:57 -0800'
  date_gmt: ''
  content: <p>Indeed it is, it makes this post obsolte. It didn't exist when I wrote
    this. </p>
---
<p>In spite of being the author of one of the more (in)famous vim color schemes,
<a href="http://www.vim.org/scripts/script.php?script_id=105">desert.vim</a>, I have been
vimming primarily in the console for quite some time now. The primary reason is
that gvim on OS X sucks. </p>

<p>Still, it's nice to have gvim working for various reasons. One of the more
important reasons is dragging stuff to the Vim icon on the dock. </p>

<p>As a follow-up to my post on unicode in the terminal, I decided to install the latest Vim.app from <a href="http://www.macvim.org/OSX">macvim.org</a> and see how it handled unicode. It didn't handle it very well, but it's only a few settings away.</p>

<p>First, there's the issue of font. I don't like Monaco very much. I use
<a href="http://www.ms-studio.com/FontSales/anonymous.html">Anonymous</a> for the terminal
and I think it is an excellent font. In fact, I find myself likeing Anonymous
just as much as <a href="http://www.is-vn.bg/hamster/jimmy-en.html">Terminus</a>, but it
has the added advantage of being TrueType and looking great with antialiasing.
Unfortunately, in Vim at least it looks terrible <em>without</em> antialiasing. So I
got the <a href="http://fractal.csie.org/~eric/wiki/Terminus_font">pseudo-TrueType Terminus
font</a> by Eric Cheng. It took
some fiddling, because of various Bad Things™ happening with Vim and OS X
dealing with a TrueType-wrapped bitmap font, but I found the following settings
work great (put them in <code>~/.gvimrc</code>):</p>

<pre><code>set enc=utf-8
set macatsui noanti gfn=Terminus:h12
</code></pre>

<p>It's not antialiased, but it is Terminus and it handles Unicode just fine (as
far as the Terminus font itself does, which is pretty good).</p>

<p>You can use antialiased fonts, e.g. Anonymous, with the following <code>.gvimrc</code>:</p>

<pre><code>set enc=utf-8
set nomacatsui anti termencoding=macroman gfn=Anonymous:h10
</code></pre>

<p>but Bad Things™ happen when you use Unicode, so I'm sticking with the Terminus setup.</p>
