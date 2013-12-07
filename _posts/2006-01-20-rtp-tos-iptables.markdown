---
layout: post
status: publish
published: true
title: Using iptables to set ToS
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 101
wordpress_url: urn:uuid:a9f7017f-b27c-4767-a363-1c755234630c
date: 2006-01-20 12:03:16.000000000 -08:00
tags:
- voip
comments:
- id: 2394
  author: Cristian Marian
  author_email: prodan_rd@yahoo.com
  author_url: ''
  date: '2011-05-17 05:03:31 -0700'
  date_gmt: '2011-05-17 05:03:31 -0700'
  content: "Hello, \r\n\r\nI need some help in the following problem: \r\nAll my search
    brings me to this site.\r\n\r\nUsing iptables command, i want to mark udp traffic
    from destination port 1234, with DSCP for Expedited forward PHB, on a linux router,
    if the input rate of this trafic is over 2Mbps. It is a didactic problem and I
    need some sugestions.\r\nWhat I now: one rule for accept the trafic &lt;=2Mbp
    and another rule to mark the trafic over 2Mbps.\r\n\r\nCan you help me please?\r\nThank
    you!\r\nCristian"
---
<p>X-Lite and Twinkle don't have a way to set <acronym title="Type of
Service">ToS</acronym>. So let's get iptables to do it:</p>

<pre><code>iptables -A POSTROUTING -t mangle -p udp -m udp --sport 8000:8009 \
    -j DSCP --set-dscp 0x2e
</code></pre>

<p>That sets the DSCP for UDP packets with a source port of 8000-8009 to 0x2e,
which is the Expedited Forwarding PHB. You'll need to pick a range that works
for you. Both X-Lite and Twinkle use 8000 as a default, so that's what this
rule says.</p>
