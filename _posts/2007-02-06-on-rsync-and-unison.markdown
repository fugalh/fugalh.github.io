---
layout: post
status: publish
published: true
title: On rsync and unison
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 781
wordpress_url: urn:uuid:e0474619-e135-4501-9d8c-8b8622bc33dc
date: 2007-02-06 11:02:12.000000000 -08:00
tags:
- linux
- rsync
- unison
- yepp
- synchronization
comments:
- id: 1544
  author: Kyle Mathews
  author_email: ''
  author_url: ''
  date: '2007-02-08 15:53:11 -0800'
  date_gmt: ''
  content: |-
    <p>Using Unison for the initial synchronization is, as you found out, a bad idea.  What's normally recommended (and what I did) is just use scp to copy your files between computers and then use Unison from then out to sync changes.  Unision has worked great for me.  Almost fool-proof.  Here's a great blog post:
    <a href="http://web.mit.edu/pgbovine/www/unison_guide.htm" rel="nofollow">http://web.mit.edu/pgbovine/www/unison_guide.htm</a></p>
- id: 1545
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-02-08 16:00:22 -0800'
  date_gmt: ''
  content: <p>Copying the files over doesn't help, it still has to build its little
    internal database. Plus, when the entire task is to copy new files over and delete
    old files, it's an irrelevant workaround. Unison is good for some things. It is
    patently bad for this application.</p>
- id: 1546
  author: Marcelo Oliveira
  author_email: ''
  author_url: ''
  date: '2008-02-22 14:18:51 -0800'
  date_gmt: ''
  content: |-
    <p>Tks,
    these tips were very useful to me.</p>

    <p>My 2 cents below:</p>

    <p>I was trying to sync my homedir with a pendrive (fat32), kubuntu 7.10.</p>

    <p>To solve the problem I have to:</p>

    <p>1) manually remount the pendrive with option shortname=mixed (default is lower).
    2) --modify-window=2
    3) remove the --perms option, actually I'm using -rltODvz</p>
- id: 1547
  author: chris carroll
  author_email: carrolc575@gmail.com
  author_url: ''
  date: '2008-05-02 09:47:25 -0700'
  date_gmt: ''
  content: <p>i have found that if run as a cron job unison is surprisingly fast and
    data transfers are no really noticed and are faster than running it from the comand
    line.</p>
- id: 2235
  author: Brandon
  author_email: brandon@myshape.com
  author_url: ''
  date: '2010-04-09 16:48:46 -0700'
  date_gmt: '2010-04-09 16:48:46 -0700'
  content: "The reason you find Unison slow is because you are using it with FAT (aka
    Windows) file systems.  Unison *has* to use a slower algorithm with Windows file
    systems in order to be 100% safe.\r\n\r\nUsing Unison with file systems like EXT3
    should be much faster because it can use a faster algorithm (primarily based on
    file modify date rather than checksums)to synchronize files."
- id: 2287
  author: Leo
  author_email: ''
  author_url: ''
  date: '2010-08-18 08:48:48 -0700'
  date_gmt: '2010-08-18 08:48:48 -0700'
  content: "Brandon is right.\r\n\r\nI synchronize a bunch of data (25.000 files,
    43GB) and Unison takes a few seconds to tell me that nothing was changed.\r\n\r\nIf
    something was changed, it only takes an amount of time that is fairly proportional
    to the changed data, and if it runs remotely it only sends the differences through
    the network.\r\n\r\nOf course, I use ext3/ext4 filesystems.\r\n\r\nI need it to
    be two-way because the same bunch of data that may be modified in more than one
    computer.\r\n\r\nBut indeed, if you only plan to modify your files in one source,
    and all you want is to save a snapshot of it from time to time, the best solution
    is rsync --delete -av.\r\n\r\nIf you insist on fat, add the --modify-window=1.
    But, hey!, you may try to use unison with the options pretendwin, times, fastcheck,
    and perms=0. First delete your old unison archives and do the slow first run."
- id: 2405
  author: archive and synchronizations with unison and rsync
  author_email: ''
  author_url: http://blog.nguyenvq.com/2011/07/22/archive-and-synchronizations-with-unison-and-rsync/
  date: '2011-07-22 23:00:17 -0700'
  date_gmt: '2011-07-22 23:00:17 -0700'
  content: '[...] it is horrendously slow when transferring to a FAT drive since it
    uses checksum on all the files; it is discussed in the [...]'
---
<p>I have a <acronym title="Samsung YP-MT6X MP3 Player">Yepp</acronym>, which is a wonderful mp3 player because it's small (the size of a AA battery), plays OGG (out of the box!), and presents itself as USB mass storage. </p>

<p>As I am frequently changing the contents for my yepp, because I use it mostly for listening to podcasts, I decided the best thing to do is to keep a mirror on my hard drive and then just hook up the yepp and sync it. Because I also keep music on for relatively long time (compared to podcasts) and I let my podcasting software handle deletions so some longer-period podcasts hang around for awhile, I figured something like rsync or unison would be the best approach.</p>

