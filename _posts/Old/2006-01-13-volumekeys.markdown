---
layout: post
status: publish
published: true
title: Hardware Keys on iBook 10.4.3
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 92
wordpress_url: urn:uuid:c08f3296-acc2-4675-bd7b-c5ecbe447d06
date: '2006-01-13 07:46:44.000000000 -08:00'
tags:
- mac
comments: []
---
<p><em>Update</em>: The same thing just happened on the upgrade to 10.4.4. Again,
shutting down the laptop and cutting all power did the trick. I didn't have to
hold down the power button.</p>

<p>The 10.4.3 "trick or treat" update of OS X Tiger caused my hardware keys
(volume, brightness, power button, and even, oddly, the About This Mac menu
option) to stop working. I tried a few reboots, heard a rumor on /. about the
airport update so updated that, and searched and searched for a solution.
Apparently people with TiBooks have had this trouble since Tiger first came out
and were told, more or less, to wait for 10.4.3. Well maybe whatever they fixed
"broke" things for us iBook G4 users. Or maybe it was something entirely
unrelated. In any case, one of those sites gave a recommendation that I tried
as a second-to-last ditch effort (the last would have been to boot into linux
and see if I could jump-start things from there). Shutdown (you may need to do
this from the command prompt: <code>sudo halt</code>), take out the battery and disconnect
the power, and (for good measure) hold down the power button for one minute.
That last bit may not be necessary but the TiBook people talked about a reset
button that I don't seem to have so I figured it couldn't hurt. When I booted
up, things worked as they should. Phew!</p>
