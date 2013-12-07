---
layout: post
status: publish
published: true
title: '&#161;Adios, MediaProxy!'
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 815
wordpress_url: urn:uuid:fbdcb6fa-b703-48b8-a484-74e22c599ed5
date: 2007-03-06 10:46:29.000000000 -08:00
tags:
- asterisk
- voip
- ser
- mediaproxy
- openser
- sip
- rtpproxy
- rtp
comments: []
---
<p>I have extolled the virtues of
(<a href="http://openser.org">Open</a>)<a href="http://iptel.org/ser">SER</a>+<a href="http://www.ag-projects.com/MediaProxy.html">MediaProxy</a>
in the past, but I can no longer recommend it. Instead I recommend using
<a href="http://asterisk.org">Asterisk</a> as a sort of pseudo media proxy. Why? Read on.</p>

<p>The problem is that
<a href="http://en.wikipedia.org/wiki/Session_Initiation_Protocol">SIP</a> and
<a href="http://en.wikipedia.org/wiki/Network_address_translation">NAT</a> don't get
along. The reason they don't get along (besides that NAT is evil) is that the
<a href="http://en.wikipedia.org/wiki/Real-time_Transport_Protocol">RTP</a> packets (the
media stream) may follow a completely different, and more direct, path from
endpoint to endpoint than the SIP packets do. This is a good thing, except in
the face of NAT. If there's a NAT involved, the RTP packets often can't get
through. SER+MediaProxy solves this by tricking the endpoints into thinking
mediaproxy is the other endpoint for RTP data. MediaProxy, which is not behind
a NAT, is able to receive data from both parties and forward it on to each
party (via the NAT holes already punched by them talking to the media proxy).</p>

<p>It's an elegant setup. It's a wonderful solution to an evil problem. But it
turns out, quite surprisingly, that MediaProxy doesn't scale as well as other
solutions. That is, there's a too-low ceiling on the number of simultaneous
calls that MediaProxy can handle before the CPU maxes out.</p>

<p>Here's a setup that scales much better. Instead of doing the MediaProxy dance
when NAT is detected, instead have SER proxy the packets through Asterisk. Have
Asterisk set up to accept calls from SER (who has already authenticated the
user), or to do the user authentication (in addition to SER?), and it will
happily insert itself in the middle of the call as a back-to-back user agent.
If you do this you will want to take care that you avoid gratuitous transcoding
because that will certainly not scale as well as MediaProxy. But if you can
keep from transcoding, this scales more than 2x better than MediaProxy.</p>

<p>This is a surprising result, because Asterisk is more complicated than
MediaProxy, and the whole back-to-back user agent scheme is a lot more
complicated than simply forwarding packets which is in essence all MediaProxy
has to do, and that Asterisk has generally done a poor job of supporting SIP.
MediaProxy is written in Python, and Asterisk in C. That might be part of it.
<a href="http://www.jaredsmith.net/asterisk-consultant.php">Jared Smith</a> tells me that
there are various new optimizations for bridging calls in Asterisk, such as
header caching. That might be another part of it.</p>

<p>Since setting up Asterisk this way is no harder and I think quite a bit easier
than setting up MediaProxy (esp. in light of the "don't use_mediaproxy() (and
friends) more than once in a route" bug), and Asterisk scales better in the
real world, I have to recommend Asterisk as your media "proxy".</p>

<p>The story doesn't end here, though. It continues to evolve. It remains to be
seen whether another implementation of a media proxy than MediaProxy or
RTPProxy (which is still not as scalable as Asterisk in our tests) can do the
job more efficiently still. I think that it should be possible. I might do it
as a learning project in Erlang, but no promises. At this point I think it is
doubtful whether a naïve implementation in any language, even C, would outrun
Asterisk with its bridging optimizations. On the other hand, forwarding RTP and
RTCP packets unchanged isn't rocket science and it just might be easy to outrun
Asterisk.</p>

<p>Thanks to Elliot at <a href="http://arrivaltel.com/">Arrivaltel</a> and Jared for helping
me with testing, pontificating, and discussion, and to Brent Thomson for
casting a shadow of doubt over MediaProxy (for other reasons) in my mind in the
first place.</p>
