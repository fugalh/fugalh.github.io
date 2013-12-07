---
layout: post
status: publish
published: true
title: Only Share Some Printers
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 67
wordpress_url: urn:uuid:1eff239c-32ad-41cb-b371-d7c35dc45e05
date: 2005-08-04 11:14:38.000000000 -07:00
tags:
- linux
comments: []
---
<p>At work we have a server that has a bunch of printers that should not be
shared, and incidentally also happens to be the file/print server. The standard
cups which is so easy to implement shares all available printers, even the ones
we didn't want to share. Here's how to share only some.</p>

<p>First, we have to not share everything. To do that, remove (or comment out) the
<code>[printers]</code> section. It seems like <code>load printers = no</code> would be important
too, but I have not been able to discern any difference when changing that.</p>

<p>Second, you need to put a share for each printer. Well, with 52 printers that is tedious and prone to decay, so I wrote a script to generate the stanzas:</p>

<pre><code>#!/bin/sh
# cd /etc/samba
# ./gen_printers.sh &gt; printers.conf

printers=`lpstat -a | cut -d ' ' -f 1 | egrep -v '(label|DEVNULL|test)'`

echo "# auto-generated `date -R`"

for p in $printers; do cat &lt;&lt;EOF
[$p]
path=/var/spool/samba
printable = yes
public = yes
writable = no
browseable = yes

EOF
done
</code></pre>

<p>Now that you have printers.conf, you just need to include it from smb.conf, which you do like this:</p>

<pre><code>echo "include = /etc/samba/printers.conf" &gt;&gt; /etc/samba/smb.conf
</code></pre>

<p><em>Warning:</em> I tried putting the include directive in the <code>[global]</code> section and
it really messed with samba's mind, creating AWOL processes that needed to be
killed with signal 9 and other ugly stuff. I don't know if it was the
indentation or the file position, but it works best if you include it at the
end of the file instead.</p>
