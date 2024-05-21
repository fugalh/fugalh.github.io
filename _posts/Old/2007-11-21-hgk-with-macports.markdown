---
layout: post
status: publish
published: true
title: hgk with MacPorts
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 905
wordpress_url: urn:uuid:db2031fc-e909-48c6-abcf-efdcec9091b8
date: '2007-11-21 11:23:09.000000000 -08:00'
tags:
- hg
- mercurial
- hgk
- macports
comments: []
---
<p>If you use mercurial from MacPorts, you need the following in your <code>~/.hgrc</code> to enable the hgk extension (GUI tree browser, invoked with <code>hg view</code>):</p>

<pre><code>[extensions]
hgk=

[hgk]
path=/opt/local/share/mercurial/contrib/hgk
</code></pre>

<p>While you're in there, enable the mq, fetch, and record extensions.</p>
