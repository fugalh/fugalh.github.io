---
layout: post
status: publish
published: true
title: Darcs and Mercurial Redux
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 904
wordpress_url: urn:uuid:3e72ae86-0aed-4a1c-a665-8545b8e7d2b0
date: '2007-11-20 20:36:00.000000000 -08:00'
tags:
- darcs
- control
- mercurial
- revision
- reply
comments:
- id: 1656
  author: Trent W. Buck
  author_email: ''
  author_url: ''
  date: '2007-11-20 21:49:22 -0800'
  date_gmt: ''
  content: |-
    <blockquote>
        <p>I assume you mean with a darcs cgi? In
        any case, hg serve is undeniably easier.</p>
    </blockquote>

    <p>I simply meant any old "dumb" http server.
    I used thttpd as an example because I know off the top of my head how to start new daemons as non-privileged users on non-privileged ports.</p>

    <p>I was operating on the assumption that one starts an http server in order to export the repository to anonymous users.  Obviously if you want something like ViewVC, you'd need to use a non-"dumb" httpd; hg serve falls into this category.</p>

    <p>thttpd: <a href="http://www.acme.com/software/thttpd/" rel="nofollow">http://www.acme.com/software/thttpd/</a></p>

    <p>viewvc: <a href="http://www.viewvc.org" rel="nofollow">http://www.viewvc.org</a></p>
- id: 1657
  author: Trent W. Buck
  author_email: ''
  author_url: ''
  date: '2007-11-20 21:58:26 -0800'
  date_gmt: ''
  content: |-
    <p>Regarding .hgignore's emptiness-by-default, I simply worked around this by copying darcs' default boring entries into ~/.hgignore (and pointing ~/.hgrc at it).</p>

    <p>It's worth pointing out that darcs' repo-local boring file depends on which version of darcs did the <code>darcs init' or</code>darcs get', and that it doesn't ever get updated by a push or pull.  So if you make a repo with darcs 1.0.3, it will have "obsolete" or "wrong" boring entries.  If you have a heterogeneous develop group, some using old versions, this may cause confusion if generated files are ignored by one version (by default) but not another.</p>

    <p>ftp://twb.ath.cx/Preferences/.hgignore</p>
- id: 1658
  author: Trent W. Buck
  author_email: ''
  author_url: ''
  date: '2007-11-20 22:08:59 -0800'
  date_gmt: ''
  content: |-
    <p>Regarding default "upstream" repo, Darcs uses _darcs/prefs/defaultrepo much like .hg/hgrc:paths:default.  Darcs will by default write it (and idempotently append _darcs/prefs/repos) for each get, push and pull (IIRC).</p>

    <p>I found this pretty annoying, since I often use temporary and feature branches, and these would clobber defaultrepo.  In ~/.darcs/prefs I have 'ALL no-set-default', which amounts to adding --no-set-default to each invocation.  AIUI this means _darcs/prefs/defaultrepo is only written if it does not already exist, which is the best DWIM heuristic I've seen so far (for me, anyway).</p>
- id: 1659
  author: Trent W. Buck
  author_email: ''
  author_url: ''
  date: '2007-11-20 22:14:02 -0800'
  date_gmt: ''
  content: |-
    <p>Oh, and I should not let any comparison of SCMs go by without referring to </p>

    <p><a href="http://revctrl.org/" rel="nofollow">http://revctrl.org/</a> and irc://irc.freenode.net/#revctrl</p>
- id: 1660
  author: Trent W. Buck
  author_email: ''
  author_url: ''
  date: '2007-11-20 22:19:59 -0800'
  date_gmt: ''
  content: |-
    <p>I wish to emphasize the (current) lack of an analogue of "darcs amend" in Mercurial.    In the same way I compulsively save a source file whenever I stop typing, I like to compulsively record incomplete patches in my local working repository and then incrementally re-record them until the patch is complete (whereupon I push it upstream).  Having code that's only stored in the working tree and not even in the metadata of the working tree makes me nervous, and it can become confusing if you stop working on one feature to make an unrelated fix that you run into while working on that feature -- e.g. fixing a typo.</p>

    <p>darcs amend makes this very easy, whereas it is several steps in hg -- or impossible, if you have committed another changeset (e.g. an unrelated typo fix in ./doc/) after your partial changeset.</p>
