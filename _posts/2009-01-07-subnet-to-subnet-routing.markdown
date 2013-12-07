---
layout: post
status: publish
published: true
title: Subnet-to-Subnet Routing
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1033
wordpress_url: urn:uuid:fd3f261a-eb44-4e19-8e8e-c5343cadc9fc
date: 2009-01-07 10:21:00.000000000 -08:00
tags:
- linux
- openvpn
- vpn
- tap
- tun
- route
- bridge
- switch
- hub
- ethernet
- tcpdump
- icmp
- arp
comments:
- id: 1796
  author: Hans
  author_email: ''
  author_url: ''
  date: '2009-01-08 09:35:09 -0800'
  date_gmt: ''
  content: '<p>Von asked a good question: why would I set up routes without a gateway?
    I wasn''t doing explicit routes without a gateway, I was originally giving the
    clients the address 172.17.0.x/16, and thinking that they would be able to figure
    out the routing. This creates a route to 172.17.0.0/16 via dev tap0.</p>'
---
<p>This is a note to myself, since I always seem to get this wrong and spend an hour or two racking my brain over it, and yet it's so simple.</p>

<p>Consider the following network:</p>

<pre><code>172.17.77.0/24 -- A --+-- B -- 172.17.82.0/24
                      |

                      S

A: 172.17.77.1/24 and 172.17.0.77/24
B: 172.17.82.1/24 and 172.17.0.82/24
S: 172.17.0.1/24
</code></pre>

<p>It is instructive to watch a tcpdump on A, S, and B while you ping between these three hosts. In particular, S sees nothing when A and B ping eachother. Well, not nothing—S will see the arp requests—but if you were running <code>tcpdump icmp</code> you wouldn't see anything. Now, if A is the gateway for its subnet and B is the gateway for its subnet, and you put a route for 172.17.0.0/16 via S on both A and B, the two subnets can find each other. But what if you instead put a route for 172.17.0.0/16 via the interface alone, and try to leave S out of it? A will not respond to ARP requests for 172.17.77.42, and so packets from B's subnet for A's subnet will fall off the edge of the network at B.</p>

<p>I hope that makes sense. It's rather simple when you look at it that way and not much to sing about. But when I make this little modification my brain always seems to go on vacation:</p>

<pre><code>172.17.77.0/24 -- A      B -- 172.17.82.0/24
                   \    /
                    tap0
                     |
                     S
</code></pre>

<p>Now A, B, and S are connected by OpenVPN using TAP. TAP is like a virtual switch (Layer 2), so in reality it's <em>the exact same setup</em>. But for some reason whenever I set this up I tend to think that a route on A and B for 172.17.0.0/16 via dev tap0 will work. And so it does, when pinging just A and B. Then when I finally get around to hooking up their subnets, they can't see the other side of the VPN and I get confused. Then I fire up umpteen tcpdumps and having forgot to look for ARP traffic I get utterly flabbergasted. My mind thinks that since S is the VPN server that I should see ping traffic from A to B (or A's subnet to B's subnet) on S, if it's making it through the VPN. Then I assume that OpenVPN is doing something funky. At this point I get confused by the <code>client-to-client</code> option, and things go downhill fast.</p>

<p>So lets set things straight once and for all. OpenVPN's <code>client-to-client</code> option, when used with TAP, makes the VPN behave like a true switch. When it is set, A can see B's ARPs, and vice versa. When it is not, they can't. Think of it as S having one NIC for each client and they're all bridged together on tap0, or not, depending on the setting of <code>client-to-client</code>.</p>

<p>If you set routes for 172.17.0.0/24 via 172.17.0.1 then A can reach B anyway, but S will helpfully send ICMP redirects which won't work if followed. I suppose you could turn off this "helpfulness", but if you want to get from A to B just turn on the aptly-named <code>client-to-client</code> option. </p>

<p>The next important thing is to remember that when <code>client-to-client</code> is set and you're using TAP, the VPN behaves like a true switch. Packets direct from A to B will not show up on tap0 as far as external programs like tcpdump are concerned. That also goes for packets from A's subnet to B's subnet. Of course, they are still running through the VPN, and so S is playing the middleman as far as bandwidth, firewall, and encryption go. But you won't see it with tcpdump. (It makes me wonder if tap0 is behaving like a switch in that traffic from A to S never travels to C at all—I think this is probably the case.) Switch, not hub.</p>

<p>Finally, the important thing to realize when doing TAP is that the network looks like this:</p>

<pre><code>A -- + -- B
     |

     S
</code></pre>

<p><em>not</em> like this:</p>

<pre><code>A -- S -- B
</code></pre>

<p>And the final take-home lesson is, use <code>tcpdump icmp or arp</code> to avoid confusion and hair loss.</p>

<p>There. hopefully that straightens me out, if nobody else.</p>
