---
layout: post
status: publish
published: true
title: Trashless
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 852
wordpress_url: urn:uuid:5b43b3d7-5002-47e5-99d4-4c971aace35b
date: 2007-07-17 16:03:57.000000000 -07:00
tags:
- mac
- trash
comments:
- id: 1585
  author: '"utrrrongeeb"'
  author_email: ''
  author_url: ''
  date: '2007-12-29 03:53:28 -0800'
  date_gmt: ''
  content: |-
    <p>Thank you for posting that tip on disabling trashes on a removable device in Leopard.
    My dad has been looking for how to do this, and [should] be happy to see this.</p>
- id: 1586
  author: Vitaliy
  author_email: ''
  author_url: ''
  date: '2008-04-18 07:22:22 -0700'
  date_gmt: ''
  content: <p>Thanks for the Flash command, I hate to have to always empty all my
    trash just to clean my flash.</p>
---
<p>In OS X, when you "delete" something in the Finder it ends up in the trash. Each device has its own trash, which makes a lot of sense, but can be problematic. </p>

<p>First, let's consider the real-world analogy that is the trash. When you have something you want to get rid of, you throw it in a trash can. Later, you empty the trash <em>at your convenience</em> at which point the stuff is really gone. In the meantime, you can dig through the trash and retrieve stuff you didn't really mean to throw away.</p>

<p>Now some people use the computer trash (or "Recycle Bin") as a sort of junk
drawer. They don't really want anything in there thrown away yet, they just
want it out of their face. This is bad, for the same reason that putting
something in the real trash that you might still want later is: someone might
empty the trash while your back is turned. This happens at our house all the
time—it's like magic. </p>

<p>On the other end of the stick are the people that berate the poor junk drawer souls, but don't flinch at having to empty the trash every time you turn around to accomplish something (see next paragraph). They're wrong too. The trash should be emptied when you feel like it and/or when you run out of trash can space.</p>

<p>Now, OS X doesn't afford the sane behavior because of the way it handles trash for removable drives. That is, it handles it the same as for permanent drives. When I delete something on my flash drive, it is still on my flash drive (in the trash) until I empty the one grand unified trash. In other words, you can't empty the bathroom trash without emptying every trashroom in the house. Also, you can't throw out those leftovers that have been rotting in tupperware for 3 weeks now unless you take out all the trash. </p>

<p>This is unfortunate for two reasons. First, since computer trash doesn't start to reek, we'd like to keep the trash around as long as we have spare disk space to do so, on the off chance we need something we deleted a few weeks ago. This is, after all, the whole point of having a trash can instead of instantaneous deletion, and the longer the better. Yes, it might fuel the junk drawer fire, but oh well. Second, taking out the trash to free up space is a bother, and the main trash usage pattern really is different from the delete-stuff-off-my-jump-drive usage pattern.</p>

<p>As an example, my MP3 player is a USB mass storage device. I put songs and podcasts on, and take them off, all the time. The Finder is more convenient than the commandline for this because of the file browsing nature of the task (not to mention spaces and special characters in the names of files). But when I press cmd-delete to delete the latest album I tired of, there's no more space than there was before. I have to empty my whole trash (or <code>rm -rf /Volumes/YEPP/.Trashes</code>) to reclaim it. This is unacceptable. </p>

<p>I found an elegant way to disable the trash on a device. That is, treat it more like a fridge than a house. It's quite simple:</p>

<pre><code>cd /Volumes/YEPP
rm -rf .Trashes
touch .Trashes
</code></pre>

<p>Now when you delete stuff, Finder will see that it can't make the <code>.Trashes</code> <em>directory</em>, because a file of that name already exists, so it wil confirm that you really want to permanently delete stuff, and not put it in the trash. Everyone's happy.</p>

<p>If you don't like the idea of no trash at all, I think you can set something up with Automator and some shell scripting to empty the trash. Here's a sample workflow: "Get Selected Finder Items", then "Run Shell Script" with the input as arguments:</p>

<pre><code>for i in "$@"; do
    if [ -d "$i"/.Trashes/501 ]; then
        rm -rf "$i"/.Trashes/501
        mkdir -p "$i"/.Trashes/501
    fi
done
</code></pre>
