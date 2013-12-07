---
layout: post
status: publish
published: true
title: Implications of BIND Forwarders
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 38
wordpress_url: urn:uuid:b7dbffcc-51a4-4db9-bd48-a6b554ad9f49
date: 2005-07-15 14:56:31.000000000 -07:00
tags:
- linux
comments: []
---
<p>I've got forwarders set on the nameserver at work. Last week, I tried to
delegate a subdomain to another nameserver and had a devil of a time. The
problem was the forwarders; here is the solution:</p>

<pre><code>zone "subdomain.example.com" in {
    // ...
    forwarders { };
};
</code></pre>

<p>Otherwise, the nameserver will ask the forwarders and not the delegate. Having
learned this tidbit, my subconscious realized a few days later (i.e. today)
that I could use this to my advantage in another seemingly unrelated situation.</p>

<p>My LAN at home is connected to work's LAN. At work, as well as at home, I have
split views for internal and external. You can use per-zone <code>forwarders</code>
clauses in situations like these to access work's internal view (without
becoming a slave) even though your normal forwarders are third parties such as
your ISP's name servers. Here is the config on my home box, in the internal
view:</p>

<pre><code>zone "example.com" in {
    type forward;
    forwarders { 172.16.5.3; 172.16.59.7; };
    forward only;
};
</code></pre>
