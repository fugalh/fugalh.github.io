---
layout: post
status: publish
published: true
title: NuFone Outgong Call Woes
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 99
wordpress_url: urn:uuid:a40218c9-167d-4fcf-bda4-45c65861e8c8
date: '2005-08-05 08:43:13.000000000 -07:00'
tags:
- voip
comments: []
---
<p>NuFone is my VOIP provider of choice, but I had a devil of a time being able to
call out from my Sipura SPA-1001, through Asterisk, to NuFone. It turns out the
problem was Caller ID. When I set my sipura's extension to 42 instead of
sipura, I was able to dial out, but the CID said simply 42. Well that is kind
of cool, and demonstrates that the reason NuFone's Asterisk (or PSTN
connection) was rejecting my call is that I had invalid Caller ID for the
number ("sipura"), but I would like to be a good phone system citizen. Junction
Networks, of whom I had never before heard until google matched us up, <a href="http://www.junctionnetworks.com/Asterisk-config.htm">has the
answer</a>.  So I added that
<code>SetCIDNum</code> call and things are working great.</p>
