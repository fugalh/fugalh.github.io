---
layout: post
status: publish
published: true
title: Trackback Spam
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 655
wordpress_url: urn:uuid:53421c30-fcf3-4615-93ba-006388c92559
date: '2006-07-03 11:29:41.000000000 -07:00'
tags:
- typo
- meta
- trackback
- spam
comments: []
---
<p>My blog is fairly impervious to comment spam. I've got one or two comments that
I had to delete, but I can respond fairly quickly because I get a Jabber
notification of comments. I think the ajax comment mechanism does most of the
filtering.</p>

<p>I just discovered that I am <em>not</em> impervious to trackback spam. Turns out there
was a lot that I didn't even know existed. Luckily, I didn't have a single
valid trackback so I could just do this at the rails console:</p>

<pre><code>Trackback.find(:all).map {|t| t.destroy}
Article.find(:all).map {|a| a.allow_pings=false; a.save}
</code></pre>

<p>I also changed the default allow trackbacks setting to no.  Trackbacks are a
neat idea but obviously not one that works.</p>