- id: 1661
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-11-21 07:36:34 -0800'
  date_gmt: ''
  content: |-
    <p>Ah, I see what you're saying about thttpd. I do the same thing by just putting my repo somewhere in my public_html directory. I believe it's the same with mercurial also. It's a nice feature. I was thinking more about human-browseable repositories (look at history, diffs, etc.) than pullable.</p>

    <p>You can accomplish the <code>darcs amend</code> workflow with MQ, but it has to be intentional. I too really like <code>darcs amend</code>.</p>
- id: 1662
  author: Masklinn
  author_email: ''
  author_url: ''
  date: '2007-11-21 13:14:17 -0800'
  date_gmt: ''
  content: |-
    <blockquote>
        <p>I wish to emphasize the (current) lack of an analogue of "darcs amend" in Mercurial. In the same way I compulsively save a source file whenever I stop typing, I like to compulsively record incomplete patches in my local working repository and then incrementally re-record them until the patch is complete (whereupon I push it upstream).</p>
    </blockquote>

    <p>You can easily do that via MQ, but it's noticeably more involved:</p>

    <ul>
    <li><p>Create a new patch via <code>hg qnew "commitmessage" patchname</code> (add <code>-f</code> if you already have changes in your working directories)</p></li>
    <li><p>Refresh the patch with <code>hg qrefresh</code>, or just create new patches on top of the old one and merge everything later</p></li>
    <li><p>[OPTIONAL] If you used the second solution (create several patches), <code>hg qgoto</code> the initial patch, then <code>hg qfold</code> to fold all the patches into the original one</p></li>
    <li><p>Finally, <code>hg qdel-r qbase:qtip</code> will transform all your MQ patches into regular Mercurial revisions</p></li>
    </ul>

    <p>The edge over <code>darcs amend</code> is that unless you specifically ask that they are, <code>mq</code> patches are not versioned, thus can't be pulled by someone pulling from you.</p>
- id: 1663
  author: Kevin
  author_email: ''
  author_url: ''
  date: '2007-12-11 15:43:29 -0800'
  date_gmt: ''
  content: <p>for ignoring patches you don't want to pull in darcs, check out the
    complement repo flag (new). basically, you build a repo with all the patches you
    don't want, and tell darcs that is the complement repo, and it won't prompt you
    to pull the patches in your complement repo.</p>
---
<p>I've been getting a few comments on <a href="http://hans.fugal.net/blog/articles/2007/11/16/mercurial-and-darcs">my other post</a>, and I just got another excellent reply by email from Trent Buck. As I was writing my reply to him, it occurred to me that it might be better to reply here in order to clarify things for posterity.</p>

<p>Regarding <code>darcs record</code>, Trent said,</p>

<blockquote>
    <p>Analogous to <code>hg record</code>, new in 0.9.5</p>
</blockquote>

<p>I was aware of this, as of that morning, but hadn't had much opportunity to try it out. I did mention it in passing later in the post. It bears repeating what I said then—many of the most useful behaviors of mercurial are in extensions that while distributed must be enabled in your <code>.hgrc</code>.</p>

<blockquote>
    <blockquote>
        <p>On the other hand, darcs uses _darcs to store its metadata, which is
        probably for cross-platform reasons but is definitely an
        eyesore. (.darcs would be better).</p>
    </blockquote>

    <p>I don't know why people complain about this.  CVS doesn't use dotdirs
    either, but nobody switching away from it says "wow, fantastic!  At
    last I need ls -a to see the metadata!".</p>
</blockquote>

