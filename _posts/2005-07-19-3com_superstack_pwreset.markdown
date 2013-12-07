---
layout: post
status: publish
published: true
title: Password Recovery on 3COM SuperStack Switches
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 32
wordpress_url: urn:uuid:2fe35cb1-1219-4d3e-8dcf-94e2c98e4289
date: 2005-07-19 10:32:00.000000000 -07:00
tags:
- linux
comments: []
---
<p>Google has some answers, some of which are bogus and some of which don't apply
to all switches. It's a lot easier than Google would make it seem, though, if
you have one switch with a known password and a management module. Just stack
up the other switches, log into the management one, and do <code>system initialize</code>.
That will initialize the whole stack (reset to factory defaults, including
password but <em>not</em> including IP addresses). If initializing isn't your cup of
tea, I <code>system password</code> will reset the passwords on the whole stack as well.
(Hint: verify the stack is what you think it is with <code>system inventory</code>)</p>
