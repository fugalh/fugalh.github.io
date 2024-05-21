---
layout: post
status: publish
published: true
title: git-push is worse than worthless
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1020
wordpress_url: urn:uuid:f13008b3-a922-4c91-a454-67c82a3877d1
date: '2008-11-10 17:00:00.000000000 -08:00'
tags:
- git
- darcs
- usability
- hg
- mercurial
- push
- pull
- surprising
- bad
- unusable
- evil
comments:
- id: 1789
  author: Mike Moore
  author_email: mike@blowmage.com
  author_url: http://blowmage.com
  date: '2008-11-10 18:10:25 -0800'
  date_gmt: ''
  content: |-
    <p>I don't think I follow 100%. Can't you just rebase, resolve your conflicts if neccessary, and then push?</p>

    <p>I'm not entirely sure why you would push from one local repo to another local repo.</p>
- id: 1790
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-11-10 19:18:54 -0800'
  date_gmt: ''
  content: |-
    <p>Hi Mike,</p>

    <p>The example is local just to demonstrate, because it was easier to record (using <code>script</code>) the example and behaves the same way.</p>

    <p>In the real world, I ended up having to muck with the index to get git to forget about the undo changes, then do a revert. I think this is because on the server an older version of git (1.4 vs 1.6 here) is behaving slightly different from what you see in my example. A rebase might also work as a way to dig yourself out of the hole if you accidentally do this.</p>

    <p>The big deal isn't that push behaves this way. It's a design choice, and one I can live with. But it's a counterintuitive choice for people coming from other DRCSes, and so it warrants at least a warning in the man page and preferably a refusal to screw up your working copy (without a --force).</p>
- id: 1791
  author: Eric Drechsel
  author_email: xerdcire@gmail.com
  author_url: http://oheric.com
  date: '2008-11-12 02:55:30 -0800'
  date_gmt: ''
  content: |-
    <p>Don't sad codemonkey!
    This feature (it is a feature) puzzled me for awhile too. As a web dev it's very useful to push your local (laptop) changes to a live copy on a server, but the remote origin working copy doesn't update.</p>

    <p>Check out <a href="http://git.or.cz/gitwiki/GitFaq#head-b96f48bc9c925074be9f95c0fce69bcece5f6e73" rel="nofollow">http://git.or.cz/gitwiki/GitFaq#head-b96f48bc9c925074be9f95c0fce69bcece5f6e73</a> for a solution. Download the post-update hook to $REPO/.git/hooks and chmod +x it. Now the working copy gets updated!</p>
- id: 1792
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-11-12 07:58:31 -0800'
  date_gmt: ''
  content: |-
    <p>That's a good link, thanks. I think I would like to make two points in response to your comment. First, yes it is useful as a web developer, but also in many other normal situations. I realize it doesn't really come up in kernel development (where they send patches by email) but that doesn't make it an irrelevant way to work for many development situations, not just web development (which is a kind of minority discriminated against by many "serious" programmers, and nothing is more "serious" than kernel development).</p>

    <p>The second thing I disagree with is that it's a feature. The feature is that they don't want to update the working directory because they don't know if they can safely do that. That's ok. Mercurial does the same thing—you have to update your working directory manually (or set up a hook). Darcs takes a slightly different but just as safe approach: it refuses to do the push if it's not safe. Either way, no big deal.</p>

    <p>Where git gets it wrong is by yanking the HEAD out from under the working directory and replacing it with a different HEAD, without updating the working directory and without warning the user.</p>

    <p>I have heard a few times that "push is the mirror of fetch". I encourage you to try <code>git fetch</code> followed by a <code>git status</code> and see if your working directory is now out of whack. It's not, because you have to manually merge the fetch (which updates your working directory) with <code>git merge FETCH_HEAD</code>. If git push used a <code>PUSH_HEAD</code>, that would be a mirror operation, and I would not consider it broken in any way.</p>
- id: 1793
  author: Hanno
  author_email: ''
  author_url: ''
  date: '2008-12-03 12:49:39 -0800'
  date_gmt: ''
  content: <p>Thanks for this. I was wondering about whats going on for a while. I
    agree that this is more like a bug than a  feature. </p>
- id: 1824
  author: Ron
  author_email: b0b0b0b@gmail.com
  author_url: ''
  date: '2009-02-05 17:56:08 -0800'
  date_gmt: '2009-02-05 17:56:08 -0800'
  content: Your updated update is the workflow I follow.  Thanks for the write-up.
