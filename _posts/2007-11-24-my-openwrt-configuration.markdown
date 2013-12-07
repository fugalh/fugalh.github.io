---
layout: post
status: publish
published: true
title: My OpenWRT Configuration
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 907
wordpress_url: urn:uuid:df5726c7-399f-49a0-8a49-95af4e4e131b
date: '2007-11-24 08:47:00.000000000 -08:00'
tags:
- linux
- router
- openwrt
- embedded
- qos
- vlan
- subnet
comments:
- id: 1664
  author: JJ
  author_email: calliope_jja@yahoo.com
  author_url: http://www.modernpunches.org
  date: '2008-03-03 08:42:21 -0800'
  date_gmt: ''
  content: <p>That is very tedious work! Good job. You were able to fix everything!</p>
- id: 1665
  author: John
  author_email: webdb22@hotmail.com
  author_url: ''
  date: '2008-03-26 14:50:29 -0700'
  date_gmt: ''
  content: |-
    <p>Hi!</p>

    <p>Very detailed description! Great! I've a very similar setup, only using Tomato firmware instead of OpenWRT. I've tried to follow your example, but I'm stuck :-( Could you elaborate a bit more on the topology, IP adresses and networks? I can't match your "/29 subnet: .205–.210 (6 hosts)" to the "route add" commands. Maybe an extended drawing would be helpful?!</p>

    <p>Thanks a lot,</p>

    <p>John</p>
- id: 1666
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-03-26 18:16:20 -0700'
  date_gmt: ''
  content: |-
    <p>Here's what <code>ipcalc</code> has to say:</p>

    <pre><code>
    Address:   216.31.27.105        11011000.00011111.00011011.01101 001
    Netmask:   255.255.255.248 = 29 11111111.11111111.11111111.11111 000
    Wildcard:  0.0.0.7              00000000.00000000.00000000.00000 111
    =>
    Network:   216.31.27.104/29     11011000.00011111.00011011.01101 000
    HostMin:   216.31.27.105        11011000.00011111.00011011.01101 001
    HostMax:   216.31.27.110        11011000.00011111.00011011.01101 110
    Broadcast: 216.31.27.111        11011000.00011111.00011011.01101 111
    Hosts/Net: 6                     Class C
    </code></pre>

    <p>And here are the <code>ip route</code> commands again with annotations:</p>

    <pre><code>
    # Nuke the default route
    ip route del default
    # Delete the route for my /29 network through the cisco
    ip route del 216.31.27.104/29 dev vlan1
    # Add the route for my /29 network through the LAN
    ip route add 216.31.27.104/29 dev br0
    # Except the cisco which is the only device in this network out vlan1.
    ip route add 216.31.27.105 dev vlan1
    # And now the default route is through the cisco.
    ip route add default via 216.31.27.105
    </code></pre>

    <p>Hope that helps.</p>
- id: 1667
  author: John
  author_email: webdb22@hotmail.com
  author_url: ''
  date: '2008-03-27 02:50:58 -0700'
  date_gmt: ''
  content: |-
    <p>Thanks for your immediate reply! </p>

    <p>Based on your answer I assume in the second paragraph of the original post it should read "/29 subnet: .105–.110 (6 hosts)"? And further down the IP of the Cisco is meant to be "216.31.27.109"?</p>

    <p>Unfortunately there is no "init.d", "sysctl.conf", etc. in the Tomato firmware <a href="http://www.polarcloud.com/tomato/" rel="nofollow">http://www.polarcloud.com/tomato/</a> . How to achieve this anyhow? Maybe using the "Scripts" in the the WebInterface?</p>
- id: 1668
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-03-27 07:52:14 -0700'
  date_gmt: ''
  content: |-
    <p>Yes, I had some typos. Oops! The cisco is .105, which was also a typo. I've fixed them in the article now. Thanks.</p>

    <p>I don't know about Tomato, but if there's some way to run a startup script you can do everything in that. Without sysctl.conf you'll need to do e.g.:</p>

    <pre><code>echo 0 &gt; /proc/sys/net/ipv4/conf/all/arp_ignore
    </code></pre>
---
<p>I had the unfortunate occasion of reconfiguring my OpenWRT router after a fresh reflashing yesterday, without sufficient notes of how I had it set up. So, I'm documenting it this time. But it's not just notes for myself—I'm doing a few tricks that my dear readers might learn from.</p>

<p>First, the topology. I have a /29 subnet: .105–.110 (6 hosts). There is a Cisco DSL modem, a Buffalo router (running OpenWRT), my main server named falcon, a Sipura <acronym title="Analog Telephone Adapter">ATA</acronym>, a desktop, and my laptop. The latter 4 are collectively the public-IP LAN, and the topology looks like this:</p>

<pre><code>(internet) -- cisco -- buffalo +- public-IP LAN
                               |
                               +- private-IP LAN
</code></pre>

<p>The private-IP LAN is 172.17.77.0/24, and primarily for guest wireless devices or whatever other devices I happen to want to plug in.</p>

