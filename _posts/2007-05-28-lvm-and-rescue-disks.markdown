---
layout: post
status: publish
published: true
title: lvm and rescue disks
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 840
wordpress_url: urn:uuid:8a0f169e-3ed3-4c4d-9bca-663f576a75fe
date: 2007-05-28 20:45:19.000000000 -07:00
tags:
- linux
- lvm
- rescue
comments: []
---
<p>For the record, when you boot a system using LVM with a rescue CD you might
have to do the following:</p>

<pre><code>vgchange -a y $vgname
</code></pre>

<p>Where you get vgname via <code>vgscan</code>. Only then will you be able to mount the
logical volumes (which you can find with <code>lvscan</code>), e.g.</p>

<pre><code>mount /dev/VolGroup00/LogVol00 /mnt
</code></pre>

<p>This is one of those things that isn't too hard to learn, but when you need it
is the last time you want to be learning it.</p>

<p>You know how clowns run around tripping over things and hitting eachother with
mallets? That's what it feels like to be a pair of system administrators in the
room when a production server is down in the middle of the day. Not the time to
be wondering why you can't access your LVM root partition.</p>
