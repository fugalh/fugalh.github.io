---
layout: post
status: publish
published: true
title: find | while read i; do foo "$i"; done
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 48
wordpress_url: urn:uuid:f41c5fc1-8b58-48cd-bc46-f018ece597a0
date: '2005-06-23 13:08:00.000000000 -07:00'
tags:
- linux
comments: []
---
<p>Thanks to <a href="http://www.zmonkey.org/blog/">tensai</a> for inspiring me to realize
this incredible idiom. No longer will file and directory names with spaces
cause me untold grief. Behold:</p>

<pre><code>find ~/music -type d | while read i; do mp3gain -k -a "$i"/*mp3; done
</code></pre>
