---
layout: post
status: publish
published: true
title: Terminal Unicode Wrangling on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 793
wordpress_url: urn:uuid:25b2f71d-9c4a-46ae-a955-cba091aaf810
date: '2007-02-18 16:19:00.000000000 -08:00'
tags:
- mac
- vim
- bash
- utf-8
- unicode
- terminal
- iTerm
- ls
- coreutils
comments:
- id: 1555
  author: Noah Tye
  author_email: ''
  author_url: http://noah.tyes.us/
  date: '2007-02-18 17:05:57 -0800'
  date_gmt: ''
  content: <p>Your link in the second paragraph is broken. ("this article on Internationalizing
    the Mac OS X terminal")</p>
- id: 1556
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-02-18 17:07:17 -0800'
  date_gmt: ''
  content: <p>Thanks, fixed.</p>
- id: 1557
  author: tene
  author_email: tene@iodynamics.com
  author_url: ''
  date: '2007-02-18 22:22:57 -0800'
  date_gmt: ''
  content: |-
    <pre>
    [tene@corktooth ~]$ echo æøÜÉ > /tmp/ƒøø
    [tene@corktooth ~]$ ls /tmp/ƒøø
    /tmp/ƒøø
    [tene@corktooth ~]$ cat /tmp/ƒøø
    æøÜÉ
    [tene@corktooth ~]$ vim /tmp/ƒøø
    [tene@corktooth ~]$ screen vim /tmp/ƒøø
    [screen is terminating]
    [tene@corktooth ~]$
    </pre>

    <p>Everything worked just fine for me on a mundane Fedora box with xterm.</p>
- id: 1558
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-02-18 22:24:39 -0800'
  date_gmt: ''
  content: <p>Good to hear. I figured most if not all Linux distros had worked this
    out a few iterations ago.</p>
- id: 1559
  author: Lars
  author_email: lars.yencken@gmail.com
  author_url: ''
  date: '2007-03-04 20:17:10 -0800'
  date_gmt: ''
  content: <p>Ubuntu has been fine for several iterations, although getting the input
    methods working was sometimes a strain. These OS X terminal problems baffle and
    frustrate me though, since sometimes when typing in CJK glyphs, I get nothing
    but a terminal bell. I just sent feedback to Apple, and I'd encourage others to
    do the same. Lets hope it's fixed in Leopard.</p>
---
<p>This is the 21<super>st</super> Century. It's time for Unicode. OS X does a      decent job of supporting Unicode overall, but it is far from perfect. Perhaps   the most noticeable is the mass confusion that is Unicode in the terminal. The  problem is actually legion, and it takes a little effort to fix it. But you     can fix it and you can do it today.</p>

<p>Start at <a href="http://www.rift.dk/news.php?item.7.6">this article on Internationalizing the Mac OS X terminal</a>. Following the instructions there will get you 90%   of the way there. You will install a new version of bash and coreutils (for     ls, cd, etc.), you'll set up your locale information (actually you only need    to set LANG, in my experience. I <code>export LANG=en_US.UTF-8</code> in my <code>.bashrc</code>).</p>

<p>If you use OS X's default vim (<code>/usr/bin/vim</code>), it will Just Work. But if you    have vim 7.0 from some other source, it may or may not work. In particular if   you do <code>sudo port install vim</code> you'll probably get a broken vim. Be sure to     use the multibyte variant if you install from ports.</p>

<p>If you use iTerm, it might work worse than before you made the changes above.    But notice that it works fine if you run another bash instance, or screen. I'm  not sure but I think you fix it with the <code>LC_CTYPE</code> hack detailed in <a href="http://desp.night.pl/terminal.html">this      article</a>. Those <code>.inputrc</code> lines probably   won't hurt either, though I'm not sure what problem they fix. One of those two  changes seems to have fixed the iTerm problem.</p>

<p>Speaking of screen, you probably want to add <code>defutf8 on</code> to your <code>~/.screenrc</code>.</p>

<p>I'm curious if things work out of the box in $YOUR<em>FAVORITE</em>DISTRO. I've         previously mucked about with unicode so much in Debian and Ubuntu I have no     recollection of what the default state of affairs is. Try the following and     let me know in the comments how it worked.</p>

<pre><code>echo æøÜÉ &gt; /tmp/ƒøø
ls /tmp/ƒøø
cat /tmp/ƒ&lt;tab&gt;
vim /tmp/ƒøø
screen vim /tmp/ƒøø
</code></pre>

<p>For me, I see exactly that and exactly what you'd expect on the terminal and in  vim (both in and out of screen), which has never all happened in OS X for me    before. It does work over ssh on my Debian box, but as I say I've played with   things there so it may or may not have worked out of the box.</p>
