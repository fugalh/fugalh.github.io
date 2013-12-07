---
layout: post
status: publish
published: true
title: autotools
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1009
wordpress_url: urn:uuid:a016a311-866e-40ae-8138-83901a3fd10a
date: 2008-10-07 17:31:00.000000000 -07:00
tags:
- make
- autoconf
- automake
- autotools
- makefile
- autoheader
- autoreconf
- aclocal
- m4
- libtool
- gnu
- configure
- tutorial
comments: []
---
<p>I've been known to knock autotools (autoconf and automake and friends), but let it not be forgotten that I have also been known to say that alternative pickings are pretty slim.</p>

<p>Part of the problem with autotools is that it's easy to make an unmaintainable and unusable mess, and one that is essentially opaque to the uninitiated.</p>

<p>But, on the other hand, it's equally easy to use autotools in a sane way which is just as easy or easier than writing makefiles and whatnot by hand. <em>Once you get over the initial learning curve.</em> That has been a big caveat. I've climbed that curve a few times and it goes in one ear and out the other. </p>

<p>Well, a friend pointed out an <a href="http://www.lrde.epita.fr/~adl/autotools.html">excellent tutorial on autotools</a> which demystifies autotools. It also makes a good reference for next week when you've forgotten everything. </p>

<p>If you're writing code to distribute, you should consider using autotools (and doing so sanely), and this is a good starting point. But that's not the only reason to check it out. You may just be curious, or you may wish to learn how this works so you can contribute patches and bring sanity to your favorite project's build system.</p>

<p>But whatever you do, <em>never ever</em> just copy someone else's autotools configuration into yours and apply "shotgun debugging" to shoehorn it into your project. That is the wrong approach and the primary cause of so many broken autotools setups.</p>
