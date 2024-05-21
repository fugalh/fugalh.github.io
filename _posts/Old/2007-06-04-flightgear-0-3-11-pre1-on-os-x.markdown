---
layout: post
status: publish
published: true
title: FlightGear 0.3.11-pre1 on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 844
wordpress_url: urn:uuid:950ec683-8876-4600-bb54-222681f42140
date: '2007-06-04 14:58:07.000000000 -07:00'
tags:
- mac
- flightgear
comments: []
---
<p>Good news! <a href="http://flightgear.org/">FlightGear</a> version 0.3.11-pre1 builds
perfectly well on OS X (Tiger). The dependencies are plib and SimGear. You
should install plib via macports (the 1.8.4 upstream tarball fails to build,
CVS might fare better), then compile and install
<a href="http://www.simgear.org/">SImGear</a> version 0.3.11-pre1, then compile and
install FlightGear and grab the fgfs-base package and move it to
/usr/local/share/FlightGear.</p>

<p><a href="http://macflightgear.sourceforge.net/home/">MacFlightGear</a> works too, version
0.9.10. It will probably have an 0.9.11 release sometime not long after the
release of 0.9.11 (if not sooner), because it would be hard to justify not
releasing it when FlightGear builds out of the box. You might like the
one-download no-build nifty-gui-launcher aspects of MacFlightGear. I don't
because it messes with <code>.fgfsrc</code> and I like the consistency with Linux. But we
never said I was sane.</p>
