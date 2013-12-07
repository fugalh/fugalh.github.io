---
layout: post
status: publish
published: true
title: iptables doesn't do TOS/DSCP masking
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 952
wordpress_url: urn:uuid:f8d8ce7d-d53b-4002-9a97-4f2ab9d9bb3f
date: '2008-03-29 08:14:00.000000000 -07:00'
tags:
- qos
- iptables
- ipchains
- tos
- dscp
- tc
- mask
comments: []
---
<p>iptables, I'm really disappointed in you. If I'm reading your manpage correctly, and <a href="http://www.faqs.org/docs/linux_network/x-087-2-firewall.tos.manipulation.html">the NAG</a> says that I am, you don't support matching or setting the TOS field (whether as a TOS byte or as the DSCP 6-bit subfield) with a mask. You can only match exact values. </p>

<p>That's just about pretty much useless. And considering that ipchains did let you do masks (although it was a cumbersome and-mask and xor-mask pair), inexcusable. One could use <code>-m u32</code>, but this doesn't seem to be available in OpenWRT. Luckily the goal is to mark packets for <acronym title="Quality of Service">QoS</acronym>, and I can just drop into <code>tc</code> directly to accomplish what I need. So to match any packet with the low delay bit set,</p>

<pre><code>tc filter add dev $DEV parent $PARENT protocol ip u32 \
    match ip tos 0x10 0xff flowid $FLOW
</code></pre>
