---
layout: post
status: publish
published: true
title: Typo Cache
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 886
wordpress_url: urn:uuid:a1bbba87-00dc-4479-b03d-a3e7d06c720c
date: 2007-10-26 22:13:06.000000000 -07:00
tags:
- typo
comments: []
---
<p><a href="http://typosphere.org/">Typo</a>, the blogging software that runs this blog, was getting slower and slower for an unknown reason. Finally I decided I had had enough and begged for help in IRC. sprewell was kind enough to help me track it down to an odd caching problem. Apparently my caches weren't going away like they should, and I had accumulated some 1.7 million files in my <code>tmp/cache</code> directory. Even running <code>find tmp/cache | wc -l</code> took a few minutes. No wonder typo (which was probably actually looking at each file's contents) was having a cow. Apparently this isn't a common problem, but they have struggled with cache problems in the past. So if your typo is feeling sluggish, check for the ballooning cache. If it's there, stop typo and move or delete the offending cache directory, i.e.</p>

<pre><code>typo stop .
mv tmp/cache /tmp
typo start .
</code></pre>

<p>It's nice to have my old typo back.</p>
