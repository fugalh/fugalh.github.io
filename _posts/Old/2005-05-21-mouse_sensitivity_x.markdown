---
layout: post
status: publish
published: true
title: Trackpad Sensitivity
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 80
wordpress_url: urn:uuid:accd56fa-7742-4dce-b9b0-e780df52aa80
date: '2005-05-21 09:31:30.000000000 -07:00'
tags:
- mac
comments: []
---
<p>I thought the trackpad in XFree86 (Debian) on my iBook was set to turbo or
something.  I tried <code>xset m 1</code> and that helped but it was still too sensitive.
The problem turned out to be <a href="http://differentpla.net/node/view/377">something I didn't
expect</a>: both the "Configured Mouse" and
"Generic Mouse" sections were sending events. I changed two lines in my
ServerLayout section, so it now looks like this:</p>

<pre><code>Section "ServerLayout"
    Identifier    "Default Layout"
    Screen        "Default Screen"
    InputDevice   "Generic Keyboard"
    #InputDevice  "Configured Mouse"
    InputDevice   "Generic Mouse" "CorePointer"
EndSection
</code></pre>

<p>My trackpad has dropped out of warp.</p>
