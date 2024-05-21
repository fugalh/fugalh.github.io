---
layout: post
status: publish
published: true
title: OSX ignores ownership on external drives by default.
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1223
wordpress_url: http://hans.fugal.net/blog/?p=1223
date: '2010-08-06 14:38:10.000000000 -07:00'
tags:
- linux
- mac
- osx
- rsync
- backup
comments: []
---
I had reason to copy my harddrive off and back (to reformat as case-sensitive), and I missed one very important detail.

http://www.egg-tech.com/mac_backup/

IMPORTANT STEP: disable "Ignore ownership on this volume".

Yeah, with everything owned by user 99, it won't even boot. You can boot into single-user mode and "chown -R root:wheel /" which will at least let it boot, then you can go into Disk Utility and repair permissions (which will actually do something useful and vital in this situation). Then chown -R your home directory. But it's still a mess to clean up, and you lose all that user and group info. 
