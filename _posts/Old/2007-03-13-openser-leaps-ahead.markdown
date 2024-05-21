---
layout: post
status: publish
published: true
title: OpenSER Leaps Ahead
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 820
wordpress_url: urn:uuid:91716f2c-5ea6-4920-aa33-4d237472d712
date: '2007-03-13 12:31:49.000000000 -07:00'
tags:
- voip
- ser
- openser
- sip
comments:
- id: 1568
  author: Marc
  author_email: ''
  author_url: ''
  date: '2007-03-15 08:14:50 -0700'
  date_gmt: ''
  content: <p>The seas module and Java SIP Servlet application server (wesip.eu) is
    another new cool thing, waiting long for such way to integrate VoIP and HTTP services
    ... gonna love the 1.2.0...</p>
---
<p>Thanks to serendipitous timing on <a href="http://www.zmonkey.org">tensai</a>'s part, I learned today that <a href="http://www.openser.org/">OpenSER</a> version 1.2.0 was released just yesterday. It looks exciting; a few of the most fundamental problems with SER have finally been fixed. Number one on this list is script variables. Now you can do:</p>

<pre><code>$ruri = "sip:" + $from.user + ":" + $to.domain;
</code></pre>

<p>Second on the list is that you can now "extend OpenSER functionality by writing Perl applications to be executed embedded in configuration files."
Other wonderful things: </p>

<ul>
<li>Pseudo variables can be used directly in the script</li>
<li>Pseudo variable transformations</li>
<li>DNS NAPTR/SRV failover</li>
<li>An XMLRPC management interface</li>
<li>XMPP (Jabber) Gateway</li>
<li>SNMP</li>
<li>LCR database caching</li>
</ul>

<p>All in all, it looks like an exciting release. If (Open)SER disappointed you in the past, now might be the time to look again at OpenSER.</p>