- id: 1831
  author: Dmitrii 'Mamut' DImandt
  author_email: dmitrii@dmitriid.com
  author_url: http://dmitriid.com/
  date: '2009-02-11 14:24:02 -0800'
  date_gmt: '2009-02-11 14:24:02 -0800'
  content: Thank you! That' exactly what I needed!
- id: 1833
  author: philip
  author_email: phil@orsa-studio.com
  author_url: http://www.philipandrew.com
  date: '2009-02-14 03:23:36 -0800'
  date_gmt: '2009-02-14 03:23:36 -0800'
  content: "I'm trying to understand this.\r\n\r\nI have a client machine A and server
    machine B, I want to send my client changes to my server.\r\nMy client A can only
    connect to my server, so I tried git push to send the changes up, it didn't work,
    then I read your article and felt more lost...........\r\nI try to read it again."
- id: 1834
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-02-14 03:47:19 -0800'
  date_gmt: '2009-02-14 03:47:19 -0800'
  content: Philip, see also http://hans.fugal.net/blog/2009/02/12/initialize-a-remote-git-repository
- id: 1835
  author: philip
  author_email: phil@orsa-studio.com
  author_url: http://www.philipandrew.com
  date: '2009-02-14 08:47:23 -0800'
  date_gmt: '2009-02-14 08:47:23 -0800'
  content: "Well I read your article on the bus, now I got it - its amazingly stupid
    because everyone is going to think that git push is going to put my stuff across
    to the other machine and then some command on the other machine is going to re-integrate
    those changes back into the files.\r\n\r\nSomeone just set a trap for 10 thousand
    newbies to git.\r\n\r\nI'm a subversion person, so I'm trying to work out whether
    to move over to git.... let me look at your other article."
- id: 1890
  author: henry
  author_email: ''
  author_url: ''
  date: '2009-03-02 22:19:30 -0800'
  date_gmt: '2009-03-02 22:19:30 -0800'
  content: I feel your pain. I hate this so-called feature as well. a coworker said
    my best bet is to create a bare repo in server, and then push my local repo on
    my laptop to it, and then have a working tree on the server pull from the bare
    repo. seems like a lot of work for something that seem to be logically trivial...
    :(
- id: 1891
  author: Jeff
  author_email: jbell60@cox.net
  author_url: ''
  date: '2009-03-03 09:16:53 -0800'
  date_gmt: '2009-03-03 09:16:53 -0800'
  content: Thanks for this write-up.  This was the final (famous last words) setup
    that I needed to get my laptop setup for development.  I'm running ubuntu on virtual-box,
    and I'm using git and ssh to update my django site on Dreamhost.  Thanks, man!
    Now I can develop anytime anywhere!
- id: 1892
  author: Jacques
  author_email: jthomas@cs.purdue.edu
  author_url: ''
  date: '2009-03-04 09:19:47 -0800'
  date_gmt: '2009-03-04 09:19:47 -0800'
  content: "Eric: thanks for the heads up warning, and the updates.\r\n\r\nHans: thanks
    for the link.\r\n\r\nThe whole story finally made sense when reading:\r\nhttp://git.or.cz/gitwiki/GitFaq#push-is-reverse-of-fetch\r\n\"Reverse\"
    is not the most adequate term.\r\n\r\nIt's funny how the \"updated update\" ends
    up implicitly rebuilding a centralized solution."
- id: 1900
  author: Room for Sk3pticism &raquo; Setting up git/ssh server w/gitosis in Debian
    5.0
  author_email: ''
  author_url: http://www.sk3ptik.net/blog/?p=256
  date: '2009-03-11 22:32:53 -0700'
  date_gmt: '2009-03-11 22:32:53 -0700'
  content: '[...] Git push is worse than worthless [...]'
- id: 1906
  author: Tijn
  author_email: tijn@soocial.com
  author_url: http://tijnschuurmans.nl
  date: '2009-03-18 20:04:39 -0700'
  date_gmt: '2009-03-18 20:04:39 -0700'
  content: Ah, so it seems it wasn't me doing something wrong. I was bitten by this
    'feature' yesterday. Thanks for writing it out in detail! Now I have some good
    starting points to figure out the correct workaround for my special case.
- id: 1952
  author: www.rzr.online.fr
  author_email: www.rzr.online.fr
  author_url: http://rzr.online.fr
  date: '2009-04-23 22:54:42 -0700'
  date_gmt: '2009-04-23 22:54:42 -0700'
  content: "I wonder if there is some hacks to emulate  a : git update command ?\r\nSince
    update the keyword is not used , what would you suggest it do ?\r\n\r\n-- \r\nhttp://rzr.online.fr/q/git"
- id: 1960
  author: Daniel
  author_email: daniel.keep@gmail.com
  author_url: ''
  date: '2009-04-28 12:17:49 -0700'
  date_gmt: '2009-04-28 12:17:49 -0700'
  content: Thanks very much for this; I was wondering exactly how I should push changes
    from my laptop to my desktop.  I ended up going with an incoming branch, since
    it's pretty simple and it seems to work well.
- id: 1964
  author: Dave Kapp
  author_email: davekapp@gmail.com
  author_url: ''
  date: '2009-04-29 05:21:10 -0700'
  date_gmt: '2009-04-29 05:21:10 -0700'
  content: "I spent an hour or so agonizing over what was going on here as well. I
    like almost everything about Git, but this is -really- unintuitive.\r\n\r\nIf
    I'm reading everything correctly, what is happening is that HEAD is \"silently\"
    being changed underneath you, but your altered working tree files aren't affected.
    Thus, it looks like Git wants to undo everything that was just pushed. Does that
    sound right?\r\n\r\nIf that's the case, can you just \"update\" by doing a git
    checkout HEAD -f ? Or would that have side effects I'm not seeing?"
- id: 1966
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-29 13:59:50 -0700'
  date_gmt: '2009-04-29 13:59:50 -0700'
  content: Dave, you've got it right. Yes, you can update with git checkout or git
    reset. The caveat is if you've made changes to your local working directory (or
    make changes after the push but before doing the reset to the new HEAD), you would
    lose those changes.
