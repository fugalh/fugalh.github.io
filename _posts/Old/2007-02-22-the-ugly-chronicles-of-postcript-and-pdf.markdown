---
layout: post
status: publish
published: true
title: The Ugly Chronicles of Postcript and PDF
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 802
wordpress_url: urn:uuid:2ab83623-7e02-4d9e-a822-89e2efcb3cce
date: '2007-02-22 19:04:35.000000000 -08:00'
tags:
- cs
- pdf
- fonts
- ps
- ps2pdf
- pstopdf
- ugly
- Type 3
comments: []
---
<p><a href="http://lifeoflevi.com/blog/">Levi</a> and I tried to figure out the age-old question of how to get not-ugly PDFs out of troublesome PS files. This question used to be primarily "how do I get legible PDFs out of LaTeX?" That question has been answered and answered well, and in most setups of LaTeX it just works these days (in my experience). <a href="http://www.physics.ohio-state.edu/~yurh/doc/tex2pdf/">Here</a> is a good page on that subject.</p>

<p>The question now has become, how do I get legible PDFs out of PostScript files for which I do not have the <code>.dvi</code> or source files? The web is fairly silent on this point.</p>

<p>First, let's talk about the problem. The problem is bitmapped fonts. The beautiful Computer Modern fonts are (were) not vectorized fonts, but bitmapped fonts. That means, in a nutshell, they only look right at certain resolutions. When <code>ps2pdf</code> or its kin converts such a PostScript file to PDF, it generates a PDF file with <em>Type 3</em> fonts. I believe Type 3 fonts can be either vector or raster, but we're interested in the raster case. </p>

<p>Many many programs do a fantastically terrible job of rendering Type 3 fonts. This includes Adobe Acrobat (rumor has it newer versions are improved), OS X Preview, gv, and a whole slew of others. So what you get is a PDF that is fairly illegible on-screen but that prints fine. Some nice screenshots <a href="http://www.sciencemag.org/about/authors/prep/TeX_help/tex2pdf.dtl">here</a>.</p>

<p>This inability to cope with Type 3 fonts seems to be a matter of utter incompetence. If you know anything about image processing, you know that it would be hard <em>not</em> to do a better job of downsampling. There do seem to be programs capable of displaying PDFs with Type 3 fonts in at least an acceptable manner. On linux, xpdf and whatever GNOME's PDF viewer is called manage well enough. gv does not handle a PDF with Type 3 fonts well, however it handles the original PostScript file very well. On OS X, Preview fails miserably. You should be able to get xpdf from MacPorts, which is a valid option. Another option is to enhance the generated PDF to the point of moderate legibility:</p>

<pre><code>ps2pdf -dPDFSETTINGS=/screen -dGrayDownsampleType=2 foo.ps
</code></pre>

<p>That says downsample to screen resolution not printer resolution, and use
bicubic resampling instead of the fast and worthless default. Levi reports <a href="http://www.kiffe.com/macghostview.html">MacGhostView</a> ($20 shareware) works well too, but I can't get it to extract out of the sitx file for some reason. I tried <a href="http://www.pstill.com/">PStill</a> ($70) and got an absolutely pitiful output (and the UI sucks too).  Probably the best option is to use gv in X11 to view the original PostScript file, if you don't mind the interface (I actually am kind of fond of gv's interface). However my initial attempt at this with MacPorts doesn't seem to work - I get no fonts at all.</p>

<p>Hopefully this helps somebody. If you know anyone that is responsible for the abysmal state of things, whack him upside the head for me. If you ever generate a PostScript or PDF file from LaTeX with bitmapped fonts instead of vector fonts, whack <em>yourself</em> upside the head for me.</p>
