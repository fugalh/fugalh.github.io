---
layout: post
status: publish
published: true
title: ssh tricks
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1105
wordpress_url: http://hans.fugal.net/blog/?p=1105
date: '2009-02-14 06:17:51.000000000 -08:00'
tags:
- linux
- ssh
- key
- config
- ControlPath
- ssh-copy-id
- id_rsa.pub
- authentication
- rsa
- tricks
comments: []
---
Dennis Muhlestein posted a <a href="http://allmybrain.com/2009/02/13/quick-ssh-tip/">quick ssh tip</a>, and then a couple of really neat gems emerged in the comments. For the sake of those who didn't click through, and my non-Utah readers, I repeat them here:

<ol>
	<li><code>ssh-copy-id</code> is a little utility to copy your public key to a remote server. Passwordless authentication has never been easier to set up!

<code>ssh-keygen -t rsa
ssh-copy-id $remote_host</code>
</li>

	<li><code>ControlPath</code> reuses the same connection for subsequent logins, so if you ssh into the same server from several terminals the logins after the first happen much faster. This is a really neat trick.

<code># in ~/.ssh/config
Host *
    ControlMaster auto
    ControlPath ~/.ssh/master-%r@%h:%p</code></li>
</ol>

