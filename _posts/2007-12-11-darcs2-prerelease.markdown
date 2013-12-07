---
layout: post
status: publish
published: true
title: Darcs2 Prerelease
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 913
wordpress_url: urn:uuid:3828520b-d7e3-4536-8a27-d99e996975ae
date: 2007-12-11 11:33:12.000000000 -08:00
tags:
- git
- darcs
- hg
comments: []
---
<p><a href="http://lifeoflevi.com/">Levi</a> referred me to a post entitled <a href="http://blog.moertel.com/articles/2007/12/10/how-i-stopped-missing-darcs-and-started-loving-git">"How I stopped missing Darcs and started loving Git"</a>. It's an interesting read, but ironically the thing that interested me most was a comment mentioning that just yesterday <a href="http://article.gmane.org/gmane.comp.lang.haskell.cafe/33159">darcs 2.0.0pre1 was released</a>. It looks like some very exciting things are coming down the darcs pipe:</p>

<ol>
<li>It should no longer be possible to confuse darcs or freeze it indefinitely by merging conflicting changes.</li>
<li>Identical primitive changes no longer conflict.</li>
<li>Darcs get is now much faster, and always operates in a "lazy" fashion, meaning that patches are downloaded only when they are needed.</li>
<li>Darcs now supports caching of patches and file contents to reduce bandwidth and save disk space.</li>
<li>Speed improvements.</li>
</ol>

<p>The most exciting change is, of course, the elimination of the exponential merge. This is very good news indeed, if it means what I think it means. The second change I listed is also very interesting to me. You'll remember I posited that exact situation in <a href="http://hans.fugal.net/blog/articles/2007/11/16/mercurial-and-darcs">a previous post</a>, and was teased incessantly as a result.</p>

<p>Do read the release notes. If darcs2 is released within a reasonable time frame, it will continue to be a strong contender.</p>
