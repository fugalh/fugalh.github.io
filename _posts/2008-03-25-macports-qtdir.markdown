---
layout: post
status: publish
published: true
title: MacPorts QTDIR
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 946
wordpress_url: urn:uuid:1d41e040-7808-4c64-ad1f-a6159fb240f1
date: 2008-03-25 21:38:30.000000000 -07:00
tags:
- mac
- qt
- qt3
- macports
- qtdir
comments: []
---
<p>If I had a nickel for every time I had to scour the web to figure out the right setting for <code>QTDIR</code> on {Debian,Ubuntu,OS X}…</p>

<p>On OS X, if you installed the <code>qt3</code> package, then the proper setting is
<code>QTDIR=/opt/local/lib/qt3</code>. I wrote this little script to source before
commencing building a Qt3 project:</p>

<pre><code>#QTDIR=/usr/local/Trolltech/qt-mac-free-3.3.7
#QTDIR=/Developer/qt
QTDIR=/opt/local/lib/qt3
PATH=$QTDIR/bin:$PATH
DYLD_LIBRARY_PATH=$QTDIR/lib:$DYLD_LIBRARY_PATH

export QTDIR PATH DYLD_LIBRARY_PATH
</code></pre>
