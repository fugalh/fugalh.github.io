---
layout: post
status: publish
published: true
title: LaTeX Search Path
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 892
wordpress_url: urn:uuid:2830b6af-ac1b-405c-9e0a-6e1a6f324b85
date: 2007-11-01 10:55:26.000000000 -07:00
tags:
- mac
- latex
- bibtex
- path
comments:
- id: 1633
  author: Chris Conway
  author_email: ''
  author_url: http://procrastiblog.blogspot.com
  date: '2007-11-09 11:30:01 -0800'
  date_gmt: ''
  content: <p>Nice tip. Do you know if there is a way to add a directory to the LaTeX
    search path dynamically? I.e., inside a .tex file?</p>
- id: 1634
  author: Edwin Rijpkema
  author_email: ''
  author_url: ''
  date: '2007-11-15 04:38:53 -0800'
  date_gmt: ''
  content: |-
    <p>Have you used the TEXINPUTS environment variable?</p>

    <p>see <a href="http://myitcv.org.uk/latex/tips_and_tricks.html#answer9" rel="nofollow">http://myitcv.org.uk/latex/tips_and_tricks.html#answer9</a></p>

    <p>I put all my figures in a the subdirectory    figures of my project. So, I put the following in my .bashrc file:</p>

    <pre><code>export TEXINPUTS=".:./figures:"
    </code></pre>

    <p>This worked for me.</p>
- id: 1635
  author: Jeff Logan
  author_email: ''
  author_url: ''
  date: '2007-11-26 13:23:23 -0800'
  date_gmt: ''
  content: <p>Thank you Edwin, this saved me a lot of trouble :)</p>
- id: 2690
  author: Ron
  author_email: ''
  author_url: ''
  date: '2012-09-18 12:09:48 -0700'
  date_gmt: '2012-09-18 12:09:48 -0700'
  content: "Try \r\n\r\nkpsepath tex\r\n\r\nto see the whole search path"
---
<p>I recently had need to put a <code>.bst</code> file in my LaTeX search path. This turned out to be difficult to search for. I found a lot of pages and style files telling users to put such and such file in their LaTeX search path. I began to wonder if I was the only LaTeX user on earth who had no idea what the LaTeX search path was.</p>

<p>With some effort I found that the global path's root is usually something like <code>/usr/share/texmf</code>. I'm not interested in putting it in the global path though. We have home directories for a reason here.</p>

<p>Finally I found the answer, with some creative googling. The answer depends on your distribution/OS. Apparently on Debian it's <code>~/.texmf-config</code> (untested). The MacTeX distribution (which I have installed) looks in <code>~/Library/texmf</code>. The macports build (don't ask) looks in <code>~/texmf</code>, which I learned only by trial and error. My guess is that latter answer is the answer if you build by yourself, and so might be a good initial guess no matter what the distribution.</p>

<p>So, I did this:</p>

<pre><code>mkdir -p ~/Library/texmf/bibtex/bst
ln -s ~/Library/texmf ~/texmf
mv acm-annotated.bst ~/texmf/bibtex/bst
</code></pre>
