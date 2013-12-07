---
layout: post
status: publish
published: true
title: Case Sensitivity on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 849
wordpress_url: urn:uuid:ae793e1b-865f-4417-896c-9fa86b943e33
date: '2007-07-01 08:20:00.000000000 -07:00'
tags:
- mac
- case
comments: []
---
<p>As you may be aware, the default filesystem for OS X is HFS+ Journaled without
case sensitivity. It retains case, but <code>foo.txt</code> and <code>foo.TXT</code> are the same
file. You <em>can</em> install on an HFS+ case-sensitive disk, but if you do some apps
may give you trouble down the road if they sloppily assume case insensitivity.
So I chose to go with the default, even though I knew someday I would really
want case sensitivity. That day came yesterday.</p>

<p>I'm using <a href="http://progetti.arstecnica.it/tailor">Tailor</a> to create a <a href="http://www.selenic.com/mercurial/wiki/">Mercurial</a> mirror of the <a href="http://www.flightgear.org">FlightGear</a> CVS
archives. More on that later, but suffice it to say that from time to time
people want to "rename" files in CVS (so far as you can call what CVS does
renaming) to change poor case decisions. e.g. a file something like
<code>747-SouthWest.xml</code> got changed to <code>747-Southwest.xml</code> (don't take my word on
the exact filename). This was causing problems because CVS would get a conflict
when it would try to check out that revision, and complain that the first
filename is in the way, and if you manually intervene and remove it then it
would claim that the first filename was missing.</p>

<p>So I thought, what would be ideal is a dynamically sized filesystem-in-a-file.
It should automatically grow, but not take up more space than it needs to. It
turned out to be easy to do in OS X. With Disk Utility, create a new image.
Make it a sparse image and give it a reasonable maximum size (I chose 8 gigs).
Then go into the partitioning and give it a nice name and an HFS+
case-sensitive filename. Uncheck the box for OS 9 support. Mount it and symlink
it to wherever you want, et voilá, you have a case-sensitive subtree in your
filesystem. It's a thing of beauty. When space gets tight and you need to
shrink it to its minimum size, delete what's not needed (i.e. make clean),
empty the trash, and then use <code>hdiutil</code>(1) to do the job (hint: compact).</p>
