---
layout: post
status: publish
published: true
title: Why vimdiff?
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1103
wordpress_url: http://hans.fugal.net/blog/?p=1103
date: '2009-02-13 00:32:04.000000000 -08:00'
tags:
- mac
- git
- vim
- diff
- mergetool
- merge
- vimdiff
- opendiff
- filemerge
comments:
- id: 2131
  author: Mike Lewis
  author_email: mikelikespie@gmail.com
  author_url: http://lolrus.org
  date: '2009-09-24 08:24:47 -0700'
  date_gmt: '2009-09-24 08:24:47 -0700'
  content: I can't find 3-way features with opendiff. I do like vimdiff as well. For
    3-way diffs I found kdiff3 to be the best, once you get used it's wonky interface
---
I love Vim and vimdiff, but vimdiff is pitiful for doing 3-way merges. So I wonder why git's search for a merge tool prefers vimdiff over opendiff (which launches OS X's fantastic FileMerge program).

<code>git config --global merge.tool opendiff</code>
