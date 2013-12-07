---
layout: post
status: publish
published: true
title: Jabber Call Notification
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 839
wordpress_url: urn:uuid:cc00c727-c7d8-4f0b-a2ef-a71f0a142f6c
date: 2007-05-17 14:52:00.000000000 -07:00
tags:
- asterisk
- voip
- jabber
comments:
- id: 1571
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-05-22 16:30:46 -0700'
  date_gmt: ''
  content: <p>It occurs to me that I could use the System application instead of AGI,
    and pass the parameters on the command line instead. That would simplify the shell
    script because you don't have to deal with reading stdin one line at a time and
    recognize when the environment is done being sent.</p>
---
<p>I can't believe I never thought of this before. It's the ultimate in couch potatoism.</p>

<p>We don't use the phone much. When it rings, the house fills with moaning and groaning because nobody wants to answer it, but we often don't dare ignore it because we don't know who it is. As I usually have my laptop with me, or at least in sight, I realized (with the idea coming from a client who wants me to do some Jabber integration) that the perfect solution is to have Asterisk send me a notification via Jabber with the caller ID.</p>

<p>It's very simple. I use the <a href="http://sendxmpp.platon.sk/">sendxmpp</a> program to
do the heavy lifting. Here's the
<a href="http://hans.fugal.net/src/batphone/doc">Batphone</a> script:</p>

<pre><code>#!/usr/bin/ruby

## Configuration
# sendxmpp config file has to be mode 600 and owned by the asterisk user
CONFIG="~fugalh/telephony/.sendxmpprc"
RESOURCE="Asterisk"
RECIPIENTS="hans@fugal.net erin@fugal.net"

require 'agi'
agi = AGI.new
IO.popen("sendxmpp -r #{RESOURCE} -f #{CONFIG} #{RECIPIENTS}", "w") {|f|
  f.puts "Incoming call from #{agi.env['callerid']}"
}
</code></pre>

<p>As much as I love Batphone, it's almost as easy to do with a shell script:</p>

<pre><code>#!/bin/sh

# sendxmpp config file needs to be mode 600 and owned by the asterisk user
CONFIG=~fugalh/telephony/.sendxmpprc
RESOURCE=Asterisk
RECIPIENTS="hans@fugal.net erin@fugal.net"

# this snippet from http://yakko.cs.wmich.edu/~drclaw/asterisk/cidname/
declare -a array
while read -e ARG &amp;&amp; [ "$ARG" ] ; do
    array=(` echo $ARG | sed -e 's/://'`)
    export ${array[0]}=${array[1]}
done

echo "Incoming call from $agi_callerid" | \
    sendxmpp -r $RESOURCE -f $CONFIG $RECIPIENTS
</code></pre>

<p>If you are lucky enough to get <code>agi_calleridname</code> set as well, you obviously
might like to integrate that information into your message too. Here's the Asterisk dialplan snippet:</p>

<pre><code>exten =&gt; s,1,AGI(/home/fugalh/telephony/jabber.agi)
exten =&gt; s,n,Dial(SIP/sipura&amp;SIP/hans,30)
; ...
</code></pre>
