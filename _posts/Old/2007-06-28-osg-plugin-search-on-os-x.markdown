---
layout: post
status: publish
published: true
title: OSG Plugin search on OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 848
wordpress_url: urn:uuid:2402fbb3-315b-4e24-a5d5-6a3bd054b7a7
date: '2007-06-28 09:08:53.000000000 -07:00'
tags:
- mac
- osg
- search
comments: []
---
<p>When you compile <a href="http://openscenegraph.org"><acronym
title="OpenSceneGraph">OSG</acronym></a> version 2.0
from source on OS X, your OSG apps won't be able to find the OSG plugins unless
you intervene. The problem is that on OS X OSG looks in
<code>{~,}/Library/Application Support/OpenSceneGraph/Plugins/{,osgPlugins-2.0.0}</code>
for the plugins, but <code>make install</code> installs them to
<code>/usr/local/lib/osgPlugins-2.0.0</code>. You can intervene either by creating the
appropriate symlink or by setting the environment variable <code>OSG_LIBRARY_PATH</code>
appropriately. Note that if you install the binary package on the website
(which puts them in <code>/Library/...</code>) it would find the wrong plugins even if you
had a symlink in <code>~/Library/...</code>, so <code>OSG_LIBRARY_PATH</code> might be a cleaner
solution. Or just don't have both the binary and hand-compiled versions
installed at the same time.</p>
