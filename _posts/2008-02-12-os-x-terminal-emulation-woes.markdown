---
layout: post
status: publish
published: true
title: OS X Terminal Emulation Woes
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 924
wordpress_url: urn:uuid:f81b5d7a-0749-4d9c-8a4d-c6ff6d0ed593
date: 2008-02-12 20:40:09.000000000 -08:00
tags:
- mac
- osx
- terminal
- xterm
- rxvt
- dtterm
- curses
- TERM
comments:
- id: 1687
  author: ./martijn
  author_email: ''
  author_url: ''
  date: '2008-02-12 22:57:48 -0800'
  date_gmt: ''
  content: <p>one of the annoyances that I experience is that it is not possible to
    set a remote hostname (and path) as a terminal/tab-title ..</p>
- id: 1688
  author: davel
  author_email: ''
  author_url: ''
  date: '2008-02-23 20:40:00 -0800'
  date_gmt: ''
  content: |-
    <p>Thanks! Debian loves this setup.
    Aptitude seems to need the "Delete sends Ctrl-H" flag, too.</p>
---
<p>OS X's Termina.app is the terminal I've been using since I switched to Leopard, because it has tabs now and it's beautiful. Oh, and <a href="http://iterm.sf.net">iTerm</a> gave me too much grief with odd, illogical and unpredictable bugs. </p>

<p>One of the drawbacks to Terminal.app is that it's broken. This is what Aptitude looks like with <code>TERM=xterm</code> (I think this is the default):</p>

<p><img src="/images/Terminal-xterm.png" alt="TERM=xterm"/></p>

<p>This is what it should look like:</p>

<p><img src="/images/Terminal-dtterm.png" alt="TERM=dtterm"/></p>

<p>How to get from there to here? The short answer is to choose <code>dtterm</code> as your terminal emulation (in Preferences, on the Advanced tab).</p>

<p>The long answer is that the problem here is that xterm supports this capability called back-color-erase (bce). If you tell programs that you are an xterm (with <code>TERM=xterm</code>), they will assume you support bce. The same goes for <code>rxvt</code> and <code>xterm-color</code> and even <code>vt100</code> (even though that one doesn't seem to support color). bce isn't the only problem, either. There's also redraw problems that are difficult to show with a screenshot.</p>

<p>Setting <code>TERM=dtterm</code> seems to get rid of at least the major breakage. It would seem that the actual capabilities of Terminal.app are closest to dtterm, or at least closer to dtterm than to xterm or rxvt. It solves all the issues I've been having with aptitude, mutt, and screen locally and on remote linux boxes. But there's a caveat—not all remote systems will have the dtterm entry in their terminfo databases. Ubuntu 7.10 didn't by default, for example. The package you want on Debian-based systems (like Ubuntu) is <code>ncurses-term</code>. </p>

<p>Alternatively, you can install it in your home directory. To do this, on OS X type</p>

<pre><code>infocmp &gt; /tmp/dtterm
scp /tmp/dtterm username@example.com:/tmp
ssh example.com tic /tmp/dtterm
</code></pre>

<p><code>tic</code> (terminfo compiler) will create a terminfo database entry in <code>~/.terminfo/d/dtterm</code>, and you should be good to go.</p>
