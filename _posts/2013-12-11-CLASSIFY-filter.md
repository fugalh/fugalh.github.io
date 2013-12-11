---
layout: post
title: "You can't chain iptables CLASSIFY and tc filter in HTB"
---
I wanted to chain an iptables CLASSIFY rule with a tc filter rule. You can't, but you can use MARK in combination with a tc filter at the root to achieve the same effect.

```
qdisc 1:
    class 1:1
        class 1:2
        class 1:3
    class 1:4
```

I wanted to install a filter to match a subnet on class 1:1, so anything to that subnet would go to class 1:2, but only if we already got to class 1:1. I set up an iptables rule to `-j CLASSIFY --set-class 1:1` and a tc filter with `parent 1:1`. It didn't work. The answer as to why is hidden in [this thread](http://mailman.ds9a.nl/pipermail/lartc/2006q2/018965.html). (I'm not sure if that limitation could be fixed in the HTB code easily or not.) In short, CLASSIFY can only target leaf classes in HTB.

Instead, I'm using `-j MARK --set-mark $mark` with iptables, and adding a tc filter on the root that matches that mark. So I'm doing the same thing, indirectly. Here's a sample script with all the details:

```bash
dev=eth0
subnet=10.4.172.85/24
dport=5001
mark=42

tc qdisc add dev $dev handle 1: root htb

tc class add dev $dev classid 1:1 parent 1: htb rate 1gbit
tc class add dev $dev classid 1:2 parent 1:1 htb rate 1mbit
tc class add dev $dev classid 1:3 parent 1:1 htb rate 1kbit
tc class add dev $dev classid 1:4 parent 1: htb rate 10gbit

tc filter add dev $dev prio 1 protocol ip handle $mark fw flowid 1:1
tc filter add dev $dev prio 1 protocol ip parent 1:1 u32 match ip dst $subnet flowid 1:2

iptables -t mangle -A POSTROUTING -p tcp --dport $dport -j MARK --set-mark $mark
```

You can test with iperf to a host inside and outside of the given subnet. (Whose default destination port is 5001)

The example is of course contrived and simplified. What I'm actually doing is maintaining ipsets of hosts, using iptables to match the ipset and set the appropriate mark, and then subdividing the classes further by subnet.
