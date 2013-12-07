---
layout: post
status: publish
published: true
title: Code Reading on a Kindle
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1288
wordpress_url: http://hans.fugal.net/blog/?p=1288
date: 2012-06-06 04:05:11.000000000 -07:00
tags:
- linux
- mac
- pdf
- code
- script
- kindle
- ebook
- source
- enscript
- postscript
comments:
- id: 2662
  author: Levi
  author_email: levipearson@gmail.com
  author_url: ''
  date: '2012-06-06 08:28:29 -0700'
  date_gmt: '2012-06-06 08:28:29 -0700'
  content: I love reading books on the Kindle, but for me its usefulness pretty much
    ends beyond novels. It's just too hard to do anything non-linear and anything
    with non-trivial layout needs gets mangled. I do tech stuff and reference books
    on my iPad now, which I like less than the Kindle for novels, but way more for
    other kinds of books/magazines.
---
First, add this to your <tt>~/.enscriptrc</tt> file:
<code>
Media:  kindle 498 612 0 0 498 612
</code>

Now, here's a script (I call it <tt>kindlecode</tt>) to generate a pdf on stdout:
<code>
#!/bin/bash
enscript -Mkindle -E -p- "$@" | ps2pdf - -
</code>

Usage is something like this:
<code>
$ kindlecode *.{c,h} > /Volumes/Kindle/documents/foo.pdf
</code>

<img src="/kindlecode.jpg" alt="kindlecode in real life" />
