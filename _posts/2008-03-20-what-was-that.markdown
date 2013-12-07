---
layout: post
status: publish
published: true
title: What was that macro?
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 944
wordpress_url: urn:uuid:1c13cc5b-8dba-4afb-a733-f9bca8ef908b
date: 2008-03-20 14:46:00.000000000 -07:00
tags:
- C
- osx
- gcc
- preprocessor
- macro
- define
- detect
comments: []
---
<p>I find myself asking this question a lot: "Now what was that define that detects <em>annoying platform that makes porting otherwise perfectly-portable code difficult</em>?"</p>

<p>This will narrow your search down to something useful:</p>

<pre><code>echo | cpp -dM
</code></pre>

<p>Go ahead, try it. I wish I'd known this one earlier.</p>
