---
layout: post
status: publish
published: true
title: Thoughts on Code as Design
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 12
wordpress_url: urn:uuid:742abd7d-cf56-4759-8712-a933131065a5
date: 2005-03-03 13:13:56.000000000 -08:00
tags:
- cs
comments: []
---
<p>I just read <a href="http://www.developerdotstar.com/mag/articles/PDF/DevDotStar_Reeves_CodeAsDesign.pdf">Code as Design: Three Essays by Jack W.
Reeves</a>.
I highly recommend reading it. It has given me a new perspective and I find
that it rings true in many ways.</p>

<p>I often tell people that I like "designing" software more than coding it. I was
drawing that imaginary line in the sand that so irritates Reeves, and finding
that I preferred the top-level design side of it. In reflection, since reading
his essays, I will be changing that standrad speel as I now better understand
my own feelings on the matter.  I enjoy the whole process. I do like top-level
design most, for I am a dreamer. But top-level design doesn't give the
endorphin rush that coding does when you begin laying out the code that turns
the sea of ideas in your head into a real, working system. In retrospect, I do
enjoy coding and always have - what I don't enjoy is converting a "design" into
code. That goes for my own "designs" as much as for those written by others. </p>

<p>Lately I've been following his suggestion in a subconscious way, out of
necessity. I am working as a system administrator which means very little
software development in the day job. So I have several side projects I'm
playing with, but the scarcity of time has compelled me to spend less time
fiddling with "design" and more time creating <em>design</em> (code). I haven't
neglected top-level design, and especially not the deep thought that I put into
a project at the beginning. It's been more of a rebellion against extra
"design". </p>

<p>For a fabulous concrete example, I present the work I've done so far on
<a href="http://hans.fugal.net/src/alex/">alex</a>. Alex is a softphone that I am writing,
because I have found all available softphones on linux to be inadequate and
fundamentally flawed, for what I want to do with them. I thought through major
components of alex - audio, network, UI. Then I started the skeleton. Then I
started to get lost so I fired up umbrello and made some basic UML. Then I
started to code and saw some fundamental flaws. So I completely reworked the
UML. Then I started to refactor the code and saw some detail changes that
needed to take place. Propogating those detail changes back to UML quickly
became incredibly loathsome, so I stripped the UML of almost all detail,
leaving it as a shell of top-level design that does what it's supposed to do:
show you the top-level design, without bogging you down in details. I'm very
happy with it, for now, and I'm happily coding away the details, changing the
class and interface design details as I go. The whole process is very fluid,
and very satisfying. I feel like I understand the design and the code very
well. I've been building up to this, gradually swapping my love for OO and
design out for a love for getting something done. "Release early, release
often" and all that other stuff. </p>

<p>In summary, I think I've missed out in some ways because I was looking down my
nose at coding. I've often had the unpleasant feeling of having too many dreams
and not enough to show for it. I have for some time now been trying to act more
on those dreams and not let them fizzle until they are dead, and these essays
have given me a new perspective that I believe will be profitable in that
pursuit. Thank you, Jack.</p>
