---
layout: post
status: publish
published: true
title: Only use_media_proxy once
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 102
wordpress_url: urn:uuid:90915fed-1c71-4b17-95a1-57e59f719766
date: '2006-02-04 10:52:56.000000000 -08:00'
tags:
- voip
comments: []
---
<p>If you ever see strange sdp content like the following:</p>

<pre><code>...
c=IN IP4 68.142.145.14568.142.145.145
...
m=audio 3501835018 RTP/AVP 0 8 3 98 97 101
...
</code></pre>

<p>That is, the IP address and port are repeated back to back (which really throws
off the far end), and you are using openser and mediaproxy, then you are
probably calling <code>use_media_proxy</code> twice in your ser routing. Apparently, this
is a bad idea. </p>
