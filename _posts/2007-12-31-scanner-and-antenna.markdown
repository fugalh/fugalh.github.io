---
layout: post
status: publish
published: true
title: Scanner and Antenna
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 917
wordpress_url: urn:uuid:7722e04a-014e-443b-bfdb-2f4fed87bf63
date: '2007-12-31 12:07:53.000000000 -08:00'
tags:
- aviation
- radio
- antenna
- scanner
comments: []
---
<p>I got a handheld radio scanner for my birthday and Christmas with the cash I received (thanks, everyone!). I got a <a href="http://www.radioshack.com/sm-pro-84-compact-scanner-and-headphone-bundle--pi-2180625.html">RadioShack PRO-84</a> on sale for $60. It can scan lots of different things, but I'm primarily interested in listening to aviation communications, which is from 108 MHz to 137 MHz. I've found the scanner to be quite satisfactory, with the minor annoyance that it is difficult to listen to an arbitrary frequency without assigning it to one of the 200 numbered channels (so I pick a channel or two as my temporary channels).</p>

<p>Although it works great for listening to traffic at the airport, for listening to traffic away from the airport (e.g. at home), the included "rubber duckie" antenna is not up to the task. So I set about making my own. </p>

<p>I went from knowing nothing about antennas to knowing just enough to sound like I know what I'm talking about, and apparently to build a simple one. I learned a few interesting things in the process.</p>

<p>One simple and decent antenna is the dipole. You may be familiar with a version of the dipole known as rabbit ears. What you may not realize is that the rabbit ears work best completely horizontal (not in a V shape) and adjusted in length to match the frequency of the desired television station. Also, they need to be pointed in the right direction (broadside the transmitter) for best reception, and they should be away from the TV. So much for TV antennas.</p>

<p>So I had decided on making a dipole, and started seeing claims that this variation called the <a href="http://k7mem.150m.com/Electronic_Notebook/antennas/folded_dipole.html">folded dipole</a> is "quieter" and has "more bandwidth". It is almost as simple to make as a dipole, so I decided to go with that. Now it was time to figure out how to make it cheaply. I'm happy to report I was able to make the antenna for $5 and change, and it works quite well. I am sitting in Pleasant Grove, scanner and antenna indoors, listening to Provo traffic, including planes on the ground. I imagine I'll have similar results at home where the terrain profile is similar between my house and the airport.</p>

<p>So here's what I did. I bought some <a href="http://en.wikipedia.org/wiki/Twin-lead">TV twinlead</a> (that stuff with two wires separated by insulation), one of those TV <acronym title="Balanced/Unbalanced">balun</acronym> things,  and a TV coax to BNC adapter. I cut the twin lead to 52 inches, then twisted the two wires together at each end. Then I cut one of the wires in the center and screwed the two leads to the balun. Then I attached the balun to the BNC connector and hooked it up to the radio. The improvement over the rubber duckie is very apparent. </p>

<p><img src="http://upload.wikimedia.org/wikipedia/en/thumb/b/bb/Tvbalun.jpg/180px-Tvbalun.jpg" alt="TV Balun"/></p>

<p>I also toyed with just hooking one lead of the original 6-foot length of twin lead directly to the center of the coax/BNC adapter. This also works well (I presume this is a random wire antenna), and you could probably also use a coat hanger. This would make a good portable antenna for visiting the airport. Look, two antennas in one!</p>

<p>Here's some techincal tidbits about the antenna I made. 52 inches corresponds to 108 MHz. I will probably trim it to 122.7 MHz (KLRU CTAF) when I get home, but I wanted to err on the side of too long to start with. A folded dipole is 300Ω balanced, and my scanner wants a 50Ω unbalanced connection, which is where the balun comes in. It converts to 75Ω unbalanced, which is still not a perfect match but seems to work well enough. I have since found plans for what's called a "coaxial dipole", or "double bazooka" antenna, which claims to not need a balun and match 50Ω. There are also plans for a <a href="http://www.tuc.nrao.edu/~demerson/twelfth/twelfth.htm">twelfth-wave matching transformer</a> that will match 75Ω to 50Ω with about a foot of coax, but you need both 50Ω and 75Ω coax to do it. The cost of that could be a few cents if you have spare coax lying around, or $20 if you have to buy it new. If I have unsatisfactory reception at home, I may try the bazooka and/or the transformer and report.</p>
