---
layout: post
status: publish
published: true
title: ChanSpy Silence
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 842
wordpress_url: urn:uuid:82c5ffe7-32ca-44ea-b8cd-dfce335e5901
date: 2007-06-01 11:00:34.000000000 -07:00
tags:
- asterisk
- chanspy
comments: []
---
<p>I was setting up <a href="http://www.voip-info.org/wiki-Asterisk+cmd+ChanSpy">ChanSpy</a> in an <a href="http://asterisk.org">Asterisk</a> dialplan today and it just wasn't working. Here is the snippet:</p>

<pre><code>exten =&gt; 501,1,ChanSpy()
</code></pre>

<p>I would be connected, and the Asterisk console would tell me I was spying on people, but I would hear nothing at all. For the record, the calls I was spying on were all sorts, but mostly Zap, and I was spying from a SIP softphone.</p>

<p>After some blind fiddling, I found this combination works:</p>

<pre><code>exten =&gt; 501,1,ChanSpy(,b)
</code></pre>

<p>The <code>b</code> option is "only spy on channels involved in a bridged call". I don't know why this fixes it, but it does.</p>

<p>For the record, it's working great even when calls are being recorded (with MixMonitor), without setting <code>transmit_silence_during_record=yes</code> in <code>/etc/asterisk/asterisk.conf</code> (as mentioned on the wiki). I don't know about the Record application.</p>
