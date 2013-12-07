---
layout: post
status: publish
published: true
title: Local Caller ID Database
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 920
wordpress_url: urn:uuid:a0b6e5fd-4057-4443-8d74-8d16393f5abe
date: 2008-02-03 11:54:38.000000000 -08:00
tags:
- asterisk
- local
- sh
- cid
- callerid
- caller
- id
- astdb
comments:
- id: 1679
  author: Trevor Peirce
  author_email: ''
  author_url: http://www.cnam.info
  date: '2008-03-28 14:02:53 -0700'
  date_gmt: ''
  content: |-
    <p>One solutions to not receiving Caller ID Name is to use a third party service like this one.  It integrates with asterisk, FreePBX, trixbox, etc quite easily and will resolve names for nearly all of Canada/US.  </p>

    <p>It's <a href="http://www.cnam.info" rel="nofollow">http://www.cnam.info</a></p>
---
<p>If you use a VOIP provider for PSTN calls, you will be able to relate to the frustratingly boring caller ID names that get passed down to you. Very infrequently do I get anything better than a city name. Even if you have a direct PSTN connection into Asterisk, you may find the caller ID names from cell phone users (maybe just about everyone that calls you) are less than precise. Here's a solution.</p>

<p>We want to store alternative names in some kind of database that Asterisk can access when a call comes in. AstDB is perfect for this. We also want to leave things unchanged if we haven't manually stored a name for this number. The following will do the trick:</p>

<pre><code>    Set(CALLERID(name)=${IF(${DB_EXISTS(cid/${CALLERID(num)})}?${DB(cid/${CALLERID(num)})}:${CALLERID(name)})})
</code></pre>

<p>Now, we just need a way to update the database with names. At first I had grandiose ideas of an AJAX-enabled website that shows you the last few CDR records and lets you edit the names with a spiffy in-place editor. You could still accomplish it, but in the end I came up with a much simpler if less elegant solution. At least, it's simpler if you use the terminal all the time like I do. Put this script in your path:</p>

<pre><code>#! /bin/sh
# usage: $0 number "name"
user=`username`
host=falcon
exec ssh $host asterisk -rx \'database put cid \"$1\" \"$2\"\'
</code></pre>

<p>Combine this with jabber notification as I've discussed before, and a little cut &amp; paste from your jabber window, and updating names is cake.</p>
