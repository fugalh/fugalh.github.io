---
layout: post
status: publish
published: true
title: Bash and the non-printing characters fiasco
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 890
wordpress_url: urn:uuid:29e6d618-5ec8-4450-86b4-f2cb2e8e2bca
date: 2007-10-30 09:44:00.000000000 -07:00
tags:
- linux
- mac
- bash
comments:
- id: 2701
  author: Jeroen
  author_email: fly.jdv@gmail.com
  author_url: ''
  date: '2012-11-28 09:29:37 -0800'
  date_gmt: '2012-11-28 09:29:37 -0800'
  content: "My personal work a round is to include a newline at the end of my prompt.\r\n\r\nPS1=\"
    \\n\\$\""
---
<p>Once upon a time, <a href="http://www.gnu.org/software/bash/">bash</a> (or some other shell) introduced color in the shell prompt. The syntax was funky and all but illegible, so manpages and HOWTOs were written. The technical elite (i.e. high school kids and sysadmins with nothing better to do than configure their bash prompts) rejoiced.</p>

<p>Once upon a more recent time, I crafted this bash prompt:</p>

<pre><code>PS1='$(r=$?; [ 0 == $r ] || echo "\[\e[33m\]$r\[\e[0m\] ")\u@\h:\w\n\[\e[32m\]\$\[\e[0m\] '
</code></pre>

<p>Actually, its history is more of an evolution than a crafting, but nonetheless
I like it. </p>

<p>Then, out of the blue, someone broke bash. The <code>\[</code> and <code>\]</code> non-printing character delimiters stopped working (or stopped working properly). Their purpose is to tell bash that the stuff inside is non-printing so don't count it when you're counting the number of characters in the prompt. This is vital for proper wrapping and tab completion in the presence of color escape sequences. I don't know who broke it or why, but removing <code>\[</code> and <code>\]</code> seemed to fix the symptom. </p>

<p>Fast forward far too long, and someone fixed the problem. Once again you needed <code>\[</code> and <code>\]</code>.</p>

<p>Fast forward again, and it's broken. Or maybe we're just going around in circles on which version of bash is being used in various distributions and OS's. In this case, Ubuntu is still (or again) broken and OS X is broken in a different way. They're both running 3.2.x. The bug is probably the same and the manifestation is simply different.</p>

<p>The current manifestation of this bug is that neither with nor without the delimiters works. I'm forced to go back to a noncolored prompt, and I'm not happy about it. This bug has been around for at least a year. I've reported it several times to various distros. Why is it not yet fixed? If they fixed it today, we'd still be battling the bug for years to come because of the many distros and OS's that have assumed buggy versions of bash.</p>
