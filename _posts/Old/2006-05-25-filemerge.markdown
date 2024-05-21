---
layout: post
status: publish
published: true
title: FileMerge
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 208
wordpress_url: urn:uuid:c8f3ac5d-1eac-40a4-90ff-1114f4741c94
date: '2006-05-25 16:53:38.000000000 -07:00'
tags:
- cs
- osx
- diff
- svn
comments: []
---
<p>OS X has this nifty utility called FileMerge which is far and away the best way
to merge differing files that I have ever seen. Yes, that includes vimdiff,
although a sufficiently large gvimdiff is pretty good too. If you give it a
try, don't give up saying "too much mousing" until you've explored the (mostly
hidden) keyboard acceleration. I found sensible accelerators for every function
I hoped for.</p>

<p><a href="http://ssel.vub.ac.be/ssel/about:members:brunodefraine">Bruno De Fraine</a> has
gifted us with <a href="http://ssel.vub.ac.be/ssel/internal:fmdiff">a set of bash
scripts</a> to use FileMerge as
Subversion's <code>--diff-cmd</code> and <code>--diff3-cmd</code>.  This means when you have a
conflict in Subversion you can merge with FileMerge. Along with the <code>[helpers]</code>
section in <code>~/.subversion/config</code> you can be in FileMerge/SVN paradise.</p>

<p>I intend to figure out how to get this working with darcs soon. Actually I've
found some pages about it that don't seem to work with my current version of
darcs. When I get more HDD space I can install that silly Haskell compiler and
upgrade, then I will report if it works.</p>
