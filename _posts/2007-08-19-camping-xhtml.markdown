---
layout: post
status: publish
published: true
title: Camping XHTML
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 864
wordpress_url: urn:uuid:ef2ad0b6-8269-409c-9aee-72f149105df3
date: '2007-08-19 17:53:16.000000000 -07:00'
tags:
- ruby
- camping
- xhtml
- mathml
comments:
- id: 1604
  author: Don Park
  author_email: don.park@gmail.com
  author_url: ''
  date: '2008-03-02 12:05:34 -0800'
  date_gmt: ''
  content: <p>just what I was looking for! thanks!</p>
---
<p>I have a little <a href="http://camping.rubyforge.org">Camping</a> toy, and I decided to
play a bit with <a href="http://www.w3.org/Math/">MathML</a> to render a few simple
equations. I read <a href="http://www.w3.org/Math/XSL/">the insructions</a> and played
around with a static file and found that all I needed was to use XHTML and
everything would Just Work™. </p>

<p>Until I tried to do it in Camping. I'll spare you the boring details and cut to
the chase:</p>

<pre><code>def layout
  @headers['Content-Type'] = 'application/xhtml+xml'
  xhtml_transitional do
    body { self &lt;&lt; yield }
  end
end
</code></pre>

<p>The trick is getting the MIME type right.</p>