- id: 1990
  author: Samuel
  author_email: kc5tja@arrl.net
  author_url: ''
  date: '2009-05-20 23:01:38 -0700'
  date_gmt: '2009-05-20 23:01:38 -0700'
  content: "Strangely enough, it is precisely because of this issue that I moved AWAY
    from Git towards Mercurial.  (That, and Windows performance issues.)\r\n\r\nI've
    never been happier."
- id: 2012
  author: Noxius
  author_email: ''
  author_url: ''
  date: '2009-06-02 07:11:09 -0700'
  date_gmt: '2009-06-02 07:11:09 -0700'
  content: "Hmm i don't understand this post, because if you push to origin, origin
    is NOT updated, so live webpage is not affected. You have to reset --hard HEAD
    if you want see this changes, but you will loose all your changes on live webpage,
    better solution is to create another branch on live webpage push there any changes
    and use git merge on live webpage ... so you have all changes under control\r\n\r\ni
    love git, because ist extremly fast compere to svn or any other version system
    ... with project of about 100 000 code lines is realy fast. i had headache with
    svn on that project, git solve my problem, the speed, the easy way to find bug
    code, the size of repository (svn was huge after some time), the git grep (excelent
    function if you want find some string in code).\r\n\r\nBye"
- id: 2099
  author: Brandon Thomson
  author_email: gravix@gmail.com
  author_url: http://www.bthomson.com
  date: '2009-09-04 02:08:05 -0700'
  date_gmt: '2009-09-04 02:08:05 -0700'
  content: I got bitten by this too just now... Very annoying, ended up having to
    throw some local changes away to get the repo back to a sane state :(
- id: 2114
  author: David Frech
  author_email: david@nimblemachines.com
  author_url: http://notes.nimblemachines.com
  date: '2009-09-13 06:06:02 -0700'
  date_gmt: '2009-09-13 06:06:02 -0700'
  content: "I agree that the docs for git push are misleading, and Git certainly doesn't
    warn you if you're doing anything \"stupid\". I did exactly the same thing when
    I was learning Git - I pushed to a repo on another machine that had a checked-out
    tree, and was confused when I did \"git status\" on the remote.\r\n\r\nSome comments:\r\n\r\n(1)
    Since git push only transfers objects and moves the remote head (it doesn't touch
    the index or the working tree - how could it? since a bare repo has neither) -
    you should be able to recover by doing a \"git reset --soft HEAD^\" - which will
    back up one commmit (the one accidentally pushed) and leave the index and tree
    alone.\r\n\r\n(2) \"git fetch thathost\" - the way we bring new objects and heads
    (from thathost) into a repo (on thishost) that has an index and a working tree
    - only ever updates heads in thishost's refs/remotes/thathost/* - not in refs/heads/*.
    So the \"opposite\" command - \"git push thathost\" - assuming thathost also contains
    a working tree and index - should update thathost's refs/remotes/thishost/* heads
    - and not its refs/heads/*. I've done this _lots_ and it works great.\r\n\r\nOf
    course, if you set up a remote using \"git remote add\" it sets up to push by
    default into thathost's refs/heads/* - tacitly assuming the remote to be a bare
    repo.\r\n\r\n(3) \"git init\" should add a hook that refuses pushes to refs/heads/*.
    We only ever push this way into --bare repos.\r\n\r\nAnd perhaps \"git remote
    add\" should ask if the remote is bare or not.\r\n\r\nDoes that all make sense?"
- id: 2116
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-09-13 18:20:51 -0700'
  date_gmt: '2009-09-13 18:20:51 -0700'
  content: "David, excellent points all. I am now fully convinced that the proper
    thing for git push to do is as you outlined in (2).\r\n\r\nThankfully, recent
    versions of git are much more proactive about warning you about this, and require
    you to confirm that you really want to unwisely push to a working directory."
- id: 2122
  author: Gary
  author_email: garyo@genarts.com
  author_url: ''
  date: '2009-09-20 01:02:51 -0700'
  date_gmt: '2009-09-20 01:02:51 -0700'
  content: I juts got the warning about this and googled around and found this post.  I
    totally agree that this is broken.  I already have enough trouble keeping track
    of all the git repos that might have changes, this just means everyone needs yet
    another one on their main machine just so they can push back from their laptops!  And
    they have to remember to check that bare repo when they get back into the office,
    and so on... it's just not sustainable.  For a supposedly distributed version
    control system, this seems at best a really odd choice.  As someone else said,
    basically with the extra bare repo you're just reinventing the centralized model.
- id: 2170
  author: Jakub Narebski
  author_email: jnareb@gmail.com
  author_url: ''
  date: '2010-02-11 11:28:01 -0800'
  date_gmt: '2010-02-11 11:28:01 -0800'
  content: "Git from version 1.7.0 would (by default) refuse to push to currently
    checked out branch.  By default it means that you can configure this behavior.\r\n\r\nNote
    also that all tutorials, user manuals, etc. tell you to not push into non-bare
    repository (i.e. one with working directory attached)!"
- id: 2199
  author: Rob Jones
  author_email: jones@craic.com
  author_url: http://craic.com
  date: '2010-03-04 01:47:14 -0800'
  date_gmt: '2010-03-04 01:47:14 -0800'
  content: "I've written up the steps needed to set up a bare repository which makes
    all of this pretty simple. \r\n\r\nhttp://craiccomputing.blogspot.com/2010/03/git-push-and-pull-between-repositories.html\r\n\r\nLike
    much of what we do, it's easy once you know - but getting there can be a pain."
- id: 2202
  author: Git | meta/LPAR
  author_email: ''
  author_url: http://lpar.ath0.com/2009/02/20/git/
  date: '2010-03-06 04:51:29 -0800'
  date_gmt: '2010-03-06 04:51:29 -0800'
  content: '[...] need to work on your usability. If the obvious command to push data
    to a repository actually loses changes, you may want to rethink your command [...]'
- id: 2217
  author: Allan K
  author_email: allankelly@gmail.com
  author_url: http://www.hasnews.com
  date: '2010-03-19 12:45:46 -0700'
  date_gmt: '2010-03-19 12:45:46 -0700'
  content: "Thanks for this post. I'm sure many people are bitten by this 'feature'
    and just walk away. I kind of get the logic, but it's very surprising.\r\nI never
    work directly on the server so 'losing changes' made there isn't a relevant concept.
    On my laptops I have a number of scripts that I run to check for updated-ness
    of git repos and for 'publish'. The last stage of publish is\r\n[code]\r\nssh
    server_name \"cd $REMOTE_DIR &amp;&amp; git checkout -f\"\r\n[/code]\r\nI've been
    aware for a while that a bare server repo with working copies on laptop and server
    is better, but this works for me so \"que sera sera\".\r\n\r\nBTW, a handy incantation
    for updating your local repo status, assuming all your code is in trees under
    ~/code:\r\n\r\n[CODE]\r\n$ find ~/code -type d -name .git -exec sh -c 'D=`echo
    {} | sed -e \"s,/.git,,\"`; echo $D; cd $D; git pull; cd - &gt;/dev/null' \\;\r\n[/CODE]\r\n\r\nCheers,
    al."
- id: 2222
  author: Hans
  author_email: ''
  author_url: ''
  date: '2010-03-29 19:44:51 -0700'
  date_gmt: '2010-03-29 19:44:51 -0700'
  content: "Hi everyone, this post is beginning to show its age. Thanks for all the
    links, comments, etc.\r\n\r\nRecent versions of git now refuse to push to a working
    directory with a nice explanation. I don't know if my post had any influence on
    making that a reality, but as users we can claim victory nonetheless!\r\n\r\nThe
    biggest use case for git push is laptop/dev server. The laptop is behind various
    firewalls at any given time, and the dev server can't pull from it. I've found
    two highly successful ways of dealing with this. The first is to set up ssh to
    automatically set up a tunnel back to your laptop, so you can pull over the tunnel.
    This works quite well in practice, but is slightly noisy (ssh will complain a
    bit about not being able to set up the tunnel if the tunnel already exists).\r\n\r\nThe
    second approach is to set up repositories on the laptop to push to a prefix, making
    push symmetric with fetch. e.g. in .git/config\r\n\r\n\tpush = +refs/heads/*:refs/remotes/laptop/*\r\n\r\nIf
    your laptop is sometimes available for pull (e.g. with an ssh tunnel or a non-firewall
    connection some of the time), then this works rather well. Otherwise it builds
    up cruft that you can't get rid of with \"git remote prune\", and you have to
    \"rm -r .git/refs/remotes/laptop\" and then repush from the laptop, which might
    make some queasy."
- id: 2263
  author: Dan
  author_email: ''
  author_url: ''
  date: '2010-06-10 11:09:53 -0700'
  date_gmt: '2010-06-10 11:09:53 -0700'
  content: I think the best solution is not clear cut. The behaviour you observe can
    seem counter intuitive but the question is what are the other options? I can only
    really think of one that makes sense. To have the remote machine end up on a temporary
    branch whose HEAD is the commit they were basing their work off. They would then
    be free to rebase their work off of the master branch. When they were happy, they'd
    be able to merge their changes into the master branch. This avoids the typical
    confusion and allows as many pushes as you'd like to take place before you rebase
    without having to remember anything special. The only concern is the user not
    noticing they are no longer on the master, but I guess you could get around this
    with a warning when they next execute a git command "you're now on branch 'old_master'
    instead of 'master' due to a push". In this way you never see strange things in
    "git status" and you have as much flexibility as with "git fetch ; git rebase".
    In fact in writing this I've convinced myself that it's the correct approach.
    Can anyone see a reason why this wouldn't work?
- id: 2264
  author: Hans
  author_email: ''
  author_url: ''
  date: '2010-06-10 16:07:37 -0700'
  date_gmt: '2010-06-10 16:07:37 -0700'
  content: Dan, the fundamental problem with that line of reasoning is that you assume
    that a push should change the working state of the remote repository in a way
    that is compatible with *not* changing the working state of the remote repository.
    This is just silliness. Either go whole hog and push the full state (refusing
    if the checkout isn't clean), or don't mess with the working checkout at all (mirror
    operation to git fetch) and let the user do the merge or rebase. I think the latter
    is more git-like. I think the former is fine too. But I think the current behavior
    is completely broken. (Although, these days it does spit out a big warning with
    instructions and maybe even refuses to push to a non-bare repository without overriding.
    So we've come a long way.)
- id: 2265
  author: Dan
  author_email: ''
  author_url: ''
  date: '2010-06-11 11:14:25 -0700'
  date_gmt: '2010-06-11 11:14:25 -0700'
  content: "Well.. I always want several things to happen with an operation like push.
    \r\n\r\n1. The remote and local repositories to end up in a meaningful state (ie
    they have all the commits).\r\n2. The remote and local checkouts to end up in
    a sensible state (they have all their local changes, considered to be made against
    the relevant parent).\r\n3. The remote and local user be aware that the changes
    have occurred (I won't necessarily be the remote user, nor am I necessarily in
    contact with him).\r\n\r\nThe concern I have with mirroring fetch is that when
    you fetch you know you've done it, and that it makes sense to rebase... If push
    effectively did a fetch on the remote machine the user of the remote repo wouldn't
    necessarily know that they should be rebasing or that they'd been pushed to. I
    suspect we have different workflows in mind. I am not happy with automatic creation
    of a temporary branch, but it seems more \"obvious\" to the user than directly
    paralleling fetch."
- id: 2267
  author: Hans
  author_email: ''
  author_url: ''
  date: '2010-06-11 16:18:43 -0700'
  date_gmt: '2010-06-11 16:18:43 -0700'
  content: 'If you are not the remote user, then mucking about with the remote checkout
    is Bad Idea #1™. But the mirror of a fetch hurts nobody. If you are the remote
    user, then you''re not at all surprised either way.'
- id: 2388
  author: tbear
  author_email: taesoobear@gmail.com
  author_url: ''
  date: '2011-04-27 17:16:16 -0700'
  date_gmt: '2011-04-27 17:16:16 -0700'
  content: How about post-editing the first line near the title that this problem
    was fixed in recent versions. I read all of this just to figure out this is non-issue
    any more.
- id: 2389
  author: Hans
  author_email: ''
  author_url: ''
  date: '2011-04-27 17:39:38 -0700'
  date_gmt: '2011-04-27 17:39:38 -0700'
  content: tbear, it's not a non-issue. It's a mitigated issue. It won't bite you
    like it did because you are protected unless you override it, but I still feel
    it's a fundamentally wrong verb for what it's doing.
- id: 2427
  author: Does “git push” make sense?
  author_email: ''
  author_url: http://www.smashcompany.com/technology/does-git-push-make-sense
  date: '2011-09-28 16:10:45 -0700'
  date_gmt: '2011-09-28 16:10:45 -0700'
  content: ''
- id: 2530
  author: tleo
  author_email: the.gun007@laposte.net
  author_url: ''
  date: '2012-03-27 12:41:01 -0700'
  date_gmt: '2012-03-27 12:41:01 -0700'
  content: "I agree some things seems strange and not well thought-out, but they are.\r\nYou
    just need to practice it more :D"
- id: 2578
  author: Kzqai
  author_email: tchavakspam@gmail.com
  author_url: http://bitlucid.com
  date: '2012-05-10 19:41:45 -0700'
  date_gmt: '2012-05-10 19:41:45 -0700'
  content: "My solution has been to use a staging branch on any working copy that
    isn't bare.  For example, some of my live websites are serving staging branches
    (with .git directories forbidden, importantly).\r\n\r\nThat way, when you push,
    it updates the master branch, but that master branch itself isn't checked out,
    so it doesn't matter, the staging branch is checked out, and remains unchanged."
- id: 2681
  author: Hassan
  author_email: ''
  author_url: ''
  date: '2012-07-31 11:52:51 -0700'
  date_gmt: '2012-07-31 11:52:51 -0700'
  content: As tbear said, I would have appreciated a couple of line saying that this
    issue has at least been mitigated. Thanks.
- id: 2682
  author: Hassan
  author_email: ''
  author_url: ''
  date: '2012-07-31 12:00:59 -0700'
  date_gmt: '2012-07-31 12:00:59 -0700'
  content: Sorry, that sounds grumpy, I'm just new to Git, after spending quite a
    while finding a good system for version control in my company and was quite disappointed
    after reading just the title. I'm glad I decided to read further. :)
- id: 2757
  author: Using Git As A Central Repository | Click &amp; Find Answer !
  author_email: ''
  author_url: http://www.eonlinegratis.com/2013/using-git-as-a-central-repository/
  date: '2013-04-21 22:19:42 -0700'
  date_gmt: '2013-04-21 22:19:42 -0700'
  content: '[...] Useful if you have multiple branches.I was just researching this
    same problem today. This blog post has a lot of discussion on the issue, but the
    majority opinion is to do what Manni said. Look at a [...]'
- id: 2773
  author: teki
  author_email: nomail@nomail.com
  author_url: ''
  date: '2013-05-22 00:58:33 -0700'
  date_gmt: '2013-05-22 00:58:33 -0700'
  content: "$ git --version\r\ngit version 1.8.2\r\n\r\n$ git push ../foo\r\nCounting
    objects: 5, done.\r\nWriting objects: 100% (3/3), 255 bytes, done.\r\nTotal 3
    (delta 0), reused 0 (delta 0)\r\nremote: error: refusing to update checked out
    branch: refs/heads/master\r\nremote: error: By default, updating the current branch
    in a non-bare repository\r\nremote: error: is denied, because it will make the
    index and work tree inconsistent\r\nremote: error: with what you pushed, and will
    require 'git reset --hard' to match\r\nremote: error: the work tree to HEAD.\r\nremote:
    error: \r\nremote: error: You can set 'receive.denyCurrentBranch' configuration
    variable to\r\nremote: error: 'ignore' or 'warn' in the remote repository to allow
    pushing into\r\nremote: error: its current branch; however, this is not recommended
    unless you\r\nremote: error: arranged to update its work tree to match what you
    pushed in some\r\nremote: error: other way.\r\nremote: error: \r\nremote: error:
    To squelch this message and still keep the default behaviour, set\r\nremote: error:
    'receive.denyCurrentBranch' configuration variable to 'refuse'.\r\nTo ../foo\r\n
    ! [remote rejected] HEAD -&gt; master (branch is currently checked out)\r\nerror:
    failed to push some refs to '../foo'"
- id: 2774
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2013-05-22 04:58:54 -0700'
  date_gmt: '2013-05-22 04:58:54 -0700'
  content: Yup, we've come a long way since 2008.
---
<p><em>Ugh</em></p>

<p>Let's say you are a web developer, and you do development on your laptop, then when things are nice and shiny you want to push those changes to the webserver. Seems natural enough, right?</p>

<pre><code>git clone server:/var/www/foo
# ...
git pull

# edit stuff
git commit -a -m 'i edited stuff'
</code></pre>

<p>Now, let's say you're a (possibly former) darcs/bzr/mercurial user and this time you're using git. Git has <a href="http://www.kernel.org/pub/software/scm/git/docs/git-push.html"><code>git-push</code></a>. You read the man page like a good little code monkey, and it seems like it does the same or similar thing to <code>darcs push</code> or <code>hg push</code>. It seems like if you want to push your changes to the server, you'd do this:</p>

<pre><code>git push
</code></pre>

<p>Am I off in left field or does this not seem 100% rational? But wo be unto the code monkey that utters this unfortunate incantation. Observe:</p>

<pre><code>$ mkdir foo
$ cd foo
$ git init
Initialized empty Git repository in /private/tmp/foo/.git/
$ echo hello &gt; foo.txt
$ git add foo.txt
$ git commit -m 'hello'
Created initial commit bee50da: hello
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 foo.txt
$ cd ..
$ git clone foo bar
Initialized empty Git repository in /private/tmp/bar/.git/
$ cd bar
$ echo goodbye &gt;&gt; foo.txt
$ git commit -a -m goodbye
Created commit 99c13c1: goodbye
 1 files changed, 1 insertions(+), 0 deletions(-)
$ git push ../foo
Counting objects: 5, done.
Writing objects: 100% (3/3), 248 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
To ../foo
   bee50da..99c13c1  master -&gt; master
$ cd ../foo
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD &lt;file&gt;..." to unstage)
#
#   modified:   foo.txt
#
$ git diff
$ git diff --cache
error: invalid option: --cache
$ git diff --cached
diff --git a/foo.txt b/foo.txt
index a32119c..ce01362 100644
--- a/foo.txt
+++ b/foo.txt
@@ -1,2 +1 @@
 hello
-goodbye
$ git log
commit 99c13c1e60888ae2c0e221898411e1cd52ad3815
Author: Hans Fugal &lt;hans@fugal.net&gt;
Date:   Mon Nov 10 17:11:57 2008 -0700

    goodbye

commit bee50da72798edc47ddc36dbc4f559f141b1e28b
Author: Hans Fugal &lt;hans@fugal.net&gt;
Date:   Mon Nov 10 17:11:34 2008 -0700

    hello
</code></pre>

<p>I promise I didn't fake that. Yes, you saw that correctly—git wants to <em>undo</em> the changes you just committed. If you happen to have a clean working directory, all you need to do to return to sanity is <code>git reset HEAD</code>. If not, heaven help you.</p>

<p>This is totally unacceptable. It's unforgivable on so many levels. At the <em>very least</em>, the manpage should warn you to not push to repositories with working copies. Git should warn you before you push and screw up your repo that it has a working copy checked out. Ideally, git would behave like darcs and update the working copy. Suboptimally, it would behave like mercurial and make it a new revision that you have to manually checkout. But this is simply ridiculous.</p>

<p>So what is the solution? They tell you to use pull. <em>Hello! Is anyone home?</em> My laptop is roving. It's often behind a NATing firewall. I'm supposed to find my public IP address and figure out how to subvert the evil firewalls of the world every time I want to push my changes to the server?</p>

<p>A workaround, and probably the best real-world workflow, is to have a second bare repository or a second branch on the server, push into that, then ssh into the server and pull the changes. I think <a href="http://www.kernel.org/pub/software/scm/git/docs/everyday.html">this page</a> describes how to do that with a second branch, though I'm short on time to actually try it out at the moment.</p>

<p>More of this sickening story in <a href="http://kerneltrap.org/mailarchive/git/2007/3/18/241553">this thread</a>, where you will learn that at least one other person out there has his head screwed on properly, that the developers are more interested in how hooks work (and fail to allow you to do this even if you grok them), and that they've discussed the problem before and decided the correct response is to RTFM (M for <em>minds</em> this time, since the manual was completely unhelpful).</p>

<p><em>Update:</em> Some of you have been quick to defend git and the design choice of how push behaves. I want to clarify that I don't care so much that push updates the repository but not the working directory. Mercurial works this way too. Not the way I'd do it but it's a valid approach. The problem here is that <code>git push</code> seems like a natural thing to do but screws up your working directory on the remote side. Mercurial doesn't change the working directory, but neither does it silently rebase it and set you up to undo your changes if you're not careful. The problem here is a lack of safety and a lack of warning. They know it's a problem, they've fielded enough "morons". A few words of warning in the man page is all it would take to make me happy.</p>

<p>And now, I have had time to work out a more specific workaround. Here's what I did, and it seems to work well:</p>

<pre><code># Server setup (set up incoming branch)
server$ git branch incoming
server$ git branch
  incoming
* master
  origin

# Laptop setup (local master to remote incoming)
laptop$ git config remote.origin.push master:incoming

# Everyday usage
laptop$ git push
Counting objects: 5, done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 279 bytes, done.
Total 3 (delta 1), reused 0 (delta 0)
To server:/tmp/foo
   b108a07..a9d3282  master -&gt; incoming

server$ git status
# On branch master
nothing to commit (working directory clean)
server$ git pull . incoming
From .
 * branch            incoming   -&gt; FETCH_HEAD
Updating b108a07..a9d3282
Fast forward
 foo.txt |    1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
</code></pre>

<p>You could use hooks to automatically do that <code>git pull . incoming</code> if you liked, making it more like darcs than mercurial.</p>

<p><em>Updated update:</em> On further thought, the cleanest solution is probably to have a separate master (bare) repository, e.g.</p>

<pre><code>$ mkdir master
$ cd master
$ git init
Initialized empty Git repository in /private/tmp/foo/master/.git/
$ git commit --allow-empty -m initial
Created initial commit 999755e: initial
$ cd ..
$ git clone master live
Initialized empty Git repository in /private/tmp/foo/live/.git/
$ cd live
$ git branch
* master
$ cd ..
$ git clone master laptop
Initialized empty Git repository in /private/tmp/foo/laptop/.git/
$ cd laptop
$ echo hello &gt; foo.txt
$ git add foo.txt
$ git commit -m hello
Created commit 2297bcf: hello
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 foo.txt
$ git push
Counting objects: 4, done.
Writing objects: 100% (3/3), 239 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
To /tmp/foo/master/.git
   999755e..2297bcf  master -&gt; master
$ cd ../live
$ ls
$ git pull
remote: Counting objects: 4, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From /tmp/foo/master/
   999755e..2297bcf  master     -&gt; origin/master
Updating 999755e..2297bcf
Fast forward
 foo.txt |    1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 foo.txt
$ echo goodbye &gt;&gt; foo.txt
$ git commit -a -m goodbye
Created commit 04f6702: goodbye
 1 files changed, 1 insertions(+), 0 deletions(-)
$ git push
Counting objects: 5, done.
Writing objects: 100% (3/3), 248 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
To /tmp/foo/master/.git
   2297bcf..04f6702  master -&gt; master
$ cd ../laptop
$ git pull
remote: Counting objects: 5, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From /tmp/foo/master/
   2297bcf..04f6702  master     -&gt; origin/master
Updating 2297bcf..04f6702
Fast forward
 foo.txt |    1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
</code></pre>
