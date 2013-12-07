---
layout: post
status: publish
published: true
title: Observations in Data Models
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1116
wordpress_url: http://hans.fugal.net/blog/?p=1116
date: '2009-03-04 23:08:52.000000000 -08:00'
tags:
- family
- genealogy
- evidence
- history
- gedcom
- model
- data
- gdm
- martin
- fowler
- observation
- familysearch
comments: []
---
Martin Fowler has an <a href="http://martinfowler.com/bliki/ContradictoryObservations.html">excellent article</a> on contradictory observations and data models, which I think should be required reading for everyone who even <em>thinks</em> about writing genealogical software.

I had never thought about the specific examples that he brings up in the health care profession, though they make perfect sense. I have thought about these very issues quite a bit in the realm of genealogical data and it is my firm belief that software that doesn't allow for building up a "web of belief" from evidence (or observations as he calls them here)—including contradictory and rejected evidence—is fundamentally broken. That means almost every piece of genealogical software ever written. Certainly all of the commercial ones. Thankfully we're seeing some progress on this front. The new.familysearch.org site gets us part of the way there—you have separate observations that are merged and disputed and give a view of the data. Unfortunately there are still holes in the conclusions drawn from observations, especially contradictory ones. Hopefully this will get worked out, so that if I have solid evidence that rejects someone else's entry (which may have been based on no evidence at all, or weak evidence), the view should update to reflect that automatically. Likewise, if I have weak evidence that contradicts someone else's strong evidence, it should by no means change the view to my new data, but I should be able to record it for posterity (that rejection is important to record so that when someone else stumbles on the same weak evidence they can see that it was given full consideration). Also the new.familysearch.org merging stuff is both not transparent enough and too transparent—you have to really dig to figure out where each bit of data came from and yet every single alternate spelling or date is right there in your face whether the differences are important or not. But these issues are things that can incrementally improve. The important thing is that they're fundamentally on the right track.

I have a book on genealogical evidence (thanks Mom!) that I'm reading. When I finish it I plan to pontificate in depth about data models and genealogy, and maybe even put some code where my mouth is.
