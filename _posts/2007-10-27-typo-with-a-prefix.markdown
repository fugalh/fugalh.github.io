---
layout: post
status: publish
published: true
title: Typo with a Prefix
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 887
wordpress_url: urn:uuid:24e05b25-28a7-4ab7-bdab-958d1d890d51
date: 2007-10-27 22:06:26.000000000 -07:00
tags:
- typo
comments: []
---
<p>I just set up <a href="http://typosphere.org">Typo</a> again, for my <a href="http://erin.fugal.net/blog">wife's blog</a>. She wanted the url <a href="http://erin.fugal.net/blog">http://erin.fugal.net/blog</a>, the important part here is the <code>/blog</code> bit at the end. Rails in general has traditionally been fairly hostile to this prefix thing, but Typo has smoothed things out considerably. I've blogged about this before, but typo has changed in the meantime. Here's what you do:</p>

<p>First, in your Apache2 config change the <code>ProxyPass</code> and <code>ProxyPassReverse</code> lines to have <code>/blog</code> in both places, e.g. </p>

<pre><code>ProxyPass             /blog http://localhost:4907/blog
ProxyPassReverse      /blog http://localhost:4907/blog
</code></pre>

<p>Then, tell typo about it:</p>

<pre><code>cd /path/to/my/typo
typo config . prefix-url=/blog
typo restart .
</code></pre>

<p>Finally, you may need to flush the cache and/or reactivate the theme of your choice. </p>

<p>Kudos to the typo folks for making this relatively painless. Getting it to work in the "good ol' days" was truly painful.</p>
