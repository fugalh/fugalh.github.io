---
layout: post
status: publish
published: true
title: An Heir to SER
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 811
wordpress_url: urn:uuid:5e378cf0-6060-4b2a-be2a-a1fdf52a0a2d
date: 2007-03-02 10:03:00.000000000 -08:00
tags:
- voip
- ser
- sip
- router
comments:
- id: 1564
  author: Levi
  author_email: levi@cold.org
  author_url: http://lifeoflevi.com/blog/
  date: '2007-03-02 11:58:04 -0800'
  date_gmt: ''
  content: |-
    <p>Looks like you won't have to write it:</p>

    <p><a href="http://www.stacken.kth.se/project/yxa/" rel="nofollow">http://www.stacken.kth.se/project/yxa/</a></p>

    <p>I have no idea how good it is, but looking at it might help you decide if you think Erlang is the way to go.  Perhaps you could help out with it, or perhaps it will send you in another direction.</p>
- id: 1565
  author: malcontent
  author_email: ''
  author_url: ''
  date: '2007-04-25 16:46:46 -0700'
  date_gmt: ''
  content: |-
    <p>yxa looks pretty decent. Not quite an asterisk replacement but maybe someday...</p>

    <p>It does seem odd that erlang does not have a full fledged PBX software yet. What's an open telephony platform without good VOIP support?</p>
---
<p><a href="http://www.iptel.org/ser/">SER</a> (and <a href="http://www.openser.org/">OpenSER</a>) is a SIP router. That is, it receives SIP messages and decides where to send them or how to reply to them, in order to connect the two endpoints of a SIP call. It doesn't do media, it doesn't do voicemail or IVR or PBX or any of these other things. It's focus is routing, and it does it well and fast, and can handle a whole boatload of traffic.</p>

<p>But SER is not perfect. In fact, I would classify SER as barely adequate. In my
opinion, a SIP router should be four things:</p>

<ul>
<li>Robust</li>
<li>Powerful</li>
<li>Scalable</li>
<li>Easy to Administer</li>
</ul>

<p>By robust I mean it doesn't crash, it's fault-tolerant, and it doesn't require 'reboots' (of the software, not the OS). I like to call this lack of reboot the "living" property, following Steve Yegge's post <a href="http://steve-yegge.blogspot.com/2007/01/pinocchio-problem.html">The Pinocchio Problem</a>. SER is fairly robust, in that if you have a good dialplan and no flaky modules it doesn't crash often, and it's tolerant of rogue packets and other external problems. It is most definitely <em>not</em> living software though, and the constant restarting of the server during development and debugging is a serious problem. </p>

<p>By powerful I mean you can do whatever you need or want to do. You want to hook it up to your database for user authentication. You want to send yourself a Jabber message when Such and Such calls So and So. You want to do least-cost routing or some kind of convoluted load balancing that nobody has ever tried before. This is power. SER has this power, ultimately, through writing modules and using the exec module, it can be difficult (writing a C module), expensive (spawning a new process for every message!), or both. SER is severly limited by its scripting language which has no concept of variables (except storing stuff in an RDBMS with <acronym title="Attribute/Value Pairs">AVP</acronym>s) and almost no string processing abilities.</p>

<p>By scalable I don't mean speed (though speed can't hurt), but throughput. One
SER server can handle on the order of 6000 SIP messages per second. (Your
mileage may vary, depending on what you're doing and how you do it.) This is
where SER really shines. You might even say it's SER's raison d'être. It's also
important to be able to distribute load across multiple servers. You can <a href="http://www.iptel.org/faq/how_can_i_get_load_balancing_failover_with_ser">do
this</a>
with SER also.</p>

<p>By easy to administer I mean that a normal human being should be able to configure the daemon, write the routing scripts, and <em>debug</em> the routing scripts. Given, the person doing the routing scripts will need to have a solid understanding of SIP. But with SER, you have to practically be a SIP guru in order to set up even a basic route script. The scripting syntax is simple enough, but as mentioned above the limitations make doing anything nontrivial a real acrobatic programming trick. Don't even get me started on SER route script debugging. I'll just say it involves <code>ngrep</code> and either very terse and unhelpful logs, or very verbose and unhelpful logs.</p>

<p>Ok, so we see how SER measures up to my ideal. What can be done? Can the SER people step up to the plate and bridge the gap? Anything is possible, but I'm not holding my breath. Why not? Because of technical and architectural reasons, let alone community reasons. Technical because SER is written in C, and C makes things hard, and when things are hard niceties like living software often don't happen. Architectural because SER is locked into their scripting language and the design decisions that go along with that. They'd have to break compatibility (or walk on eggshells) to fix that. Even if they surprise us in these areas, there's still the difficulty of writing modules and extensions in C.</p>

<p>No, we can't expect the SER people to make this leap for us. They might, and
that would be nice, but let's not count on it. So where does that leave us? A
SER heir could be written with these four aspects in mind. I think it could be
done and done well if the right tools are chosen. Although I'm not 100% sure
yet, I think the most important tool will be <a href="http://www.erlang.org/">Erlang</a>.
Erlang almost solves the robust and scalable aspects from the very start.
Erlang makes living software almost by default. Erlang was designed by and for
the telephony industry. Erlang has good performance. The only part I'm not sure
about yet (because I'm not familiar enough with Erlang), is whether it will be
easy or hard to do routing scripts. Obviously, I think, you wouldn't ask
sysadmins to write them in Erlang. It's a language with a different paradigm
and that would be a serious barrier to entry. However, it would be nice to
allow scripting to be done in Erlang for those with that skill. I don't know
whether it will be hard to make a sensible <acronym title="Domain Specific
Language">DSL</acronym> in Erlang or not. Based on my experience with
<a href="http://ejabberd.jabber.ru/">ejabberd</a> the daemon running/interaction might
need some TLC, but I'm confident that can be accomplished with a few good shell
scripts.</p>

<p>Will I write it? Not while you're looking. But I do want to learn Erlang and I
do like to do real programs when learning a language. So don't be surprised if
an infant heir to the throne of SER comes out of left field some day.</p>

<p>In the meantime, please enjoy <a href="http://video.google.com/videoplay?docid=-5830318882717959520">Erlang: The Movie</a>.</p>
