---
layout: post
status: publish
published: true
title: Mercurial and Darcs
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 901
wordpress_url: urn:uuid:de18e9f4-1a4a-4728-b71b-f8a31bef43f4
date: '2007-11-16 21:10:55.000000000 -08:00'
tags:
- darcs
- distributed
- hg
- mercurial
- revision control
comments:
- id: 1644
  author: Scott Robertson
  author_email: ''
  author_url: http://scottr.org/blog/
  date: '2007-11-16 22:24:03 -0800'
  date_gmt: ''
  content: |-
    <p>I'm not sure it's too fair to grip about hg not catching semantic similarity, but you can just change your habit to an order like this:</p>

    <pre><code>tar xzf foo-1.0.tar.gz
    cd foo-1.0
    hg init
    hg ci -Am 'initial'
    cd ..
    hg clone foo-1.0 foo-1.0.2
    </code></pre>

    <p>and get the same result.</p>
- id: 1645
  author: Monkey Boy
  author_email: ''
  author_url: ''
  date: '2007-11-20 16:27:04 -0800'
  date_gmt: ''
  content: |-
    <p>I don't think git is really complicated.  Maybe people look for complicated theories that just aren't there, and feel that they've missed something.  The below is in the manual, maybe people just don't believe it.</p>

    <p>First and foremost, git does not store or work in terms of patches or diffs. It can certainly output them, but it's not the way it works internally .  There are objects.  Objects are a bit like files, only immutable (See also the plan 9 "venti" data store...). They have a "name", their hash code. Some objects are "commits", these describe a bunch of objects i.e. a coherent state of the whole tree.   The commits are arranged into a coherent timeline as each commit (except the initial commit) has a parent  Most objects, however, are just the content of files.  There are a few details about tags and branches and merging, but they're basically just chains of commits.</p>

    <p>That's pretty much it.  Everything else is layered on top.  Git doesn't give a crap about neat patch theory or microoptimisation: it just relies on the filesystem underneath being a very high-performance unixoid file system (that's why git particularly sucks on windows and works well on linux).</p>
- id: 1646
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-11-20 17:16:14 -0800'
  date_gmt: ''
  content: |-
    <p>It's not the theory of git that I'm claiming is complicated. It's the UI.</p>

    <p>Actually, although the theory behind git is straightforward and not too hard to understand, its mapping to real-world use (outside of kernel development) *is* nontrivial and can really hang you up if you don't think like Linus. If you're not hardwired for filesystem development, mapping git to your internal notions of changes is quite unnatural.</p>
- id: 1647
  author: David
  author_email: ''
  author_url: ''
  date: '2007-11-20 17:16:27 -0800'
  date_gmt: ''
  content: |-
    <p>If you want the power of darcs' cool hunk recording, you might want to check out commit-patch: <a href="http://porkrind.org/commit-patch/" rel="nofollow">http://porkrind.org/commit-patch/</a></p>

    <p>It lets you check in patches (not whole files) to darcs, mercurial, and cvs. I find it very very useful.</p>

    <p>-David</p>
- id: 1648
  author: Jamie
  author_email: ''
  author_url: ''
  date: '2007-11-20 18:56:19 -0800'
  date_gmt: ''
  content: |-
    <p>I can't claim I have much trouble setting default push/pull locations, and if you hg clone from a remote repository it sets it up automatically to be there for you.</p>

    <p>In .hg/hgrc,</p>

    <pre>[paths]
    default=ssh://host/path</pre>
- id: 1649
  author: Monkey Boy
  author_email: ''
  author_url: ''
  date: '2007-11-20 20:55:56 -0800'
  date_gmt: ''
  content: |-
    <p>"mapping git to your internal notions of changes is quite unnatural"</p>

    <p>But are they just learned notions?  I don't find any of rcs, cvs, svn and darcs more natural than git, any more than windows is more natural than linux (in fact, having learnt linux first, I prefer it). I wouldn't say I'm "hardwired for filesystem development".</p>

    <p>"its mapping to real-world use (outside of kernel development) *is* nontrivial"</p>

    <p>I don't believe that either. Git is used for a whole bunch of other large projects (mesa and freedesktop.org stuff for starters, but also end-user apps and things like website management
    (<a href="http://jointheconversation.org/railsgit" rel="nofollow">http://jointheconversation.org/railsgit</a>)), </p>

    <p>Do you just mean to "mapping to use like some other RCS instead of git"? But it IS different to other RCSes, I don't dispute that. That said, there is a darcs interface for git:
    <a href="http://wiki.darcs.net/DarcsWiki/DarcsGit" rel="nofollow">http://wiki.darcs.net/DarcsWiki/DarcsGit</a></p>

    <ul>
    <li>so you get darcs' interface and git's engine.</li>
    </ul>

    <p>quilt-like functionality for git is provided by stgit. Like cogito, I guess it might get effectively superseded by core git at some stage, but anyway:
    <a href="http://procode.org/stgit/" rel="nofollow">http://procode.org/stgit/</a></p>
- id: 1650
  author: Garry
  author_email: ''
  author_url: http://scie.nti.st
  date: '2007-11-21 02:05:45 -0800'
  date_gmt: ''
  content: |-
    <p>In 2 jobs I've had, I've taught fairly non-die-hard-technical people (read: HTML/CSS/Javascript guys / designers) to use Git.  And I did it fairly easily.  No one told them it was hard.  As a result, they took it for granted and just used it.  The myth that Git is hard these days is simply a myth.</p>

    <p>When I hear relatively technical people have trouble with Git, yet my CSS guy doesn't have any problem committing his changes back to the repo, I wonder if people are over thinking it.</p>
- id: 1651
  author: Larry Hastings
  author_email: ''
  author_url: ''
  date: '2007-11-21 03:45:22 -0800'
  date_gmt: ''
  content: <p>I'm guessing Darcs uses _darcs instead of .darcs because of VMS.  Last
    year, Monotone changed the names of all its sekrit information, and it was going
    to use .mtn until a VMS user complained that "." isn't a legal character in a
    VMS filename.  (Why they couldn't just use a different directory name on VMS,
    I don't know.)</p>
- id: 1652
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-11-21 07:17:57 -0800'
  date_gmt: ''
  content: |-
    <p>Hi Garry,</p>

    <p>The basics of using git unimaginatively are indeed just as easy as CVS or any other RCS. It didn't used to be so, but it is so now. Using git isn't hard. Understanding it can be mildly difficult. Bending it to your will (as technical folk are wont to do) requires understanding.</p>

    <p>I'm not saying git is rocket science. I'm saying it's more complicated than hg, with marginal if any benefit.</p>
- id: 1653
  author: gebi
  author_email: ''
  author_url: ''
  date: '2007-11-22 06:40:14 -0800'
  date_gmt: ''
  content: <p>i miss real branch support in mercurial with all the neat refspec formats
    of git</p>
- id: 1654
  author: Victor
  author_email: ''
  author_url: ''
  date: '2008-04-01 16:11:04 -0700'
  date_gmt: ''
  content: |-
    <p>"I'm guessing Darcs uses _darcs instead of .darcs because of VMS."</p>

    <p>No, it's because of MSs Visual Studio. It doesn't work with .XYZ files, so some other VCSs have patches/version too wich use _XYZ files/archives.</p>
- id: 2266
  author: Pete
  author_email: pete.hurst@gmail.com
  author_url: http://www.downplay.co.uk
  date: '2010-06-11 15:22:05 -0700'
  date_gmt: '2010-06-11 15:22:05 -0700'
  content: "I'm not sure what Victor means when he says \"Visual Studio. It doesn’t
    work with .XYZ files\".\r\n\r\nI've been working on SVN projects in Visual Studio
    for a long time and have never had any issues with .svn directories. In fact,
    Visual Studio simply doesn't see them - which is exactly what I want, otherwise
    every time I did a project-wide search it would be taking forever scanning through
    the repository directories!"
- id: 2387
  author: Andrew Pennebaker
  author_email: andrew.pennebaker@gmail.com
  author_url: http://www.yellosoft.us/
  date: '2011-04-26 08:42:04 -0700'
  date_gmt: '2011-04-26 08:42:04 -0700'
  content: ':( MacPorts is indeed always out of date.'
---
<p>I'm a long-time distributed revision control user and advocate. I think it's the only way to go, but this article isn't about convincing you of that. I'll just take it for granted.</p>

<p>From almost the beginning, I have used <a href="http://darcs.net/">darcs</a>. I did try Tom's <em>ahem</em> Lame Arch, which I found to be completely unusable. Darcs hasn't been around as long as arch, but it is in roughly the same generation as other early systems like monotone and bazaar. I think of these as the second wave of distributed revision control (the first wave being, basically, tla). When I read about darcs I was impressed by the <a href="http://darcs.net/manual/node8.html">theory of patches</a>. When I tried darcs I was very impressed by how easy it is to use. Soon it became second nature and I never looked back.</p>

<p>But I did look forward, and sideways. When collaborating on a project using <a href="http://subversion.tigris.org/">svn</a> I gave <a href="http://svk.bestpractical.com/view/HomePage">svk</a> a whirl. I don't hesitate to recommend svk if you're otherwise stuck with svn.</p>

<p>When the third wave of distributed revision control came along, ushered in by the Great Linux/BitKeeper Fiasco, I took a cursory look at git. A couple years later (aka earlier this year) I took a closer look. I can see that it has come a long way (in user interface). You don't need "chrome" or whatever they used to call the wrappers like cogito anymore. It's fairly usable. But it's also fairly complicated (that's an understatement, if you left your understatement detector at home). It's perfectly tailored for what Linus and other kernel developers need, but that's not necessarily what the rest of us need. I wouldn't hesitate to nod my head in agreement if you moved from CVS or subversion to git.</p>

<p>Not entirely satisfied with git, and not being able to use darcs (because of the dreaded exponential merge, and general slowness), I looked at <a href="http://www.selenic.com/mercurial/wiki/">Mercurial</a> (Hg from now on). I found that it was fast like git, but easy to use like darcs. The <a href="http://hgbook.red-bean.com/">documentation</a> is excellent, probably the best in the game. The underlying theory is easy to grok, and this is important. Darcs is the same way, although the two theories are definitely different. It has served me well in the application where I couldn't use darcs, but I remained a darcs user for other things. </p>

<p>But mercurial has been seeping into my consciousness of late. Rumors surface from time to time of darcs users migrating to mercurial (it seems to be the only one they migrate to). Other people praise it too. I find it plenty easy to use even as a second-class arrow in my quiver. Finally it gains enough ground that I decide to use it for a project where I'm actually exercising the version control system. I have really liked what I've seen. So the rest of this already-long post will be a comparison of darcs and mercurial. I'm not saying either one or even both together are "the best" by any objective measure, though I definitely prefer them over others myself. I don't know that I'll come to any conclusion over whether to use darcs or mercurial in the future (I haven't yet, anyway, though I'm leaning towards mercurial). I just want to get my comparison out there. Note also that I'm probably not going to mention every feature that I love that they both have in common. As such this isn't an evangelism for either one over the rest of the pack. Just a comparison of what distinguishes these two.</p>

<p>First, darcs. Darcs has excellent support for cherry picking. Its user interface is second to none. It is easy to mail a set of patches to another darcs user or to someone in general. The theory of patches is very interesting and flexible, and easy to follow (until strange things happen, when it gets really hard to follow). It's written in Haskell by a physicist, which has got to count for something. <code>darcs record</code>, which will ask you whether you want to check in each hunk that's changed in your working directory, rather than an all-or-nothing commit, is a joy to work with (especially for those of us who seem to lack the discipline to check in features and bugfixes in neat little packages).</p>

<p>On the other hand, darcs uses <code>_darcs</code> to store its metadata, which is probably for cross-platform reasons but is definitely an eyesore. (<code>.darcs</code> would be better). It's annoyingly inconvenient to grab a specific revision (partly because such a concept doesn't really exist) or a specific point of time. Darcs has no idea of branching. Or more precisely, every darcs repository is its own branch and so it leaves that up to you. That's theoretically ok, but I do prefer to keep the clutter of multiple working copies at bay. Combined with not having to rebuild the whole project from scratch and not wasting the disk space for a large working directory, in-place switching to certain branches/revisions like git and hg do is really nice. Darcs doesn't support symlinks or permissions, again for cross-platform reasons. The two real thorns in the side of darcs are the dreaded exponential merge (I have run into it, alas), and the fact that I have a devil of a time getting it to run everywhere I am. Haskell is not that common, and it's a big thing to have to build, e.g. with MacPorts. That's when it will build at all (but that MacPorts rant is for another post). There are binaries for windows and mac, but sometimes they don't work and versions don't match up... it can be a nightmare. It can usually work out, but it can be difficult.</p>

<p>I mentioned cherry picking. One UI flaw in darcs that greatly reduces the real-world utility of its excellent cherry picking support is that you can't tell it that you would prefer to refuse this patch for ever and ever. Every time you pull you have to tell it "no, I don't want that patch". This makes maintaining similar but subtly different branches impractical. A better tool for this job is <a href="http://www.suse.de/~agruen/quilt.pdf">quilt</a>. In practice, I've done precious little cherry picking. It's always nice to know I can, but after some deep thought on the subject over the last couple days I'm not at all convinced that it's worth supporting in the revision control system. More on that in another post.</p>

<p>Now, mercurial. It's fast, easy to use, and easy to install. It is written in Python (with some C) and works well on all three platforms. The <code>.hg</code> directory is not an eyesore. <code>hg</code> is quick and easy to type. It supports branching. It has a powerful extension mechanism, with many interesting extensions available. The theory is easy to grok and follow, so you're not surprised very often. The implementation seems excellent, from the point of view of both a user and a system administrator. CVS-like abbreviations for minimal typing are handy (like <code>hg ci</code> for <code>hg commit</code>). I've already mentioned the excellent documentation. I might as well mention an excellent <a href="http://video.google.com/videoplay?docid=-7724296011317502612">Google Tech Talk</a> given by the author of said documentation. <code>hg clone</code> is fast and efficient and uses hardlinks where it can (for the metadata, not the working directory). It has a built in webserver for quick and easy web-based collaboration (for firewall reasons or for an interface to the repo for non-hg users). It's storage efficient, and has the novel and all-important optimization principle of avoiding disk seeks. That hg, written in python, gives git a run for its money shows that the devs know what they're doing when it comes to systems programming. Mercurial Queues is extremely cool and useful.</p>

<p>As for the cons, although the theory is easy to grok and doesn't surprise you much, it <em>will</em> surprise you as a newcomer unless you grok the theory. This is especially true of pull and push which don't update the working directory. Some of the most useful stuff is provided by extensions that are disabled by default (at least they are distributed). fetch, record (for darcs-like hunk-by-hunk recording), mq, bisect, transplant (for cherry picking). It doesn't have the cherry picking abilities of darcs, though there is the record extension (for cherry picking from your working directory) and the transplant extension (for cherry picking proper). I haven't used the latter yet so I don't know if it works well or not. <code>.hgignore</code> is easy to manage, but comes with almost no useful defaults. This is for performance reasons apparently, but I'd be willing to take the hit. Let me override with a minimal <code>.hgignore</code> if performance matters that much on this project. I don't like that I have to type ssh urls out, as <code>ssh://example.com//path/to/repository</code>, and it's too difficult to set the default push/pull location so I end up having to type it more than I'd like. Directories aren't first class, which makes me slightly uneasy. It hasn't caused me grief yet though. </p>

<p>I don't like that you don't get compatible repositories if you start from the same code. For example:</p>

<pre><code>tar xzf foo-1.0.tar.gz
rsync -a foo-1.0 foo-1.0-2
cd foo-1.0
hg init
hg ci -Am 'initial'
cd ../foo-1.0-2
hg init
hg ci -Am 'initial'
</code></pre>

<p>At this point you cannot pull or push from one of these repositories to the
other, although they are semantically identical. I do this from time to time
with darcs.</p>

<p>Last, and while certainly not least it's certainly not the biggest deal, mercurial's website is <em>ugly</em>.</p>

<p>So there you have it. Look for a post on quilt and <acronym title="Mercurial Queues extension">MQ</acronym> and some thoughts on cherry picking soon.</p>
