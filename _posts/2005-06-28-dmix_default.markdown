---
layout: post
status: publish
published: true
title: dmix by Default in ALSA 1.0.9
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 3
wordpress_url: urn:uuid:9d1854be-971b-46aa-ad7f-801db85f54cd
date: 2005-06-28 09:04:07.000000000 -07:00
tags:
- audio
comments: []
---
<p>I say, it's high time to celebrate. From the ALSA 1.0.9 changelog:</p>

<pre><code>- Summary: Use dmix/dsnoop for default PCM
  Use dmix/dsnoop plugins for default PCM in most of mobo chips
</code></pre>

<p>If you don't know what dmix is, basically it solves the problem of only
one program being able to play audio at a time on cheap sound cards. In other
words, kick those abomination sound servers (e.g. esd and artsd) out the door.</p>
