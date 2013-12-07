---
layout: post
status: publish
published: true
title: Xsession and .bash_profile
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 675
wordpress_url: urn:uuid:ec85da15-4a7a-426b-928d-de91810ea538
date: 2006-07-22 13:19:34.000000000 -07:00
tags:
- linux
- xorg
- x11
- bash
- login
- shell
comments: []
---
<p>Once upon a time I fought the good battle trying to get one of [gkwx]dm to run
a <em>login</em> shell, because you know, we're <em>logging in</em>. I wanted it to run a
login shell so I could run <a href="http://www.gentoo.org/proj/en/keychain/">keychain</a>
or something.</p>

<p>Well today I wanted to figure out how to <em>keep</em> <code>startx</code> from running keychain.
It shouldn't have been running keychain because keychain runs from
<code>.bash_profile</code> which shouldn't be sourced for two good reasons: A) it's not a
login shell (this is a boot script to start freevo), and B) it's not bash,
it's /bin/sh (yes, I know that's really bash but when invoked as sh it doesn't
source <code>.bash_profile</code>). </p>

<p>It turns out some bright kid created <code>/etc/X11/Xsession.d/91source_profile</code> (I
think that's what it was called), that sourced every profile file it could
think of whenever Xsession was run. This is both bad and stupid. It's bad
because sometimes an X session is not a login. It's stupid because they could
have achieved the same thing in a more elegant way by adding <code>--login</code> to the
shebang line of <code>/etc/X11/Xsession</code>. The place to do login shell stuff is where
you actually log in, i.e. [xgkw]dm, not Xsession.</p>

<p>Please, my friends, if you go out into the world and work on something that
involves login and environment, read the manpages and understand what a login
shell, an interactive shell, and a noninteractive nonlogin shell are and when
you want each. Thanks. End of rant.</p>
