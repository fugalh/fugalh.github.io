---
layout: post
status: publish
published: true
title: LilyPond on Leopard
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 937
wordpress_url: urn:uuid:e384889b-45c8-4117-8f74-f234c5e9fbb5
date: '2008-02-27 11:44:11.000000000 -08:00'
tags:
- mac
- music
- leopard
- lilypond
- notation
comments:
- id: 1718
  author: Ajit
  author_email: aishwarya_aishwaryaa@yahoo.com
  author_url: http://www.correcty.org
  date: '2008-02-28 05:50:15 -0800'
  date_gmt: ''
  content: <p>I love and very much enjoy using LilyPond. It has much flexibility that
    I get to play around with my tunes.</p>
- id: 1719
  author: Niko Maly
  author_email: niko@fsmat.at
  author_url: ''
  date: '2008-05-25 02:45:54 -0700'
  date_gmt: ''
  content: |-
    <p>Hi Hans,
    I work on a Java program to generate jazz chords. The output is a Lilypond file.
    Well, I manage to open/compile the *.ly file from the shell (i.e. the way you describe), but I don't manage it to do this from inside the Java program using the Runtime class. (Although I am able to execute other applications...?)
    I started working on a Mac/Leopard recently, so I am not very familiar with the shell commands and setting the paths, etc.</p>

    <p>I would appreciate it, if you have any idea to help me,</p>

    <p>thanks </p>

    <p>Niko Maly</p>
- id: 1720
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-05-26 19:47:11 -0700'
  date_gmt: ''
  content: <p>I'm sorry I am no help to you. I'm not familiar with doing this in Java.
    I bet the issue has to do with setting up the environment correctly, though.</p>
- id: 1897
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-03-09 19:20:23 -0700'
  date_gmt: '2009-03-09 19:20:23 -0700'
  content: 'Correction: why it takes forever the first time isn''t Rosetta (does it
    with an Intel download too). Whatever it is, it does eventually finish and thereafter
    runs quickly.'
---
<p>For my musical notation needs, I use <a href="http://lilypond.org/">LilyPond</a>. </p>

<p>LilyPond is to music as LaTeX is to writing. I prefer to edit LilyPond files in <a href="http://vim.org/">Vim</a> and compile them with <code>lilypond</code> at the command line. However, on OS X LilyPond.app is a front end to the compiler. An IDE of sorts. Not a spectacular one, in my opinion, but it does have one thing going for it: when you click on a note in the PDF preview, it takes you that note in your LilyPond source file in the IDE.</p>

<p>On Leopard, LilyPond is severely broken. The IDE will "start", but there is no menu. Further, if you are on Intel, when you try to run it at the command line, it just keels over and does nothing. It so happens that the workaround to this problem and using LilyPond without the IDE are almost identical solutions, so I'll describe them as one and the same.</p>

<p>First, and this is the only difference between Leopard brokenness and just wanting to run on the command-line, you want the powerpc version of LilyPond.app, not the Intel version. So go over to the <a href="http://lilypond.org/web/install/">download page</a> and get the ppc version (the one that says it's for G3, G4, G5 Macs).</p>

<p><code>lilypond</code> and its friends are in <code>Lilypond.app/Contents/Resources/bin</code>. You could add this to your <code>PATH</code>, but some of the binaries in there are things that I have installed elsewhere (e.g. with <a href="http://macports.org">MacPorts</a>), and I don't want them overriding my <code>PATH</code>. Likewise, I want <code>lilypond</code> to be able to find the binaries it expects, and since they're taking up disk space anyway let's help it along. So I wrote a script. A LilyPond launcher if you will. I call it <code>ly</code> and put it in my path, and then I call e.g. <code>ly lilypond foo.ly</code>. Here's the code:</p>

<pre><code>#! /bin/sh
APP=/Applications/LilyPond.app
PATH=$APP/Contents/Resources/bin:$PATH
exec "$@"
</code></pre>

<p>Customize <code>APP</code> to point wherever you want to keep LilyPond.app. This will load up the environment that will give <code>lilypond</code> the best chance of success. You can run any of the binaries in that directory with <code>ly</code>, but the most common case is to run <code>lilypond</code>. So I recommend putting this in your <code>.bashrc</code>:</p>

<pre><code>alias lilypond='ly lilypond'
</code></pre>

<p>The first time you run the ppc version of LilyPond, or anything else, on an Intel machine, it will seem to take forever while Rosetta fires up. Be patient. Subsequent invocations are quick enough.</p>
