---
layout: post
status: publish
published: true
title: TerraSync Prefetch
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 845
wordpress_url: urn:uuid:231660d1-d09b-4016-81c4-c326d09e0f6d
date: '2007-06-05 10:54:38.000000000 -07:00'
tags:
- flightgear
- terrasync
comments:
- id: 1580
  author: momomoko
  author_email: midnight_warrior69@hotmail.com
  author_url: ''
  date: '2007-08-14 21:49:59 -0700'
  date_gmt: ''
  content: |-
    <p>so if i type terrasync-prefetch.sh into the command shell and start flight gear will it work?
    (sorry if its a noob question)</p>
- id: 1581
  author: Hans
  author_email: ''
  author_url: ''
  date: '2007-08-14 21:58:11 -0700'
  date_gmt: ''
  content: |-
    <p>Yes, download it, then type:</p>

    <pre><code>  chmod 755 terrasync-prefetch.sh
      ./terrasync-prefetch.sh
    </code></pre>
- id: 1830
  author: Gabriel
  author_email: gabars@live.ca
  author_url: ''
  date: '2009-02-10 02:10:07 -0800'
  date_gmt: '2009-02-10 02:10:07 -0800'
  content: Sorry if the last post is 2 years old but please tell me where to download
    Terrasync for FGFS.
---
<p>TerraSync is a nice little utility included with FlightGear that downloads scenery on the fly. It works like a charm, but there's one caveat. FlightGear wants the scenery <em>right now</em> and TerraSync needs to download it first, therefore the first time you start FlightGear in a new area (or "teleport" there), you won't have scenery. TerraSync will be busily downloading it in the background, though, so you just restart FlightGear a minute later, et voilá! But starting FlightGear that first time is a waste of time, since it takes forever to parse its config files and do a bunch of other stuff before it even tries to get the scenery. So I wrote <a href="http://hans.fugal.net/src/terrasync-prefetch.sh">a little shell script</a> to do the job quicker.</p>

<p>Incidentally, this is the script I use to start FlightGear. It starts TerraSync if it's not already running:</p>

<pre><code>#!/bin/sh
PORT=5500
FG_HOME=$HOME/.fgfs
FG_ROOT=/usr/local/share/FlightGear
TERRASYNC_DIR=$FG_HOME/Scenery
FG_SCENERY=$TERRASYNC_DIR:$FG_ROOT/Scenery

pgrep terrasync || \
nice terrasync -p $PORT -d $TERRASYNC_DIR &gt;&gt; $FG_HOME/terrasync.log &amp;

/usr/local/bin/fgfs --atlas=socket,out,1,localhost,$PORT,udp $*
</code></pre>
