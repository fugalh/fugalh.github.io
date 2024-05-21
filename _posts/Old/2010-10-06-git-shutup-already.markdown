---
layout: post
status: publish
published: true
title: Git shutup already
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1231
wordpress_url: http://hans.fugal.net/blog/?p=1231
date: '2010-10-06 19:27:34.000000000 -07:00'
tags:
- cs
- git
- ignore
- .gitignore
comments: []
---
So you have a bunch of local files you don't want to check in and you also don't want to add to the project's official .gitignore file(s)? Solution: edit .git/info/exclude. I like to make a symlink e.g. "ln -s .git/info/exclude .gitignore.local".

Thanks GitHub. http://help.github.com/git-ignore/
