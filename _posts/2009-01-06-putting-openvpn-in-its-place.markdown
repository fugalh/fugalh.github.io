---
layout: post
status: publish
published: true
title: Putting OpenVPN in its place
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1032
wordpress_url: urn:uuid:594b617f-ea1e-4e85-a9f1-fd1249a8db00
date: 2009-01-06 08:26:00.000000000 -08:00
tags:
- linux
- mac
- osx
- dynamic
- openvpn
- iproute2
- ip
- dns
- dhcp
- vpn
- ddns
- tap
- tun
- pseudodhcp
comments:
- id: 1795
  author: Doran Barton
  author_email: fozz@iodynamics.com
  author_url: http://www.fozzilinymoo.org/
  date: '2009-01-06 23:22:08 -0800'
  date_gmt: ''
  content: <p>Very cool. Thanks Hans.</p>
- id: 2158
  author: Ivars
  author_email: ivars.strazdins@gmail.com
  author_url: ''
  date: '2009-12-22 17:15:56 -0800'
  date_gmt: '2009-12-22 17:15:56 -0800'
  content: "really helpful for Linux dhcp.\r\nit is funny with openvpn that win and
    os x clients now work out of box, but linux needs special treatment ;)"
- id: 2164
  author: Casey
  author_email: pdt_pilot-wedding@yahoo.com
  author_url: ''
  date: '2010-01-30 17:25:55 -0800'
  date_gmt: '2010-01-30 17:25:55 -0800'
  content: "Could you post your entire Interface file? I guess i don't quiet understand
    how to properly incorprate this into mine since my Interface file has the internet
    connection Eth0, the Bridge Device br0, and the internal network eth1 which is
    controlled by a script that openvpn runs\r\nThank You"
- id: 2190
  author: paul
  author_email: nihaopaul@amhe.net
  author_url: http://amhe.net
  date: '2010-02-28 14:28:29 -0800'
  date_gmt: '2010-02-28 14:28:29 -0800'
  content: very cool.. i had almost given up on dhcpd over openvpn.. dont suppose
    you've tested this with IPv6? would be an excellent guide as nothing is out there
    for it.
- id: 2203
  author: ''
  author_email: 23charles@gmail.com
  author_url: http://www.nettek.ch
  date: '2010-03-06 13:03:34 -0800'
  date_gmt: '2010-03-06 13:03:34 -0800'
  content: Does my mac adresse change if I upgrade my computer with some other hardware?
    For example change the graphic card?
- id: 2208
  author: openvpn un DHCP zem linux &laquo; shpokas
  author_email: ''
  author_url: http://shpokas.wordpress.com/2010/03/12/openvpn-un-dhcp-zem-linux/
  date: '2010-03-12 20:21:40 -0800'
  date_gmt: '2010-03-12 20:21:40 -0800'
  content: '[...] Tāpēc tāds geemrojs: [...]'
