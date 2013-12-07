---
layout: post
status: publish
published: true
title: Testing/Unstable Mix with apt-get
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 35
wordpress_url: urn:uuid:c0a6ed13-2dff-4890-a8ce-5e87dfa44cd1
date: '2004-12-14 09:54:01.000000000 -08:00'
tags:
- linux
comments: []
---
<p>I like to run testing, but sometimes you just need that unstable package now. Here's how:</p>

<pre><code># /etc/apt/preferences
Package: *
Pin: release a=testing
Pin-Priority: 900

Package: *
Pin: release a=unstable
Pin-Priority: 800

Package: *
Pin: release a=experimental
Pin-Priority: 700


# /etc/apt/apt.conf
APT::Default-Release "testing";

# /etc/apt/sources.list
# put both testing and unstable lines here
</code></pre>

<p><em>Note</em>: if you don't do the preferences and apt.conf stuff, you'll end up
grabbing unstable by default and soon you'll be running unstable not testing.</p>
