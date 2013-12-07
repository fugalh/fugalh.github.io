---
layout: post
status: publish
published: true
title: Grab Conference with Hpricot
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 954
wordpress_url: urn:uuid:1ad9ae39-9b51-4447-9643-cba12b84d965
date: 2008-04-07 06:43:52.000000000 -07:00
tags:
- ruby
- hpricot
- scraping
- lds
comments: []
---
<p>So you slept through a few sessions of conference (or you were distracted by the computer or stuck in the bathroom with a potty training toddler). The natural thing to do is to listen to sessions one at a time on your mp3 player over the next week or two. But it would be too much work to go to <a href="http://www.lds.org/conference/sessions/display/0,5239,49-1-851,00.html">the archives website</a> every day to download the appropriate session, then sync your mp3 player. No, you need to download them all now. But clicking on each one is tedious at best.</p>

<p>Enter a script. Now I've done something like this in the past with just sed and grep, but this time I thought I'd skip the sed trial and error and practice some <a href="http://code.whytheluckystiff.net/hpricot/">Hpricot</a>. It was quick and painless:</p>

<pre><code>require 'rubygems'
require 'hpricot'
require 'open-uri'
CONFERENCE_URL="http://www.lds.org/conference/sessions/display/0,5239,49-1-851,00.html"
doc = Hpricot(open(CONFERENCE_URL))
puts (doc/"a").map{|a| a['href']}.join("\n")
</code></pre>

<p>That little script extracts all the urls from a URL. Well maybe there's a program that does that already. Maybe it's urlview, but an impatient google didn't find it in time (and urlview isn't installed on my laptop). Now you continue on with the grep magic:</p>

<pre><code>./strip_urls.rb | grep mp3 | grep -v Complete | xargs wget
</code></pre>

<p>And you're on your way.</p>
