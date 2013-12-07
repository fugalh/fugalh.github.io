---
layout: post
status: publish
published: true
title: Tempfile, persist!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 129
wordpress_url: urn:uuid:c97ca3f0-66d4-43d8-ab8d-8f4b5f7084d9
date: 2006-05-12 20:00:42.000000000 -07:00
tags:
- ruby
- tempfile
- mktemp
- persist
comments: []
---
<p>The Ruby <a href="http://www.ruby-doc.org/stdlib/libdoc/tempfile/rdoc/index.html">Tempfile
class</a> is a
really nifty class for using temporary files:</p>

<pre><code>tmp = Tempfile.new('foo')
tmp.write template
tmp.close
system ENV['EDITOR'], tmp.path
</code></pre>

<p>It's even considerate enough to remove the tempfile when your program
terminates. The trouble is, I didn't want it to remove the tempfile always.
Sometimes I want to tell it to persist. This is handy when you want to not
simply discard all the user's hard work when an error occurs. The fix is
simple:</p>

<pre><code>class Tempfile
  def persist
    ObjectSpace.undefine_finalizer(self)
  end
end
</code></pre>

<p>I love open classes.</p>
