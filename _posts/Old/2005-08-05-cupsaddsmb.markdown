---
layout: post
status: publish
published: true
title: Coming to Terms with cupsaddsmb
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 43
wordpress_url: urn:uuid:783ef807-3780-4302-9fbf-d604ca16c2b5
date: '2005-08-05 16:10:14.000000000 -07:00'
tags:
- linux
comments: []
---
<p>Adobe Acrobat Reader 7.0 and CUPS windows postscript drivers spooled over Samba
to a CUPS server is the recipe for not getting all pages printed. I'm not sure
who was at fault, although I am prone to blame Adobe. A workaround is to use
Adobe's postscript driver instead of the CUPS one. I'll try the CUPS driver
again when version 6 is released.</p>

<p>Along the road, I picked up a decent understanding of how Windows network
printing works, how Samba works with it, and all the idiosyncrasies of the
black art that is setting up network printing with Samba. At first, my
already-strained relationship with <code>cupsaddsmb</code> was in a nose dive. Here I was
tooling around in rpcclient seeing very long lists of drivers that were all the
same files. If every printer was using the same CUPS (or Adobe) postscript
driver, why have 100+ drivers? At this point I was ready to write my own
slightly intelligent <code>cupsaddsmb</code>.</p>

<p>Then out of the blue I found something in Google Groups that indicated that
each driver should have its own PPD, and that CUPS stores the PPD for each
file. The reason for this is that many options of the sort set with <code>lpoptions</code>
are just stored right there in that PPD. One of the things <code>cupsaddsmb</code> does is
to grab that PPD from CUPS and upload it along with the rest of the CUPS
driver. Well, ok, now I can see a good reason to do all of what <code>cupsaddsmb</code>
does with each printer even though you have almost 50 HP 4000 Series printers
that all use the same PPD, to say nothing of the other printers that use
different PPDs. So <code>cupsaddsmb</code> is off the hook for now. Still, it's not
intelligent to tell me quietly whether each printer succeeded or failed, and
it's an obvious scripting application written in C for crying out loud, so I am
not letting it off parole quite yet.</p>
