---
layout: post
status: publish
published: true
title: Buffalo AirStation WHR-G54S
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 597
wordpress_url: urn:uuid:367ab172-728e-4bab-8dfd-85106cd1998a
date: 2006-06-22 12:39:00.000000000 -07:00
tags:
- review
- hardware
- buffalo
- wireless
comments: []
---
<p>For the price of a new Actiontech DSL modem/wireless router, I purchased a used
Cisco 678 and a <a href="http://buffalotech.com/products/product-detail.php?productid=117&amp;categoryid=30">Buffalo AirStation
WHR-G54S</a>.
I don't need to tell you which is the better deal. </p>

<p>I've been hearing some good things about Buffalo, and since you can't be sure
what you're getting with a Linksys Wireless router these days I decided to go
for it. I've just finished configuring it and now I have some opinions to spout.</p>

<p>First, it seems like a good router. It's pretty, has 4 ethernet ports, a WAN
port, and wireless (of course), it's working fine, it's very configurable,  and
it's reported that <a href="http://openwrt.org/">OpenWRT</a> runs on it. The cons are that
it takes a lot of rebooting to configure, the wired port LEDs are in the back,
and some of the terminology is a bit confusing. For example it does support WPA
but nowhere in the manual is it called WPA, and only as an aside in the web
interface do you realize that "AES" is WPA, when it asks for the WPA
"previously-shared" key. </p>

<p>Some highlights from the configuration, that I had plenty of time to ponder
while rebooting after every screen:</p>

<ul>
<li>WAN
<ul>
<li>Does PPPoE, DHCP, unnumbered IP, or static</li>
<li>can set the MAC address</li>
</ul></li>
<li>LAN
<ul>
<li>lots of DHCP server options</li>
</ul></li>
<li>Misc
<ul>
<li>NTP</li>
<li>Syslog</li>
<li>Very detailed system info screen </li>
<li>Logs, and granular control over what's logged (or what's sent to syslog)</li>
</ul></li>
</ul>