<p>I purposefully didn't get started on CVS. Nobody I know <em>likes</em> seeing CVS directories, and they're really of little use 90% of the time. One thing I love about both darcs and mercurial (and most other distributed RCSs) is that the repo is right there, not stashed away in some other place on the disk. CVS has the worst of both worlds. <code>_darcs</code> made me ecstatic, <code>.hg</code> made me that much more pleased. </p>

<blockquote>
    <blockquote>
        <p>It's annoyingly inconvenient to grab a specific revision (partly
        because such a concept doesn't really exist) or a specific point of
        time.</p>
    </blockquote>

    <p>Important revisions (e.g. releases) can be named (<code>darcs tag</code>).  You can
    grab a specific subsets of patch by pulling into an null repo with the
    <code>--match</code> or <code>--patch</code> argument.  While I haven't tried it, I assume you
    can <code>--match</code> by date/time less than a particular date.</p>
</blockquote>

<p>Yes, the way to do it is by <code>--match</code> or <code>--patch</code> (I don't remember which). It's certainly possible. I may have just got off on the wrong foot in this regards with darcs, but I've always found darcs to be mildly hostile to going back to the past. On the other hand, locating certain patches is very powerful in darcs, and by the nature of darcs you can do powerful things with them.</p>

<blockquote>
    <blockquote>
        <p>Darcs has no idea of branching. Or more precisely, every darcs
        repository is its own branch and so it leaves that up to you. That's
        theoretically ok, but I do prefer to keep the clutter of multiple
        working copies at bay. Combined with not having to rebuild the whole
        project from scratch and not wasting the disk space for a large
        working directory,</p>
    </blockquote>

    <p>Both hg and darcs use hard links automatically when working on
    multiple one-branch-per-repo repos, if the filesystem supports hard
    links.</p>
</blockquote>

<p>Mea culpa. I was aware of this and the implication that darcs didn't do it slipped through in my sloppy writing.</p>

<blockquote>
    <blockquote>
        <p>in-place switching to certain branches/revisions like git and hg do
        is really nice.</p>
    </blockquote>

    <p>Agreed.</p>

    <blockquote>
        <p>The two real thorns in the side of darcs are the dreaded exponential
        merge (I have run into it, alas), and the fact that I have a devil
        of a time getting it to run everywhere I am. Haskell is not that
        common, and it's a big thing to have to build, e.g. with MacPorts.
        That's when it will build at all (but that MacPorts rant is for
        another post).  There are binaries for windows and mac, but
        sometimes they don't work and versions don't match up... it can be a
        nightmare. It can usually work out, but it can be difficult.</p>
    </blockquote>

    <p>Conceded.</p>

    <blockquote>
        <p>I mentioned cherry picking. One UI flaw in darcs that greatly
        reduces the real-world utility of its excellent cherry picking
        support is that you can't tell it that you would prefer to refuse
        this patch for ever and ever.  Every time you pull you have to tell
        it "no, I don't want that patch".</p>
    </blockquote>

    <p>Conceded.  I would quite like this feature, too.  AFAICT the current
    workaround is to pull the patch you don't want, then record an inverse
    patch (<code>darcs rollback</code>).  The other trick is to make sure you always
    pull a restricted subset using <code>--patch</code> or <code>--match</code>.  Perhaps you could
    automate this with <code>pull match not hash=XXX</code> in <code>_darcs/prefs/defaults</code>,
    but I have not tried this.</p>
</blockquote>

<p>Interesting workarounds, thanks.</p>

<blockquote>
    <blockquote>
        <p>hg is quick and easy to type.</p>
    </blockquote>

    <p>So do</p>

<pre><code>alias d=darcs
</code></pre>

    <p>or</p>

<pre><code>x=`which darcs`  # not posix
ln -s "$x" "${x%arcs}"
</code></pre>
</blockquote>

