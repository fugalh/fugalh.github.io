---
layout: post
status: publish
published: true
title: git whereami
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1173
wordpress_url: http://hans.fugal.net/blog/?p=1173
date: '2009-09-03 16:49:28.000000000 -07:00'
tags: []
comments: []
---
<em>Update:</em> I added <code>git branch -a</code> so that you can actually see where you are, and <code>--since='2 months'</code> so if your repo is huge like mine it doesn't take 2 seconds to run. (The actual value of <code>--since</code> will probably need tweaking for your situation.)

Here's the awesome git trick of the day:
<code>
# in ~/.gitconfig
[alias]
    w = !git branch -a && git log --branches --oneline --graph --decorate --simplify-by-decoration --since='2 months ago'
</code>

<code>
$ git w
* 0bfd287 (refs/remotes/git-svn, refs/heads/foo) commit message 
| * 0b5d8d4 (refs/heads/bar) another commit message
|/  
| * 575185a (refs/heads/baz) YACM
|/  
* b98de6b (refs/remotes/origin/master, refs/remotes/origin/HEAD) YACM
* eadfbbe initial commit message
</code>

If you're lucky enough to have a recent version of git, the <code>--decorate</code> option doesn't print out the boring <code>refs/{remotes,heads}</code> stuff by default.