<p>Initially I was excited about <a href="http://www.cis.upenn.edu/~bcpierce/unison/">unison</a> because I expected I would sometimes change stuff on the yepp and want to see the changes propogated to my hard drive. Possible scenarios for this are putting random files or songs on the yepp from other computers or deleting podcasts I had already listened to on the yepp. </p>

<p>I quickly found that unison was a very poor choice. Unison is designed for synchronizing incremental changes to roughly the same set of files. As such, it expends a lot of effort in doing things like checksums and who knows what else. The first time you run unison on a set of files it will take a long time, this is a <a href="http://alliance.seas.upenn.edu/~bcpierce/wiki/index.php?n=Main.UnisonFAQTips">FAQ</a>. And by long time I mean <em>long time</em>. I once timed how long it takes to copy over a bunch of files that filled all 512MB. It took about 5 minutes IIRC. I then ran unison on the same set of files and after about 5 minutes it had completed almost nothing and had an estimated completion time of an hour. I am not privy to the internal workings of unison, but I think the constant addition of new files, which is in fact basically the only change, as the MP3s themselves don't change, meant unison had to do whatever this really slow thing is fresh for every new file. I have found that it doesn't matter if unison has already built its database or not, adding new files always takes 10 times or more longer than it would to just copy them. I'm not sure what it's doing, but I do know that the whole time my yepp is flashing between "READY" and "WRITING". That tells me unison is doing a lot of itty bitty writes to the flash memory, and I don't think that can be good (yes, even when you specify rsync transfer mode).</p>

<p>So I gave up on the bidirectional sync and wrote a simple script to sync with rsync. The first version looked like this:</p>

<pre><code>rsync --delete -rv ~/Music/Podcasts /Volumes/YEPP
</code></pre>

<p>This syncs my Podcast folder to the Podcast folder on the yepp. It takes no
longer than cp to copy new files, and it deletes old podcasts. Which reminds
me, unison waits until the end to delete old files. This is not good if you're
tight on space. rsync deletes the old files first, <em>then</em> copies the
new/changed ones over.</p>

<p>There's a problem with that script, though. When you run it again tomorrow, it will think it needs to sync all the files. I think that rsync will not actually copy the whole file over, but it will have to do the checksum thing which is slow, and you'll get basically no speedup. And my yepp keeps flashing writing even when no changes would need to be propogating, so rsync is writing to my flash more often than it needs to too. </p>

<p>Well the problem isn't rsync, it's the user. With only the <code>-rv</code> options, (recursive and verbose) rsync will copy new files over with the current timestamp. When you run it again, rsync's quick check algorithm checks the timestamp and sees that they're different and assumes it has to sync those files. It then does the checksum calculations and only the changed bits are transferred over the network. Good for the network usage, not too bad if you have smallish files and a fast disk. Not very good at all if one of the disks is slow.</p>

<p>So we need to be sure and sync the modified times too. That option is <code>-t</code>, which is included in <code>-a</code>. So I tried this script:</p>

<pre><code>rsync --delete -av ~/Music/Podcasts /Volumes/YEPP
</code></pre>

<p>That kind of sort of worked. Some files weren't resynced, but others were. I tried <code>-t</code> and a few other things, and scratched my head a bit. Then I read the fine manual (<code>rsync(1)</code>).</p>

<blockquote>
    <p>When transferring to  FAT  filesystems  rsync  may  re-sync  unmodified files.  See the comments on the <code>--modify-window</code> option.</p>
</blockquote>

<p>Here's what it has to say about <code>--modify-window</code>:</p>

<blockquote>
    <p>When  comparing  two  timestamps  rsync treats the timestamps as being equal if they are within the value of <code>modify_window</code>.  This is  normally  zero,  but you may find it useful to set this to a larger value in some situations. In particular,  when  transferring  to  Windows  FAT  filesystems which cannot represent times with a 1 second resolution <code>--modify-window=1</code> is useful.</p>
</blockquote>

<p>So I updated my script and now it works like a charm:</p>

<pre><code>rsync --delete --modify-window=1 -av ~/Music/Podcasts /Volumes/YEPP
</code></pre>

<p>There are a few lessons to be learned here. First, unison isn't always the best tool for the job. Don't drink the kool-aid. I think it is a good bit of software though and has its uses. I'm not sure it can be adapted for efficient flash-drive frequent new-file usage, but if you know how feel free to comment. Second, rsync is nifty, but it's more nifty when you use it properly. Get in the habit of <code>-a</code> instead of <code>-r</code>, it almost never hurts and will often speed things up dramatically. Remember the <code>--modify-window=1</code> trick for FAT filesystems. Finally, if you *do* make a change to a file and keep the same timestamp and file size somehow, rsync won't sync that file unless you specify <code>-c</code>. It's a pathological case, but it's good to know about.</p>
