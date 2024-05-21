---
layout: post
status: publish
published: true
title: Initialize a remote git repository
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1097
wordpress_url: http://hans.fugal.net/blog/?p=1097
date: '2009-02-12 18:12:41.000000000 -08:00'
tags:
- git
- init
- rsync
- revision control
- revision
- mirror
- push
- bare
- clone
comments:
- id: 1836
  author: philip
  author_email: phil@orsa-studio.com
  author_url: http://www.philipandrew.com
  date: '2009-02-14 08:57:31 -0800'
  date_gmt: '2009-02-14 08:57:31 -0800'
  content: "Ok read it.\r\n\r\nInteresting.... but .... I'm going to go back to Subversion.
    I *think* git is good for smart people who know what they are doing and are reasonably
    independent, junior programmers are going to struggle with it, branching is difficult
    even for most junior programmers to handle.\r\n\r\nI have to write software with
    senior and junior programmers, so I'm going to go for the lowest common denominator."
- id: 1879
  author: Jon
  author_email: jon.mayo@gmail.com
  author_url: http://orangetide.com/
  date: '2009-03-01 23:17:18 -0800'
  date_gmt: '2009-03-01 23:17:18 -0800'
  content: "Subversion might seem easy at first, and branching in git might not be
    intuitive to new users. But the difference in being able to merge branches is
    like night and day between svn and git. Doing any sort of non-trivial branch collapse
    in svn is way beyond a junior programmer's abilities and they are more likely
    to create bugs or lose changes than successfully complete an svn merge. Merging
    in git is relatively painless compared to the other systems I've used (cvs, svn,
    p4, clearcase).\r\nThe draw to svn is that everything is a directory, but given
    that junior programmers almost never attempt to branch I think this feature is
    overrated. tags are better in CVS than in svn. and both tags and branches are
    fairly simple in git, once you let go of the idea that encoding all meta data
    into an URL is not the best approach."
- id: 1928
  author: piotr
  author_email: kopszak@gmail.com
  author_url: http://okle.pl
  date: '2009-04-03 20:17:52 -0700'
  date_gmt: '2009-04-03 20:17:52 -0700'
  content: I'm getting error "not a valid remote name" after  "git remote add --mirror  ..."
    Can you give examples of valid ones?
- id: 1929
  author: piotr
  author_email: kopszak@gmail.com
  author_url: http://okle.pl
  date: '2009-04-03 20:23:47 -0700'
  date_gmt: '2009-04-03 20:23:47 -0700'
  content: OK, read the man page. Anyway, it's misleading when you write bar bar:repo
- id: 1930
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-03 20:24:15 -0700'
  date_gmt: '2009-04-03 20:24:15 -0700'
  content: Any valid remote repository. For example, if you have a github project
    it might be "git remote add --mirror foo git@github.com:mygithubusername/mygithubproject.git"
- id: 1931
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-03 20:29:31 -0700'
  date_gmt: '2009-04-03 20:29:31 -0700'
  content: You can call it whatever you want, the name of the host is a logical name.
    You could write "git remote add --mirror repo_on_bar bar:repo"
- id: 2359
  author: Ryan
  author_email: ryan@rsgalloway.com
  author_url: http://rsgalloway.com
  date: '2011-01-31 23:31:52 -0800'
  date_gmt: '2011-01-31 23:31:52 -0800'
  content: "\"Ideally, git would have an option to push that instructs it to initialize
    the remote repository and just do the right thing\"\r\n\r\nI've been looking for
    a way to do this also. Is this possible yet?"
---
So you create a git repository (<code>repo</code>) on your local machine (<code>foo</code>) and begin hacking away. Then, you want to push a backup copy of that repo to another box (<code>bar</code>). What's the best way to do that? There are many ways to do it, but some ways are dangerous and some are just cumbersome.

Ideally, git would have an option to push that instructs it to initialize the remote repository and just do the right thing. I hope this is in our future, but for now we have to do some dancing around.

The canonical way is
<code>bar:~/repo$ git clone --mirror local:repo
...
foo:~/repo$ git push bar:repo --mirror</code>
but that's not always feasible due to firewalls and nasty NATs.

Unwise methods include copying the working tree with rsync or scp, doing something like the above without <code>--bare</code> or <code>--mirror</code> (which implies <code>--bare</code>), and other methods that would have you pushing to a non-bare repository.

The best method I've found is this:
<code>bar:~$ git --git-dir=repo init --bare
foo:~/repo$ git remote add --mirror bar bar:repo
foo:~/repo$ git push bar
...</code>

We set up a bare repository on bar, then set up a "remote" for bar which automatically mirrors (you could do that with the canonical method described above too), so it sends the whole shebang. After that, we push as we normally would.
