---
layout: post
status: publish
published: true
title: Samsung Printer
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 683
wordpress_url: urn:uuid:2493376b-8898-420c-8ecd-28190c39adb6
date: 2006-07-27 16:43:00.000000000 -07:00
tags:
- linux
- review
- samsung
- printer
- cups
- sane
- scx
- '4100'
comments: []
---
<p>My old Deskjet 712C bit the dust (it's probably still fixable to some degree if
you're interested), and my wife has never been pleased with the
partially-working scanner we got from who-knows-where, so we broke down and got
a <a href="http://www.samsung.com/Products/PrinterandMultifunction/DiscontinuedProducts/SCX_4100XAA.asp">Samsung
SCX-4100</a>
monochrome laser printer+scanner/copier. </p>

<p>We didn't just pick this out of the blue of course, I did some research on what
would be a good but affordable printer for linux. First stop,
linuxprinting.org's <a href="http://linuxprinting.org/suggested.html">suggested printers
page</a>. This printer wasn't mentioned
by name, but they did recommend Samsung laser printers as a possibility. This
printer was available and the price was right on NewEgg, so I googled a bit and
found <a href="http://hathawaymix.org/Weblog/2005-07-15">Shane's post</a> and the many
helpful comments. What a small world. The comments got more and more
encouraging as the page (and time) wore on, and I concluded that it would be a
good printer for linux.</p>

<p>It arrived maybe half an hour or an hour ago, and it's already working
perfectly as a printer, scanner, and copier. Anyone who's fussed with printing
in UNIX before will confirm that this is very good indeed. I ran Samsung's
latest drivers for linux installer (dated 2006-07-19) and it installed without
a hitch. I then replaced the <code>/usr/bin/lpr</code> symlink back to the original
non-GUI version. That's it. No Qt problems, no messing with kernel modules (I'm
using USB, parallel may be a different story). </p>

<p>I'm running Debian testing (etch) and a vanilla 2.6.14 kernel.</p>

<p>Kudos to Samsung for recognizing and supporting linux, and for providing good
drivers (after some growing pains), and kudos to Samsung for making a
multifunction laser that's affordable. </p>
