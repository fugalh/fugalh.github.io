---
layout: post
status: publish
published: true
title: OpenSER and MediaProxy
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 357
wordpress_url: urn:uuid:62992b9a-18ff-4b1e-b4d8-7f49449112a2
date: '2006-06-07 10:12:50.000000000 -07:00'
tags:
- voip
- ser
- mediaproxy
- utaug
- openser
- nat
- sip
comments: []
---
<p>Last night's presentation on OpenSER and MediaProxy went well, I think. We
talked a lot about SIP and NAT, and looked at some sample configurations. The
question came up about why or when one should want to deal with SER, and my
answer is either when you need the scalability of SER, or when you want to use
MediaProxy. There are other reasons why you might want to user SER, but IMHO
MediaProxy is the first and most important reason to use SER. Unless you <em>like</em>
troubleshooting NAT problems...</p>

<p>The slides and sample files are at <a href="http://hans.fugal.net/utaug">http://hans.fugal.net/utaug</a>. There are
hyperlinks in the slides, but I couldn't figure out how to get them to stand
out, so watch that mouse cursor. The sample
<a href="http://hans.fugal.net/utaug/eg/openser.cfg">openser.cfg</a> has not been tested,
but was pruned from a working config. If you see a problem with it let me know
and I'll fix it.</p>
