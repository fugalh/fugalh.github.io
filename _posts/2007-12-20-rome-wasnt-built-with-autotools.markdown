---
layout: post
status: publish
published: true
title: Rome wasn't Built with Autotools
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 916
wordpress_url: urn:uuid:ea96024a-5258-4a7e-9c81-e7eca7827d27
date: 2007-12-20 20:54:05.000000000 -08:00
tags:
- build
- make
- cmake
- scons
- rake
- autoconf
- automake
- autotools
comments:
- id: 1674
  author: Kevin
  author_email: email.ber@gmail.com
  author_url: ''
  date: '2007-12-21 22:51:05 -0800'
  date_gmt: ''
  content: |-
    <p>Amen! </p>

    <p>I have the same view on all your points. A couple other thinks I hate is when I do compile something I'd like to know what and where things get installed. Just in case, I dunno, I want to remove it. But most things instead of showing me a nice little "here's what went where" when I say make install, instead give me about a thousand lines of completely useless info.</p>

    <p>Along the same lines, with 'make install' there's also a 'make uninstall'. If that was available I wouldn't need to know the above info. But almost nobody bothers to have an uninstall target.</p>

    <p>-Kevin-</p>
- id: 1675
  author: Agrouf
  author_email: ''
  author_url: ''
  date: '2008-02-02 05:49:44 -0800'
  date_gmt: ''
  content: |-
    <p>On small projects, configure is longer to execute than make!
    My project need something like autotools, but it is making me crazy. I used mkproject to have a template, and then I hacked, trying to figure out or guessing how to do simple things. Man, how hard it is to install something in /etc!
    I hope autotools find a replacement soon.</p>
- id: 1676
  author: Wynand Winterbach
  author_email: wynand.winterbach@gmail.com
  author_url: ''
  date: '2008-02-09 10:54:53 -0800'
  date_gmt: ''
  content: |-
    <p>I was forced to learn CMake, because I had* to use the Visual C++ compiler for a project under Windows (it uses Autotools under Unix).</p>

    <p>The documentation for CMake isn't awful, but it isn't great either. Despite this, I didn't struggle too much.</p>

    <p>CMake works exactly as advertised, which is nice. My config files are also quite short.</p>

    <p>My main gripe with CMake is that its syntax seems as if it was designed to be parsed by the C pre-processor and that it's hard to debug the make files. However, this is also true for Autotools and my CMake files were quite short.</p>

    <ul>
    <li>The project uses Unicode and neither Cygwin nor Mingw has wide character support. I suppose I could have found a way to use the Visual C++ compiler with Autotools, but I just didn't feel like it.</li>
    </ul>
---
<p>I hate autotools (autoconf, automake, and friends). I hate them with a <em>passion</em>! Unfortunately, the only thing worse than a project using autotools is a project not using autotools.</p>

<p>As a user, I love the simplicity that autotools promises, and <em>sometimes</em> delivers:</p>

<pre><code>./configure
make
sudo make install
</code></pre>

<p>When it works, it's a beautiful thing. When it doesn't, it's deep voodoo to fix. This is doubly true when you're not using Linux.</p>

<p>As a developer... well let's face it. Very few developers know the first thing about using autotools. Of those that do, almost none know more than the very basics necessary to copy, paste, and hack someone else's autotools setup to mostly-successfully build their project. Developers who write elegant DRY code and would never even consider the cut, paste, and hack approach to software development, will lose all resolve when faced with learning autotools. </p>

<p>The result is sloppy, bloated, unintelligible <code>configure.{ac,in}</code> and <code>Makefile.am</code> files. <code>./configure</code> scripts that take longer performing pointless and repetitive tests, than it takes to build the project. Even on big projects, most configure scripts are many orders of magnitude slower than they need to be, because they check everything under the sun—decades of copy, paste, and hack cruft.  I recently went through <a href="http://www.seul.org/docs/autotut/">a decent tutorial on autotools</a> and made me a simple autotools setup from scratch for a simple toy project. <code>./configure</code> took all of 3 seconds to run.</p>

<p>Clearly we need something like autotools. We need something to do the following mundane tasks automatically:</p>

<ul>
<li>Figure out if the dependencies are installed and what compiler flags we need to access them.</li>
<li>Figure out the compilation, installation, etc. commands and flags.</li>
<li>Construct a nice Makefile with the expected targets (install, clean, etc.)</li>
<li>Allow the user to <em>easily</em> override and give hints.</li>
</ul>

<p>So what is so hard about this? I can see why autotools turned out the way it did; it was written in shell and m4, in the dark ages, without the benefit of 20/20 hindsight, and has accumulated decades of cruft. The truly amazing thing is that autotools has done so well and is so popular—that's a testament to something fundamentally right about autotools. So fundamentally right that in spite of all its warts it continues to be the premier build system.</p>

<p>There are contenders to replace it. Scons and CMake seem to be the leaders in this arena. I've used Scons on a large project (Ardour) and I wasn't impressed. You have to be fluent in Python to use it effectively, you have to approach your build system as a full-blown programming problem in a general purpose language (Python). It's quite slow, and you need Python installed to use it. It is very flexible, though. </p>

<p>CMake seems promising, but I was dismayed to see that its syntax is not much better than autotools, and the documentation is skimpy (unless you buy that book that's out of print until the next edition). Still, it's better documented than autotools, and the user experience is quite nice.</p>

<p>Will CMake rise to supremacy? With time, it may. I think there's room to undercut CMake though. I think one could design a tool that is flexible yet easy to use, fills the autotools niche solidly, and isn't all that complicated to boot. What do you think?</p>