- id: 2248
  author: '[SOLVED] OpenVPN+dhcpd+ldap'
  author_email: ''
  author_url: http://www.linuxquestions.org/questions/linux-server-73/openvpn-dhcpd-ldap-791287/#post3968150
  date: '2010-05-14 10:21:50 -0700'
  date_gmt: '2010-05-14 10:21:50 -0700'
  content: '[...] in a slightly different solution to this issue. The blog by Hans
    Fugal &quot;putting OpenVPN&quot; (http://hans.fugal.net/blog/2009/01/0...-in-its-place/)
    was VERY helpful in figuring this out.   I finally got it to work by letting Linux
    create the TAP [...]'
- id: 2310
  author: sam
  author_email: jesuslikesbeer@hotmail.com
  author_url: ''
  date: '2010-10-21 10:04:54 -0700'
  date_gmt: '2010-10-21 10:04:54 -0700'
  content: "crickey, that logically is a far easier concept! probably worth mentioning
    that ovpn won't like the server config if persistent ips are enabled...\r\nexcellent
    article"
---
<p><em>Update</em>: I had some errors and oversights in my general config that didn't have any direct bearing on the main message of this post. I have fixed them below and I beg you to pretend they never happened.</p>

<p><a href="http://openvpn.org/">OpenVPN</a> is a fantastic piece of software. No, it's an <em>essential</em> piece of software. A godsend.<br/>
But it has this tendency to try to be all that and a bag of chips.</p>

<p>My primary gripe with OpenVPN over the years has been what I call "psuedo-DHCP". It pretends, poorly, to be a DHCP server. If you have the audacity to prefer a real DHCP server you find very little help and sometimes even resistance from the tools and the community. I once tried to get it working and failed.</p>

<p>This week I was refreshing my OpenVPN setup and reading through the manpage for version 2.1, and saw a few references to people actually using DHCP. Still no explicit documentation, but it gave me hope. So I duly tilted at that windmill.
Now I will show you how to get DHCP working with OpenVPN. What's more, we'll get rid of <code>ifconfig</code> and <code>route</code> options (for the most part). In short, we'll put OpenVPN in its place: as a secure tunnel manager.</p>

<p>The important paradigm shift here is that you aren't required to do <em>anything</em> from withing OpenVPN to configure the interface. You can just bring up the tunnel and your TUN/TAP device will be alive but unconfigured. At that point you could do something like this:</p>

<pre><code>ip link set tap0 up
ip addr add 172.17.0.1/24 dev tap0
</code></pre>

<p>You could do this manually, or in an up script, or whatever. Or you could <em>let your distro do it</em>. Ah, so we can have a <code>tap0</code> stanza in <code>/etc/network/interfaces</code> (Debian-based distros) that will configure <code>tap0</code> when we ask it to. Let's look at a client example:</p>

<pre><code># in /etc/network/interfaces
iface tap0 inet dhcp
    hostname falcon
    # dhclient doesn't pay attention to this, so if you use dhclient (you
    # probably do) see /etc/dhcp3/dhclient.conf
    client falcon

# in the openvpn config
dev tap0
route-delay 10
cd /etc/openvpn
up "up.sh"
down-pre
down "down.sh"
…

# up.sh
#! /bin/bash
ifdown tap0 2&gt;/dev/null
ifup tap0 &amp;

# down.sh
ifdown tap0
</code></pre>

<p>There's some subtlety here, let's talk about it. Note that we're specifying both the DHCP client id and the DHCP hostname—more on that later. We use an external script because of the way OpenVPN's <code>up</code> option works, so that we can background the <code>ifup</code> call. This is important because the tunnel isn't fully up at this point, so your DHCP client won't succeed unless we background it (I tried <code>up-delay</code> to no avail). I have the <code>ifdown</code> bit in there as a safety measure—if for whatever reason Debian thinks the interface is already up it won't start the DHCP client and that would be bad. But hopefully this doesn't happen much thanks to the <code>down</code> option. Finally, the <code>route-delay</code> option gives the DHCP negotiation a chance to finish before any routes are applied (and in my setup there is one important route that I push to clients).</p>

<p>On the server side, we need to set up the DHCP server. ISC DHCP (<code>dhcp3-server</code> on Debian) isn't very intelligent about interfaces that materialize out of nowhere, so we'll need to set up a persistent TAP device. </p>

<pre><code># in /etc/network/interfaces
auto tap0
iface tap0 inet static
    address 172.17.0.1
    netmask 255.255.255.0
    pre-up openvpn --dev tap0 --mktun

# in openvpn config
dev tap0
</code></pre>

<p>Now <code>tap0</code> will be brought up automatically at boot, and will stay up even if you restart OpenVPN (you can bring it up now with <code>ifup tap0</code>). Notice that no <code>ifconfig</code> option is needed in the OpenVPN config. Now you can configure your DHCP server for the subnet:</p>

<pre><code># in dhcpd.conf
subnet 172.17.0.0 netmask 255.255.255.0 {
    # example options for VPN hosts
    option domain-name "vpn.example.com";
    option domain-name-servers 172.17.0.1;
    option netbios-name-servers 172.17.0.1;
    option ntp-servers 172.17.0.1;

    range 172.16.0.100 172.17.0.199;
}

host falcon {
    option dhcp-client-identifier "falcon";
    fixed-address 172.17.0.77;
}
</code></pre>

<p>Observe the <code>dhcp-client-identifier</code> option, and its matching entry in foo's <code>/etc/network/interfaces</code> (or <code>/etc/dhcp3/dhclient.conf</code>). This is important because TAP MAC addresses don't persist—you get a new one every time. dhcpd will use the client identifier to match a host, but alternatively you could spoof a static MAC address in foo's <code>/etc/network/interfaces</code> config. I think the client identifier is cleaner. Even if you don't use static leases, this way dhcpd will know it's the same client and give him the IP address he had before. Of course if you don't need (semi-)static leases you don't need to worry about client identifiers. You'll have some cruft leases but they should expire and disappear.</p>

<p>Unfortunately dhcpd doesn't use the client identifier for dynamic dns updates (one of the big reasons I wanted to use real DHCP in the first place), which is why I specify the <code>hostname</code> option in foo's <code>/etc/network/interfaces</code>. dhclient (as configured on Debian) sends the hostname whether or not you specify it in <code>/etc/network/interfaces</code>.</p>

<p>Other DHCP clients that do honor <code>/etc/network/interfaces</code> are available. See interfaces(5). I'm kind of partial to udhcpc, especially for hand-testing, though I usually end up sticking with dhclient.</p>

<p>Caveats: I haven't been able to get DHCP working with an OS X client. I tried initiating DHCP on the TAP interface with <code>ipconfig set tap0 DHCP</code> but it didn't work and once locked up my machine. So for this situation, or for any other reason you may have, you can still push <code>ifconfig</code> and <code>route</code> options in the client configuration directory entry for that client. </p>

<p>I haven't tried DHCP over OpenVPN on Windows clients yet but I see no reason why it wouldn't work.  </p>

<p>Finally, I tried briefly to do it with a TUN device and though I can think of no obvious reason why it shouldn't work, it didn't. I like TAP better anyway.</p>

<p>Now after all this I can see some of you shaking your heads wondering what the point of all this is. "Surely this is more complicated than <code>ifconfig</code> and <code>route</code> in OpenVPN." Yes, it's more complicated, but it's more powerful. If all you need is pseudo-DHCP, then by all means use pseudo-DHCP. But if you are a sysadmin serving a gaggle of clients you soon find yourself pining for a real DHCP server. Or perhaps you want dynamic dns updates, or proper DHCP option support. (You do realize DHCP options sent by OpenVPN's <code>dhcp-option</code> are not applied on linux unless you do so manually by reading the environment variables in an up script, don't you?) </p>

<p>When you realize OpenVPN can just set up the tunnel and get out of the way, you realize that all your fancy networking knowledge and tools can come into play to create the ultimate VPN tailored exactly to your needs. Plus, I think it snaps things into focus so that things just make more sense in your head.</p>

<p>And now, I present my OpenVPN configs (sanitized) for the server (frodo) and a client (falcon):</p>

<pre><code>## frodo (server)
dev tap0
mode server
tls-server

cd /home/fugalh/vpn
ca cacert.pem
dh dh.pem
cert frodo.pem
key frodo.pem

keepalive 10 60
comp-lzo
client-to-client
# this new option is nifty
passtos

client-config-dir ccd

# See /etc/network/interfaces for interface configuration and routing.
# (reproduced here for our web audience)
# auto tap0
# iface tap0 inet static
#         address 172.17.0.1
#         netmask 255.255.0.0
#         pre-up openvpn --dev tap0 --mktun
#         up ip route add 172.17.64.0/24 via 172.17.0.64
#         up ip route add 172.17.77.0/24 via 172.17.0.77
#         up ip route add 172.17.82.0/24 via 172.17.0.82
#         up ip route add 172.17.83.0/24 via 172.17.0.83
push "route 172.17.0.0 255.255.0.0 172.17.0.1"

#verb 3
mute 2
status /var/log/openvpn.status 60


## falcon (client)
dev tap0
client
remote frodo.fugal.net
nobind

cd /etc/openvpn
ca falcon-cacert.pem
cert falcon-cert.pem
key falcon-key.pem
tls-remote frodo.fugal.net

comp-lzo
passtos

route-delay 10
cd /etc/openvpn
up "up.sh"
# (reproduced here)
# #!/bin/bash
# ifdown tap0 &amp;&gt;/dev/null
# ifup tap0 &amp;

down "down.sh"
# (reproduced here)
# #!/bin/bash
# ifdown tap0

mute 2
#verb 3
</code></pre>

<p>In my setup the 172.17.0.0/24 subnet is for the OpenVPN server and clients, and each client is a gateway to a 172.17.x.0/24 subnet for his LAN. Assuming a static route on the LAN for 172.17.0.0/16 via the OpenVPN client, frodo will route everything so people on one LAN can find people on another. </p>

<p>I also have <a href="http://www.semicomplete.com/articles/dynamic-dns-with-dhcp/">dynamic dns updates</a> for both forward and reverse DNS in my <code>vpn.fugal.net</code> zone.</p>

<p>One thing I haven't set up which is feasible is for the LAN DHCP servers to do ddns to frodo.</p>

<p>OpenVPN is in its place, and our relationship is that much stronger. Good luck with yours!</p>
