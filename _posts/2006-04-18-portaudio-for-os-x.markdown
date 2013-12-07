---
layout: post
status: publish
published: true
title: PortAudio for OS X
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 119
wordpress_url: urn:uuid:e8e5f1e9-4dc5-497a-a475-97a87c67fb0a
date: 2006-04-18 22:03:00.000000000 -07:00
tags:
- audio
- mac
- osx
- PortAudio
- framework
comments:
- id: 1459
  author: Eric
  author_email: ''
  author_url: ''
  date: '2006-05-09 00:10:44 -0700'
  date_gmt: ''
  content: <p>Hans, you rock.  - dilvie</p>
- id: 1460
  author: scottdo82@gmail.com
  author_email: ''
  author_url: ''
  date: '2008-02-25 15:06:04 -0800'
  date_gmt: ''
  content: <p>I know this is an old post, but if this should happen to get to you...do
    you still have that XCode project that you used to build the PortAudio Framework?  It'd
    really help me out to be able to look at it.  Thanks.</p>
- id: 2374
  author: Bee
  author_email: infos@bienentendu.fr
  author_url: ''
  date: '2011-03-28 08:55:37 -0700'
  date_gmt: '2011-03-28 08:55:37 -0700'
  content: "ooohhh\r\nSame question\r\ndo you still have this xcode project ???\r\nthanks
    in advance"
---
<p><a href="http://www.portaudio.com/">PortAudio</a> is a portable cross-platform API. But it
seems like none of the developers has access to a mac because the docs for
getting started with <a href="http://www.portaudio.com/docs/pa_tut_mac_osx.html">PortAudio on OS
X</a> are a sorry joke. </p>

<p>I took the liberty of figuring it all out in XCode and creating a
<a href="http://hans.fugal.net/src/PortAudio.dmg">PortAudio.framework</a> which is a piece
of cake to use. Download it, move the resulting PortAudio.framework folder to
<code>/Library/Frameworks</code>, include as <code>#include &lt;PortAudio/portaudio.h&gt;</code>, and link
with <code>-framework PortAudio</code>. If you use XCode, include the same way and just
add the framework to your project and it takes care of the linking.</p>

<p>If you want the XCode project that I used, contact me. I don't have any qualms
about sharing it, I'm just too lazy. I didn't change any code, I just made an
XCode project to build the framework. Incidentally, all the documentation and
READMEs and license files are still in the framework, which is just a folder
which you can browse in the finder.</p>

<p>Enjoy!</p>
