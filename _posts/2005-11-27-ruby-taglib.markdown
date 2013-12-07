---
layout: post
status: publish
published: true
title: ruby-taglib on Debian
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 8
wordpress_url: urn:uuid:0337522f-0c51-486a-b5b8-b116058616cd
date: 2005-11-27 22:19:31.000000000 -08:00
tags:
- audio
comments: []
---
<p><a href="http://www.hakubi.us/ruby-taglib/">Ruby-taglib</a> works great on Debian. Grab
<a href="http://mahoro.rubyforge.org/">Mahoro</a> (which also looks very handy) and follow
the instructions. Then grab ruby-taglib and do <code>sudo ruby setup.rb</code>. </p>

<p>The only thing to watch out for is that ruby-taglib requires the <em>C</em> bindings
to taglib, which are in a separate debian package. You want libtagc0-dev, not
just libtag1-dev.</p>

<p>Taglib is extremely cool, and is going to assist me in reorganizing my music
collection. I'll try to remember to bore you with the details once I'm done.</p>
