---
layout: post
status: publish
published: true
title: On Dependencies
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 44
wordpress_url: urn:uuid:2129b5a8-dc65-4673-8cb8-0db3246770cb
date: '2005-11-27 19:20:46.000000000 -08:00'
tags:
- linux
comments: []
---
<p>I had a hankering to organize my music collection, so I went out on the prowl again. I came across <a href="http://users.otenet.gr/~jtcliper/tgf/">The GodFather</a> and had gotten excited enough to try it out when I realized it was a Windows program. It just goes to show I'm not used to 'shopping' for freeware that is useful to the masses, that I automatically assumed a program with a cool name and icon <em>must</em> be a Linux project. (Although, the icon farm at the bottom should have tipped me off)</p>

<p>I was feeling real adventurous, so I wandered over to the <a href="http://musicbrainz.org/">MusicBrainz</a> website to check on the status of <a href="http://musicbrainz.org/wd/PicardDownload">Picard</a>. Picard looks like a very cool program, or at least one worth trying out, but I have not yet succeeded in getting it to work, which brings us to the subject.</p>

<p>The problem is dependencies. Picard relies on very specific versions of programs and libraries, most of which are not in Debian. I gather from the INSTALL file that they're not in any distro. Add to that stale instructions and build errors in some of the dependencies (perhaps due to the stale instructions), and you have a real nightmare. Picard is still in development, so I can understand that easy installation is not yet on the radar, but I have to wonder how he expects people to use this program when he is done. Is he expecting development to take long enough that distros will catch up with the dependencies? Will he distribute statically-linked binaries? What about Windows users (his primary target, thus far) that aren't used to command lines and compiling stuff?</p>

<p>I think we simply have different philosophies, and I'm not saying his is wrong. I just was thinking about it and decided to blog it. If I am writing something that I'd like people to use, I go out of my way to minimize dependencies. My rule of thumb is, if it's in Debian testing or stable, I'm pretty safe. (Insert dinosaur jokes here.) This isn't always possible, especially when using less-mainstream languages (e.g. ruby) or libraries (e.g. a lot of audio stuff). It becomes even harder when you want to use cross-platform GUI toolkits, but hopefully that will stabilize soon. But then I see projects like Picard which are living on the bleeding edge and I see that my philosophy is not the same one held by others. I can only hope it works out for them, and that eventually I can run the software they produce.</p>
