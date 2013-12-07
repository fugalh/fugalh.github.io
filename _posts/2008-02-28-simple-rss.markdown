---
layout: post
status: publish
published: true
title: Simple RSS
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 940
wordpress_url: urn:uuid:75fc9302-7811-458d-93e5-9157093ad71f
date: 2008-02-28 14:28:22.000000000 -08:00
tags:
- ruby
- src
- rss
- sars
- markdown
- text
- dsl
- yaml
comments:
- id: 1724
  author: Ajit
  author_email: aishwarya_aishwaryaa@yahoo.com
  author_url: http://http;//www.correcty.org
  date: '2008-02-29 01:45:43 -0800'
  date_gmt: ''
  content: <p>hahaha i have found myself in the situation. I always have to do and
    redo things all over again. Thanks for this, very helpful!</p>
---
<p>Have you ever thrown together a simple static webpage, only to find down the road that you want to add an RSS feed? What are your options? Maintain an ugly XML file by hand, or migrate to a big slow messy CMS. Yeah, no fun.</p>

<p><a href="http://hans.fugal.net/src/sars">Sars</a> is a simple RSS domain specific language. This:</p>

<pre><code># This is a YAML stream (http://yaml.org) but you don't need to know much YAML
# to get the hang of it.
# There are multiple "documents". The first document is the channel information:
---
title: Foo News Feed
link: http://example.com/foo/
description: News for the Foo Project
webmaster: you@example.com

# The second and subsequent documents are items. The first line is the title,
# the second line is the date, and the rest is the item description (Markdown).
# Because line endings are important, don't forget the pipe character.
--- |
Really Exciting Title
2/28/08 12:00
This is where I pontificate
about the really exciting fish
that is sitting on my plate.

Here's a [download link](http://example.com/foo/foo-1.0.tar.gz).

--- |
Another Item
2/28/08 12:04
You know, it doesn't really matter what order you put them in, since they each
have dates.
</code></pre>

<p>becomes this:</p>

<pre><code>&lt;?xml version="1.0"?&gt;
&lt;rss version="2.0"&gt;
&lt;channel&gt;
    &lt;title&gt;Foo News Feed&lt;/title&gt;
    &lt;link&gt;http://example.com/foo/&lt;/link&gt;
    &lt;description&gt;News for the Foo Project&lt;/description&gt;
    &lt;lastBuildDate&gt;Thu, 28 Feb 2008 12:07:32 -0700&lt;/lastBuildDate&gt;
    &lt;generator&gt;yaml2rss&lt;/generator&gt;
    &lt;webMaster&gt;&lt;/webMaster&gt;

    &lt;item&gt;
        &lt;title&gt;Really Exciting Title&lt;/title&gt;
        &lt;description&gt;&amp;lt;p&amp;gt;This is where I pontificate
about the really exciting fish
that is sitting on my plate.&amp;lt;/p&amp;gt;

&amp;lt;p&amp;gt;Here's a &amp;lt;a href=&amp;quot;http://example.com/foo/foo-1.0.tar.gz&amp;quot;&amp;gt;download link&amp;lt;/a&amp;gt;.&amp;lt;/p&amp;gt;&lt;/description&gt;
        &lt;pubDate&gt;Thu, 28 Feb 2008 12:00:00 -0700&lt;/pubDate&gt;
        &lt;guid&gt;http://example.com/foo//2008-02-28T12:00:00-07:00&lt;/guid&gt;
    &lt;/item&gt;

    &lt;item&gt;
        &lt;title&gt;Another Item&lt;/title&gt;
        &lt;description&gt;&amp;lt;p&amp;gt;You know, it doesn't really matter what order you put them in, since they each
have dates.&amp;lt;/p&amp;gt;&lt;/description&gt;
        &lt;pubDate&gt;Thu, 28 Feb 2008 12:04:00 -0700&lt;/pubDate&gt;
        &lt;guid&gt;http://example.com/foo//2008-02-28T12:04:00-07:00&lt;/guid&gt;
    &lt;/item&gt;

&lt;/channel&gt;
&lt;/rss&gt;
</code></pre>

<p>Any questions?</p>
