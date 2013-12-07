---
layout: post
status: publish
published: true
title: Identification in PDFs
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1087
wordpress_url: http://hans.fugal.net/blog/2009/02/04/identification-in-pdfs
date: '2009-02-04 16:21:38.000000000 -08:00'
tags:
- review
- gnuplot
- pdf
- latex
- publish
- paper
- pdftex
- identity
- anonymous
- blind
comments:
- id: 2017
  author: Anonymous pdf &laquo; Code and Culture
  author_email: ''
  author_url: http://codeandculture.wordpress.com/2009/06/04/anonymous-pdf/
  date: '2009-06-04 19:59:50 -0700'
  date_gmt: '2009-06-04 19:59:50 -0700'
  content: '[...] If you want to double check that it worked you can use this procedure
    to search the meta-text of a pdf. [...]'
---
<p>If you need to create a PDF with no embedded identification it may not be enough to simply refrain from typing your name. For example:</p>

<pre><code>$ strings foo.pdf | egrep -i '(hans|fugal)'
/PTEX.FileName (./0_Users_fugalh_research_foo_fig1.pdf)
/Author (Hans Fugal)
/PTEX.FileName (./1_Users_fugalh_research_foo_fig2.pdf)
/Author (Hans Fugal)
/PTEX.FileName (./2_Users_fugalh_research_foo_fig3.pdf)
/Author (Hans Fugal)
/PTEX.FileName (./3_Users_fugalh_research_foo_fig4.pdf)
/Author (Hans Fugal)
/PTEX.FileName (./4_Users_fugalh_research_foo_fig5.pdf)
/Author (Hans Fugal)
</code></pre>

<p>The <code>/PTEX</code> lines are from pdftex and the <code>/Author</code> lines originated from gnuplot</p>

<pre><code>/Title (fig1.pdf)
/Author (Hans Fugal)
/Creator (gnuplot 4.2 patchlevel 4 )
</code></pre>

<p>Removing the offending lines didn't hurt the PDF in this situation. So if you must anonymize a PDF (e.g. to submit a paper for blind review), be sure to check for hidden identification. Of course, most reviewers wouldn't go digging for it, but you will rest easy knowing it's truly anonymous.</p>
