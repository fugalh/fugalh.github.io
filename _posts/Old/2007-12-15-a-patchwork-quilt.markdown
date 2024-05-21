---
layout: post
status: publish
published: true
title: A Patchwork Quilt
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 915
wordpress_url: urn:uuid:5d8264e8-119d-44c1-80c9-b916615a5540
date: '2007-12-15 10:29:59.000000000 -08:00'
tags:
- diff
- quilt
- patch
- oss
- vcs
comments: []
---
<p>"Patches welcome!"</p>

<p>It's a common exclamation in the open source world. In many ways, it's at the very center of the open source development model, especially the bazaar style. Sometimes flippant, sometimes derisive, sometimes earnest, sometimes pleading, always at least half true.</p>

<p>You may be familiar with how to use <code>diff</code> to create a patch. Just to quickly recap, you make a copy of the original file(s), make your change(s), and use <code>diff</code> to make a patch. Not too hard, but there's lots of intricacies to get wrong, or if not wrong then against the cultural grain. You need to make a level 1 patch, you need to make a unified diff, etc. The human overhead in making copies of files and constructing diff command lines is significant, so some smart people naturally wrote scripts to automate it. Andrew Morton was one of these smart people and wrote a set of patch scripts for working on the Linux kernel. Then Andreas Grünbacher tweaked them, generalized them, and released them as <a href="http://savannah.nongnu.org/projects/quilt">Quilt</a>.</p>

<p>Quilt makes patch management much simpler. I won't go into all its capabilities or usage, for that I recommend the excellent paper <a href="http://hans.fugal.net/quilt.pdf">How to Survive with Many Patches or an Introduction to Quilt</a>. I will give you a use case and show you how quilt applies.</p>

<p>I contribute in a small way to the project <a href="http://flightgear.org">FlightGear</a>. I don't have CVS access, so any contributions I make are in the form of bug reports or sending patches to the development list. Let's take the use case of fixing a compilation bug on my platform (OS X Leopard), from the beginning.</p>

<p>First I download the tarball and extract it somewhere. Quilt happily works over
any directory structure, it could be CVS or any other VCS, or just an extracted
tarball, or whatever.</p>

<p>Next I try to build it and notice that it fails to build. Now I know there's a patch to be made, so I tell quilt about it:</p>

<pre><code>~/fg/FlightGear-0.9.11-pre2$ quilt new leopard.diff
Patch leopard.diff is now on top
</code></pre>

<p>Now, I edit the file in question and fix the bug. Quilt needs to know ahead of time which file(s) I'm going to edit so it can make copies of the originals and create the diffs. So whenever you're constructing a patch, you use <code>quilt edit foo</code> instead of <code>$EDITOR foo</code>. You might <code>alias qvim='quilt edit'</code>. </p>

<pre><code>~/fg/FlightGear-0.9.11-pre2$ quilt edit foo
</code></pre>

<p>Lather, rinse, repeat until you've created a totally tubular bugfix. Then, tell quilt to update the patch file (which is stored in <code>patches/</code>) with</p>

<pre><code>~/fg/FlightGear-0.9.11-pre2$ quilt refresh
</code></pre>

<p>Finally, submit the patch from <code>patches/</code> however your project likes to get patch submissions. Since I use gMail for this list, I usually just type <code>quilt diff</code> and copy &amp; paste it into the message. For another project or a one-off patch I'd probably use <code>mutt -a patches/leopard.diff foo@example.com</code>. Quilt also has facilities for sending patches by mail.</p>

<p>Later you may want to start a new patch for a new feature, or a different bug. Just <code>quilt new</code> and begin working on it. If you at some point want to unapply a certain patch, or all of them, you want <code>quilt pop</code>. Likewise you can <code>quilt push</code>. You can import other people's patches, edit and refresh your patch until you get it just right, etc. Quilt is a powerful but easy-to-use tool for all your contribute-to-open-source-software-without-commit-access needs.</p>

<p>As an afterword, let me describe how I used to try to do this in general and for FlightGear in specific. In general, I'd just make a copy of the original source tree whenever I remembered to do so which is almost never. When I forgot, I'd have to move the modified one somewhere else and untar a fresh copy. It was error prone and wasteful but it worked for the single-patch use case. On large projects that I want to contribute to more than once, like FlightGear, I used to go through all sorts of gyrations trying to make a bridge from CVS to some distributed VCS using Tailor, and then try to generate meaningful diffs from my sister repositories and somehow manage to merge things back in that were changed. This is especially annoying for changes you manage to get committed, which all of a sudden are conflicts (depending on how smart the merger is and whether they modified your patch or applied it as-is). Then, I ran into the very annoying disadvantage that several other people were doing the same thing, with the same VCSes, and yet we couldn't interoperate because we had all set up our own tailor scripts and the repositories were completely independent even though semantically they were just branches of the same thing. It got very complicated and had very few benefits in real life. I finally came to the conclusion that what I was doing was generating and applying patches to the canonical sources, and when I finally figured that out it became apparent that using Quilt was the right thing to do. I can still keep the quilt stuff in revision control. Sometimes I use Mercurial Queues (based on Quilt) instead for more integration, but Quilt is usually sufficient.</p>

<p>I encourage you to give Quilt a try next time you need to make a patch. You won't be sorry.</p>
