---
layout: post
status: publish
published: true
title: RADEON Xinerama
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 63
wordpress_url: urn:uuid:957f80f0-9a68-42f8-806a-aa5ce89930ea
date: 2005-01-17 10:48:34.000000000 -08:00
tags:
- linux
comments: []
---
<p>It's a trick to get a radeon card with two outputs to work with xinerama. It
may be the same for other two-output cards.</p>

<p>Apparently we had a version of the radeon driver that didn't yet support
MergedFB, so don't ask about that. We're too lazy to do something like download
the new driver. So we tried to get xinerama working. </p>

<p>In the end, this is what we had to do, and it's a bit counterintuitive. You
need two <code>Screen</code> sections, as is normal for a Xinerama setup. A Screen section
maps a monitor to a video card. They use the same card, right, so they ought to
use the same <code>Device</code> section. Well, nope. You need <em>2</em> device sections, and
not only that but you have to specify the BusID on both, even though it's the
same BusID.</p>

<p>So basically, set up xinerama per the <a href="http://www.tldp.org/HOWTO/Xinerama-HOWTO/">xinerama
howto</a> and pretend like you _do_
have two cards - they'll just both be on the same busid.</p>
