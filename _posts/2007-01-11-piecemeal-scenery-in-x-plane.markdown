---
layout: post
status: publish
published: true
title: Piecemeal Scenery in X-Plane
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 775
wordpress_url: urn:uuid:83a426ef-5854-4083-b5ad-83d0849e600b
date: 2007-01-11 09:34:41.000000000 -08:00
tags:
- x
- plane
- scenery
comments: []
---
<p>Hypothetical situation: you buy (or receive as a gift) a copy of <a href="http://x-plane.com">X-Plane</a> with the entire World Scenery which is shipped on 6 DVD-ROM, and you're a cheapskate that doesn't happen to have 60+ gigabytes of free hard disk space. You might want to grab scenery piecemeal from the DVDs so you can fly all the places around the world that you want and ignore the rest. Here's how.</p>

<p>Stick one of the DVDs in. I'll put in the Canada and Alaska one. I have nothing against Canada, it's a cool place, but let's say I just want Alaska. In fact, let's say I'm really boring and just want the area covered by the Juneau sectional chart. A quick peek at <a href="http://skyvector.com">SkyVector</a> indicates we want roughly 57&deg; north 141&deg; west to 60&deg; north 130&deg; west. (X-Plane's scenery DVDs don't cover north of 60&deg; north latitude, unfortunately)</p>

<p>On the DVD in the directory <code>Canada/All</code> is a directory named <code>Resources</code> which
is analogous to the <code>Resources</code> directory in your <code>X-Plane 8.50</code> directory
where X-Plane is installed. Under that, if you dig a few directories down, is a
directory for each 10&deg; square, which in turn contains a zipped <code>.dsf</code> file
for each 1&deg; square of scenery. So, from the root of the DVD we have e.g.
<code>Canada/All/Resources/default scenery/DSF 820 Earth/Earth nav data/+50-140/</code>
which is the 10&deg; tile whose lower-left corner is 50&deg; north 140&deg;
west. So we want the tiles <code>+50-150</code> and <code>+50-140</code>. Density is pretty sparse
way up here, and there's a big chunk of ocean, so we can just copy those two
directories to e.g. <code>X-Plane 8.50/Resources/default scenery/DSF 820 Earth/Earth
nav data/</code>. If we wanted to drill down even more, we'd recreate the 10&deg;
tile directory and copy in the <code>.dsf</code> file for the 1&deg; tile we want. </p>

<p>So now that you've copied things over, you still need to unzip the <code>.dsf</code>
files. You could write a script to do that, or to unzip them into place instead
of copying the zip files in the first place.</p>

<p>Now you can fly X-Plane at the places that interest you without buying another hard drive. It bears mentioning that if you use <a href="http://flightgear.org/">FlightGear</a> you could <a href="http://flightgear.org/Downloads/scenery.html">download 10&deg; scenery chunks</a> without buying DVDs, or even better you can run terrasync and get the 1&deg; tiles just in time. More on X-Plane vs. FlightGear later...</p>
