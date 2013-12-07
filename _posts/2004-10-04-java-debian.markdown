---
layout: post
status: publish
published: true
title: Java on Debian Quick
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 55
wordpress_url: urn:uuid:fe09c215-5840-405a-b495-b6e7e14f15b5
date: 2004-10-04 11:10:58.000000000 -07:00
tags:
- linux
comments: []
---
<ol>
<li>Download the "Linux Binary" j2se jdk from java.sun.org</li>
<li>Run the binary</li>
<li>mv the resulting jdk directory (e.g. jdk1.5.0) to /usr/local/lib (or /usr/lib if you prefer)</li>
<li><code>ln -s /usr/local/lib/jdk1.5.0 /usr/local/lib/jdk</code></li>
<li><p>Install java-virtual-machine-dummy and make /etc/java-vm look like this (3 lines):</p>

<p><code>/usr/local/lib/jdk/bin/java</code></p>

<p><code>COMPLIANT</code></p></li>
<li><p><code>update-alternatives --config java</code></p></li>
<li><code>update-alternatives --install javac javac /usr/local/lib/bin/javac 1 --slave javac.1.gz javac.1.gz /usr/local/lib/jdk/man/man1/javac.1</code></li>
<li><code>update-alternatives --config javac</code></li>
<li>You might need to <code>ln -s /etc/alternatives/javac /usr/bin/javac</code></li>
</ol>
