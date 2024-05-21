---
layout: post
status: publish
published: true
title: OpenVPN for LARTC Readers
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 906
wordpress_url: urn:uuid:07167440-c0b0-4172-a055-d5c2cf4f4c7f
date: '2007-11-23 22:18:00.000000000 -08:00'
tags:
- linux
- lartc
- openvpn
- iproute2
comments: []
---
<p>I love <a href="http://openvpn.net/">OpenVPN</a>, but man what a <a href="http://openvpn.net/man.html">man page</a>. I've always been annoyed that I have to go digging through the manpage to figure out which options I need and what parameters they take, just to do stuff I already know how to do with <a href="http://www.linux-foundation.org/en/Net:Iproute2">iproute2</a>, no doubt familiar to you all from your dutiful study of the <a href="http://lartc.org/">LARTC</a>. Right? <em>Right?!</em></p>

<p>Finally I got fed up with it. I took a step back and looked at the big picture. There's 3 big pieces to this puzzle. First is <a href="http://vtun.sourceforge.net/tun/">tun/tap</a>, which allows a userspace program to read and write IP or ethernet frames to a virtual network device. One could set up a virtual unprivate network using tun/tap. OpenVPN sets up a virtual <em>private</em> network, by adding all the authentication and encryption stuff. The third piece of the puzzle is the piece that's always there whenever you have any kind of network device, virtual or not. That's configuring the device and setting up the routing. OpenVPN has a plethora of options for all this, but IMHO it's better done with the proper tools, in good UNIX style.</p>

<p>So I changed up my OpenVPN server config to look like this:</p>

<pre><code># tap because we act like a switch
dev tap

# mode server and tls-server to allow us to have many tls clients
mode server
tls-server

# certificate stuff
ca falcon-cacert.pem
cert falcon-cert.pem
key falcon-key.pem
dh dh2048.pem

# I don't like openvpn's --ifconfig and --route family of options for my
# server, so I do it with a script instead
up "/etc/openvpn/falcon.up"

# allow clients to find other clients and their subnets with this pushed
# route
push "route-gateway 172.17.0.3"
push "route 172.17.0.0 255.255.0.0"
client-config-dir clients

# eventually it would be nice to use a real dhcp server instead of this
ifconfig-pool 172.17.0.200 172.17.0.250 255.255.255.0

# options
keepalive 10 60
comp-lzo
learn-address "echo $*"
status /var/log/openvpn.status 60
</code></pre>

<p>Let's walk through it. I use <code>dev tap</code> because I've never had occasion to notice the overhead and it makes wrapping your head around the routing <em>a lot</em> easier. Basically (along with a couple of bits later), the server acts as a switch into which all the clients plug. <code>mode server</code> and <code>tls-server</code> denote server mode (with public key authentication), instead of peer-to-peer (one-to-one) mode. We don't use <code>server-bridge</code> because that sets some options I want to take care of myself. The cert stuff is nothing new. </p>

<p>The next line is the important bit. We use an up script to do the equivalent of OpenVPN's <code>ifconfig</code> and <code>route</code> commands. Here is where the added flexibility and tool familiarity comes into play. Here's my up script:</p>

<pre><code>#!/bin/sh

ip addr add 172.17.0.3/24 dev $dev
ip link set $dev up
ip link set $dev mtu $tun_mtu

for i in 64 77 79 82 84; do
    ip route add 172.17.$i.0/24 via 172.17.0.$i
done
</code></pre>

<p>When this script is run, <code>$dev</code> is <code>tap0</code>. I add the address and set the link up and set the mtu for the link. This is the equivalent of the OpenVPN <code>ifconfig 172.17.0.3 255.255.255.0</code> which is implied by <code>server-bridge</code> with the appropriate options. The next bit is the equivalent of several <code>route</code> options in OpenVPN. Note how I stay <acronym title="Don't Repeat Yourself">DRY</acronym> while adding 5 routes. If I was doing something more fancy, this script would allow me to do it in the natural way using the appropriate tools for the job.</p>

<p>Back to the OpenVPN config. I'm using push instead of putting the burden on future me or whoever is going to set up new clients down the road. In this case <code>route</code> and <code>ifconfig-push</code> (in the client configuration file) are the right tools for the job, and we're glad they're there. As an aside, notice the routes I'm setting up. The <code>route-gateway 172.17.0.3</code> tells them where the "switch" is, and the <code>route 172.17.0.0 255.255.0.0</code> tells them how to find other subnets. A quick example: ungol (172.17.0.64) and caradhras (172.17.0.82) to falcon (172.17.0.3). ungol's LAN subnet is 172.17.64.0/24. caradhras' LAN subnet is 172.17.82.0/24. If 172.17.64.x pings 172.17.82.x, these very important routes come into play. Otherwise, you'd only be able to reach falcon from either subnet. Naturally, the subnets need the correct routing too (ungol and caradhras are probably the default route for those subnets anyway). This is roughly the same thing that happens when you do <code>server-bridge</code> and <code>client-to-client</code>, but not precisely. The reverse routes (in the up script) are needed in either case. Incidentally, you could put <code>client-to-client</code> here too, which would keep the packets from leaving OpenVPN into the kernel stack halfway through their journey. I'm not sure how much overhead that is, but in the interest of minimalism (i.e. "because I can") I left it out.</p>

<p>The <code>ifconfig-pool</code> bit is playing at being a DHCP server. I'm even less happy about OpenVPN playing DHCP server than I am about <code>ifconfig</code> and <code>route</code>. I <em>think</em> configuring my DHCP server on falcon to serve up addresses and options instead of OpenVPN is doable, but there may be some timing issues and I still need to figure out the best way to trigger the DHCP behavior on the client. I just haven't tackled it yet. At least, not this time around. I did try to do this once upon a time using tun instead of tap, and it was mostly a crash and burn. But IIRC that was primarily due to the nature of tun.</p>

<p>The rest is just some standardish options.</p>

<p>So, I can hear you now, "you lunatic, look how much more work that was than just using the OpenVPN options". It may look that way, but in the long run it is not. I know what that up script is doing, at a glance. I know now. I know 3 months from now. I know a year from now. Reading OpenVPN options is like reading a second language. It takes effort and I just don't do it often enough, compared to the iproute2 version. I can remember what an up script does, and I can form a mental model of the network topology from that up script a lot easier than I can from the equivalent OpenVPN config, and that will save me time and frustration down the road, and it is definitely worth it.</p>

<p>As a bonus, I actually understand exactly where OpenVPN fits into the picture, and by putting it in its place I have expanded my understanding of the situation and opened the door to more advanced techniques down the road, should I find that I need them. Even if you take the road more traveled by, hopefully your mind will also have been expanded by reading this post. Happy VPNing!</p>