<p>I concede that it's a weak argument, but it <em>was</em> just a stream-of-consciousness set of observations and not a structured argument. In practice I use tab completion and only really do this sort of thing with repetitive options (e.g. <code>ll</code> for <code>ls -l</code>) or where there is an annoying tab-completion ambiguity.</p>

<blockquote>
    <blockquote>
        <p>It has a powerful extension mechanism, with many interesting
        extensions available.</p>
    </blockquote>

    <p>Agreed, this is an important feature.</p>

    <blockquote>
        <p>CVS-like abbreviations for minimal typing are handy.</p>
    </blockquote>

    <p>Darcs similarly supports truncated commands—to least ambiguous
    string, rather than explicit aliases.  I'm told Hg and Bzr do not do
    it this way because then people would be confused when activating a
    new extension suddenly meant you had to type a longer command string,
    because there was more ambiguity.</p>
</blockquote>

<p>Also true, and fell victim to my not-quite-parallel treatment of darcs and mercurial. The CVS abbreviations are nice for people who 'grew up' during the CVS occupation.</p>

<blockquote>
    <blockquote>
        <p>It has a built in webserver for quick and easy web-based
        collaboration (for firewall reasons or for an interface to the repo
        for non-hg users).</p>
    </blockquote>

    <p>Meh.  HTTPds are cheap to set up, e.g.</p>

<pre><code>thttpd -u $USER -d $PWD -p 8118
</code></pre>
</blockquote>

<p>I assume you mean with a darcs cgi? In any case, <code>hg serve</code> is undeniably easier.</p>

<blockquote>
    <p>However it's worth noting that the built-in mercurial httpd supports
    hg push (via POST), but does no access control, and does not support
    other important commands (e.g. in-repo branching).</p>
</blockquote>

<p>I was not aware push was supported at all, but according to the wiki, <a href="http://www.selenic.com/mercurial/wiki/index.cgi/PublishingRepositories#head-6f95850576bcf93ab70d809f94e7ec86690ba8a6">push
support requires
configuration</a>,
including telling it who can push (access control by http auth and using https).
In any case, for my own project I would either give developers ssh access or require they submit patches by email. But I can see where a fully-featured HTTP repo with access controls would come in handy for some development flows.</p>

<blockquote>
    <blockquote>
        <p>It's storage efficient, and has the novel and all-important
        optimization principle of avoiding disk seeks.</p>
    </blockquote>

    <p>Meh.  Optimize later.</p>
</blockquote>

<p>For the most part I agree with you. But it is the sort of thing that demonstrates that the authors have system programming experience and know what kinds of optimizations matter (disk seeks) and what kind don't (writing in Python instead of C). Premature optimization may be the root of all evil, but not all optimization is premature. As a case in point, see the thorn in darcs' side (exponential merge). If they said today that they fixed exponential merge, they would get some of their refugees back, but not all. And much of the damage of bad publicity is already done (and I regret that these posts probably contribute however small to that phenomenon).</p>

<blockquote>
    <blockquote>
        <p>This is especially true of pull and push which don't update the
        working directory.</p>
    </blockquote>

    <p>hg fetch does, but it does not (currently) support in-repo branching.</p>
</blockquote>

<p>Another of those included-but-not-enabled features. I wasn't aware fetch doesn't support in-repo branching, but probably because I think of fetch more as a network action.</p>

<blockquote>
    <blockquote>
        <p>Some of the most useful stuff is provided by extensions that are
        disabled by default (at least they are distributed). fetch, record
        (for darcs-like hunk-by-hunk recording), mq, bisect, transplant (for
        cherry picking).</p>
    </blockquote>

    <p>Transplant doesn't actually cherry-pick a changeset; it commits a
    different changeset with a different hash which happens to make
    identical changes to the working tree.</p>
</blockquote>

<p>Very true, and an important distinction. I intend to blog soon on quilt, patches, and cherry picking, so I didn't get into this much.</p>

