---
layout: post
status: publish
published: true
title: Moving MythTV
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1035
wordpress_url: urn:uuid:1ccf6fe8-7f11-4449-a311-ca9724419acb
date: '2009-01-10 06:39:00.000000000 -08:00'
tags:
- linux
- mythtv
- move
- files
- storage
- server
- backend
- frontend
comments: []
---
<p>I had MythTV on falcon, then I got a new graphics card for gwythaint and so I moved the frontend to gwythaint (HD, yay). Then I got a new hard disk and decided to put the big disks in gwythaint, which meant falcon no longer needed to be a mythtv backend of any sort (gwythaint was already doing all the transcoding). Moving the mythtv backend was not as simple as it should have been. <a href="http://www.mythpvr.com/mythtv/tips/migrate-recordings.html">These instructions</a> outline what I did at first. The database step was not an issue, and of course copying was simple enough, but MythTV couldn't find my moved files.</p>

<p>Poking around in the logs revealed it was still trying to get the movies from falcon, even though I had removed the backend on falcon. So as a stopgap I reinstalled the backend on falcon, set it up as a secondary backend, and set up a samba share so it could access the MythTV data storage directory. Now whenever I watched anything it would go back and forth across the LAN. Whee!</p>

<p>I was puzzled by these assertions that you can just move files between storage directories and MythTV would just find them, when it didn't seem to be even trying on my setup. Then it came to me in a flash of insight. It wasn't trying to look for them because it thought they were still there. I had the same data storage directory path on both machines: <code>/av/myth</code>. It saw the filenames it expected in gwythaint:/av/myth and so it assumed that no update was needed, although the files were originally on falcon:/av/myth. So I created a symlink from <code>/av/myth</code> to <code>/av/myth-dummy</code> and added that to the storage group. Still, that did not help. </p>

<p>The final solution was to hack the database directly:</p>

<pre><code>mysql&gt; update recorded set hostname='gwythaint' where hostname='falcon';
Query OK, 53 rows affected (0.00 sec)
Rows matched: 53  Changed: 53  Warnings: 0
</code></pre>
