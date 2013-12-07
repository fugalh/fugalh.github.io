---
layout: post
status: publish
published: true
title: Camping Logmarks
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 11
wordpress_url: urn:uuid:fa78ad59-4942-4f57-b27e-4b9521b3174c
date: 2006-02-24 13:14:13.000000000 -08:00
tags:
- cs
comments: []
---
<p>I quickly ran some unscientific bench^Wlogmarks (3 or 4 samples after
stabilization at the CLI with my friend <code>time</code>) for camping vs. just erb/cgi
vs. just markaby vs. my current blosxom blog (with 10 entries):</p>

<pre><code>time ruby -rrubygems -e "require 'camping'"  # about 0.5 seconds
time ruby -rcgi -rerb -e ""                  # about 0.05 seconds
time ruby -rrubygems -e "require 'markaby'"  # about 0.2 seconds
time blosxom.cgi &gt;/dev/null                  # just under 0.3 sec
time fugue.rb &gt;/dev/null                     # just over 1 sec
</code></pre>

<p>The blosxom and fugue runs dealt with the same 10 posts and produce almost to
the angle-bracket the same HTML. It looks like to me that I should think about
doing my super-simple blog without the overhead of a framework, even one as
small as camping, and go with straight markaby or erb for the template. </p>

<p>Camping does fine once it's loaded, but I don't really want 20 megabytes of
virtual memory being wasted just so the 5 people out there reading my blog can
get it in less than two seconds. As it is I'm trying to find ways to prune
rails/apache/etc. memory usage. I think I have an idea, too.</p>

<p>So apparently a lot of this time is startup time, but a lot of the time this
startup stuff is the same over and over. I started thinking about one master
process that somehow subthreads the rails/camping sites, but that gets messy
and who knows when a global variable or some other rogue will really mess
things up. Not to mention environment. But wait, I don't care about memory
usage when it's actually doing something - it's the perpetual waste of RAM that
I'm concerned about. Why don't I have N bootstrap processes that have done the
equivalent of <code>require 'rails'</code> or <code>require 'camping'</code> and are ready to <code>load</code>
the appropriate ruby script on-demand and then die gracefully after the page is
served. I get precise control over how many processes are hanging around, the
wasted RAM between requests is much less per lingering process than with a
full-blown fastcgi app, and you get fast service. </p>

<p>Well, there's at least one problem: most page loads will have a bunch of
requests all at once, so maybe it would be better to have the bootstrap process
load up a fastcgi process that can serve the rest of the requests and die after
a few seconds of idle time.</p>

<p>If you have thoughts on this scheme, let me know. Yeah, I know I don't have
comments, so you'll have to do it the old-fashioned way. If my subconcious
doesn't churn something up in the next few days/weeks I might just whip it up.</p>
