---
layout: post
status: publish
published: true
title: m-a -t a-i lirc
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 822
wordpress_url: urn:uuid:80652eab-48bb-450f-bf6a-c9be7144d8cf
date: 2007-03-15 20:55:58.000000000 -07:00
tags:
- lirc
- modass
comments: []
---
<p>The "Debian Way" to install external kernel modules is, when applicable, to use
<a href="http://alioth.debian.org/projects/modass/">module assistant</a>.
This creates and installs a .deb so that you can install/upgrade/whatever with
apt. </p>

<p>Apparently a recent change in the linux kernel moved <code>include/config.h</code> to
<code>include/autoconf.h</code>. When I tried to build the lirc modules for my new kernel
by typing:</p>

<pre><code>m-a -t a-i lirc
</code></pre>

<p>I got yelled at. Well it turns out there's a <a href="http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=400494">bug
report</a> and
<a href="http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=400494;msg=5;filename=lirc-config.patch;att=1">patch</a>,
so I could have patched the lirc-modules-source package, but armed with
knowledge of the source of the problem problem it was easier to short circuit
and just do this:</p>

<pre><code>ln -s /lib/modules/`uname -r`/source/include/linux/{autoconf,config}.h
</code></pre>

<p>Works like a charm. Enjoy.</p>