<p>The buffalo has one internal switch, to which is connected the wireless radio and 5 ethernet ports. It is split into 2 VLANs. vlan1 is the port connected to the cisco (.105), and the other ports and the wireless are bridged as br0 (with a private IP: 77.2). </p>

<p>Now remember, The cisco, buffalo, and public-IP LAN are all on the same /29 subnet. But the cisco and the public-IP LAN are on different VLANs. Let that sink in. You should be objecting about now, and questioning my sanity. (If you're not familiar with the term VLAN, it basically is a way to partition the broadcast domain.) How can I have two independent broadcast segments for one subnet?</p>

<p>Here's what the routing on the buffalo looks like:</p>

<pre><code># ip route
216.31.27.105 dev vlan1  scope link
216.31.27.104/29 dev br0  scope link
172.17.77.0/24 dev br0  proto kernel  scope link  src 172.17.77.2
default via 216.31.27.105 dev vlan1
</code></pre>

<p>and this is how it is achieved:</p>

<pre><code># cat /etc/init.d/S41routing
ip route del default
ip route del 216.31.27.104/29 dev vlan1
ip route add 216.31.27.104/29 dev br0
ip route add 216.31.27.105 dev vlan1
ip route add default via 216.31.27.105
</code></pre>

<p>So everything in .104/29 goes to the right, and only traffic to the cisco goes to the left. Of course the private subnet goes to the right too. The default route is via the cisco. (Incidentally, you need to install iproute2 for using ip: <code>ipkg install ip</code>)</p>

<p>You also need to configure a static route on the cisco:</p>

<pre><code>set route add ip 216.31.27.104 netmask 255.255.255.248 gw 216.31.27.109
</code></pre>

<p>Remember though that the left-hand IP of buffalo is 216.31.27.109, and the right-hand IP is 172.17.77.2. So if falcon, which is on the right, tries to reach .109 (its default route), will it get an ARP response? The answer is, it depends. It depends on the effective <code>arp_ignore</code> sysctl setting. By default on OpenWRT 0.9 (White Russian), <code>/proc/sys/net/ipv4/conf/{default,all}/arp_ignore</code> is set to 1. This means "reply only if the target IP address is local address configured on the incoming interface", which means buffalo won't reply to ARP requests for .109 coming from the right. We need to set <code>arp_ignore</code> to 0 for that interface, meaning "reply for any local target IP address, configured on any interface." How do we do that?</p>

<p>"The max value from <code>conf/{all,$interface}/arp_ignore</code> is used when ARP request is received on the <code>$interface</code>." So, we ned to set <code>conf/{all,br0}/arp_ignore</code> to 0. We do this in <code>/etc/sysctl.conf</code>:</p>

<pre><code>--- etc.orig/sysctl.conf        2007-11-24 08:30:22.000000000 -0700
+++ etc/sysctl.conf     2007-11-24 08:30:29.000000000 -0700
@@ -1,6 +1,7 @@
 kernel.panic=3
 net.ipv4.conf.default.arp_ignore=1
-net.ipv4.conf.all.arp_ignore=1
+net.ipv4.conf.all.arp_ignore=0
+net.ipv4.conf.br0.arp_ignore=0
 net.ipv4.ip_forward=1
 net.ipv4.icmp_echo_ignore_broadcasts=1
 net.ipv4.icmp_ignore_bogus_error_responses=1
</code></pre>

<p>There, now (after reboot) the right side of buffalo can ping .109 (don't forget to clear the ARP cache of the host you're testing from), and therefore use .109 as a default route. Everything works great, with one exception. <em>The right side of buffalo cannot ping the cisco.</em> If that bothers you, you can add a static route to the hosts on the right side, like this:</p>

<pre><code>ip route add 216.31.27.105 via 216.31.27.109
</code></pre>

<p>But in practice I don't bother. As long as you remember that you won't be able to and don't try to verify routing by pinging the cisco (pick an external IP address instead), you're fine. I can always ssh to buffalo and then have full access to cisco, or just use the serial connection from falcon.</p>

<p>Ok, so that's how I have one VLAN span two broadcast segments. That's not the only thing I do differently, though.</p>

<p>I disable DHCP on buffalo, because falcon is serving DHCP already. But I don't want to disable dnsmasq altogether because the dns bit is still useful, so I edit <code>/etc/dnsmasq.conf</code> and comment out <code>dhcp-authoritative</code>.</p>

<p>I also add <a href="http://hans.fugal.net/src/openwrt_qos.sh">this <acronym title="Quality of Service">QoS</acronym> script</a> as <code>/etc/init.d/S42qos</code>.It is the excellent <a href="http://lartc.org/wondershaper/">Wondershaper</a> modified for the limitations of the OpenWRT environment. See the comments at the top of the file for instructions. With this QoS setup I don't need to throttle my bittorrent downloads or uploads, but am still able to make clear VOIP calls.</p>

<p>I don't like the default firewall (it's no good for a server behind it), and I find modifying its config is annoying, so I generate a fresh config using <a href="http://ferm.foo-projects.org/">ferm</a> and copy it over to buffalo as <code>/etc/firewall.user</code>.</p>

<p>Everything else that I have changed is fairly standard and doesn't need special description.</p>
