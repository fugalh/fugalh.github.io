---
layout: post
status: publish
published: true
title: The Wonder Shaper
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 103
wordpress_url: urn:uuid:932e32a4-8dfb-4d6d-b0e7-a07967cfc905
date: 2005-09-05 10:11:07.000000000 -07:00
tags:
- voip
- qos
comments: []
---
<p>When we moved to <a href="http://maps.google.com/maps?q=las+cruces,+nm&amp;spn=.138376,.193085&amp;hl=en">Las Cruces</a> I ditched Qwest for telephone service, and went with standalone DSL, <a href="http://asterisk.org">Asterisk</a>, and <a href="http://www.nufone.net">NuFone</a> for my phone service. The other day someone was downloading stuff from my website, using all my upload bandwidth, and my wife was trying to talk to someone on the phone. Although she could hear them just fine, they couldn't hear a thing she said because she was breaking up so bad. Thus began my quest for QoS.</p>

<p>Actually, I had downloaded and set up a script to do QoS that I got from the <voip-info.org> wiki, and I forgot to reconfigure it to my current bandwidth. So ironically, undoing what that script did helped just because it let me use all of my bandwidth. Then I tried to adapt the script to my current situation, and found that it didn't really work. So I went to the <a href="http://lartc.org">lartc</a> and read up on Queueing Disciplines and tried to make my own VOIP QoS script. I spent hours on this, and although I gained a pretty good understanding of it all I never did get a script that worked well. It kind of worked, but not well enough.</p>

<p>This morning, I stumbled across the <a href="http://lartc.org/wondershaper">Wonder Shaper</a> and decided to give it a try. If it didn't work well for VOIP at least I'd have a starting point for modifications.  The results were truly wonderful. I was able to carry on a normal conversation with my mother while uploading an ISO with scp to <a href="http://www.xmission.com">my ISP</a>.  </p>

<p>The added bonus of having really great performance for other interactive applications such as ssh has really sold me on the Wonder Shaper. Even if you don't do VOIP, you should give it a try. If you have a recent kernel it's so easy to use, and has such great returns, that you would be foolish not to.</p>
