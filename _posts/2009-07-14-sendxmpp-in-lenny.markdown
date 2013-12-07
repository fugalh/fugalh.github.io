---
layout: post
status: publish
published: true
title: sendxmpp in Lenny
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1162
wordpress_url: http://hans.fugal.net/blog/2009/07/14/sendxmpp-in-lenny
date: 2009-07-14 16:31:58.000000000 -07:00
tags:
- debian
- jabber
- psi
- libpurple
- pidgin
- gaim
- lenny
- sendxmpp
- xmpp
comments: []
---
sendxmpp in Debian Lenny doesn't work properly with Pidgin or Adium. I don't know if it's a libpurple problem or a sendxmpp problem. sendxmpp can talk to Psi ok. Upgrading sendxmpp to the version in Sid fixes the problem. The difference seems to be that now sendxmpp is sending messages of type "chat" instead of type "message" or "normal" (by default—now you can specify which message type to use). But Psi can send "message" messages to libpurple clients ok, so it doesn't seem to be quite that simple. 