<blockquote>
    <blockquote>
        <p>It doesn't have the cherry picking abilities of darcs, though there
        is the record extension (for cherry picking from your working
        directory) and the transplant extension (for cherry picking
        proper).</p>
    </blockquote>

    <p>While vastly better than bzr shelve, these are quick and dirty hacks
    because darcs-style cherry picking isn't possible when each changeset
    implicitly depends on its immediate ancestor (the case in hg and bzr).</p>
</blockquote>

<p>Or they are simply different approaches. Again, look for that post Real Soon Now™. I might mention that to my (very limited) understanding, git cherry picking works in the same fashion. Darcs is quite unique in this respect, in  my experience.</p>

<blockquote>
    <blockquote>
        <p>I haven't used the latter yet so I don't know if it works well or
        not. .hgignore is easy to manage, but comes with almost no useful
        defaults. This is for performance reasons apparently, but I'd be
        willing to take the hit.</p>
    </blockquote>

    <p>.hgignore and darcs' boring file are much of a muchness.</p>
</blockquote>

<p>Absolutely. As are the equivalents in cvs, svn, git, etc. However, darcs' system-wide boring file is populated much more aggressively. You never have to add <code>.o</code> files or emacs/vim swap files, because they're already there.</p>

<blockquote>
    <blockquote>
        <p>I don't like that I have to type ssh urls out, as
        <code>ssh://example.com//path/to/repository</code></p>
    </blockquote>

    <p>Agreed.  Darcs uses scp notation, although it also has trouble with
    tilde expansion.  Note that darcs push to an ssh repository will apply
    pushed patches to the working tree, which hg and bzr do not attempt to
    do.  Like rsync, darcs needs to be installed on both ends of the ssh
    link for a push (but not a pull) to accomplish this.</p>
</blockquote>

<p>I have run into the tilde expansion issue. The push behavior I described above as surprising.</p>

<blockquote>
    <blockquote>
        <p>I don't like that you don't get compatible repositories if you start
        from the same code. For example:</p>

<pre><code>tar xzf foo-1.0.tar.gz
rsync -a foo-1.0 foo-1.0-2
cd foo-1.0
hg init
hg ci -Am 'initial'
cd ../foo-1.0-2
hg init
hg ci -Am 'initial'
</code></pre>

        <p>At this point you cannot pull or push from one of these repositories
        to the other, although they are semantically identical. I do this
        from time to time with darcs.</p>
    </blockquote>

    <p>This can't be done (safely) in darcs either; it's only an accident
    that it worked at all for the OP.</p>
</blockquote>

<p>I've (rightfully) gotten the most slack over this bit. I agree it's bad form. Shame on me! The frustration arose out of a frustrating situation. I was mirroring the FlightGear data repository (<code>.hg</code> alone is 890MB) for three different branches (OSG and plib from FlightGear's CVS, and someone else's git repository). Due to limitations of CVS and tailor, I had to redownload the entire CVS repo, and the two had no common history. The fault here lies with CVS and tailor, really, but the above behavior would have allowed me to work around it.</p>

<p>Jamie said in a comment, </p>

<blockquote>
    <p>I can't claim I have much trouble setting default push/pull locations, and if you hg clone from a remote repository it sets it up automatically to be there for you.</p>

    <p>In .hg/hgrc,</p>

<pre><code>  [paths]
  default=ssh://host/path
</code></pre>
</blockquote>

<p>I maintain that hg should figure it out after the first couple pushes/pulls without a set default (as darcs does), but thanks for the tip. I'm sure I would have found it when I got around to RTFMing the second time around, or when I got annoyed enough.</p>

<p>Someone else defended git as being not overly complicated. I do think git theory is slightly more complicated than hg or darcs, but what I was really referring to is the UI. <code>git help -a</code> returns a staggering 126 commands. Some may call that power and flexibility, but IMHO it's complication. Still, it has come a long long way in usability and I don't hesitate to nod my head in recommendation when someone chooses to use it.</p>

<p>Thanks to all for your comments. I enjoy the discussion.</p>
