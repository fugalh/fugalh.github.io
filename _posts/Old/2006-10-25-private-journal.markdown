---
layout: post
status: publish
published: true
title: Private Journal
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 742
wordpress_url: urn:uuid:7bafc46f-c3bd-429f-9655-cd9c3e6de132
date: '2006-10-25 09:56:22.000000000 -07:00'
tags:
- journal
- gpg
- encryption
comments: []
---
<p>So you want to keep an encrypted journal? It's amazingly easy. Basically, you want to email your encrypted entries to yourself, that way you can peruse them using your favorite gpg-enabled mail client at your leisure. Here's how I do it with mutt. I made a script <code>~/bin/journal</code> like so:</p>

<pre><code>#!/bin/sh
subj=`date`
to=you+journal@example.com

mutt -e "set pgp_autoencrypt=yes" -s "$subj" "$to"
</code></pre>

<p>Assuming you have created a gpg key and have the public key to match
you+journal@example.com in your keyring, your journal email will
automatically be encrypted and ready for later secure perusal. The only concern
for the truly paranoid is the <code>$EDITOR</code> temporary file and unprotected RAM, but
I'll assume you're not that paranoid (I'm not).</p>

<p>Here's a procmail rule to go along with the script:</p>

<pre><code>:0
* ^TO_you\+journal
journal/
</code></pre>
