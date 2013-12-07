---
layout: post
status: publish
published: true
title: VMWare Server on Hardy
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 993
wordpress_url: urn:uuid:8d35064f-3d05-459a-8d47-14ef2dfa411e
date: 2008-07-27 15:54:46.000000000 -07:00
tags:
- linux
- kernel
- vmware
- ubuntu
- hardy
- heron
comments:
- id: 1768
  author: Leon Matthews
  author_email: ''
  author_url: http://lost.co.nz/
  date: '2008-07-27 22:10:22 -0700'
  date_gmt: ''
  content: <p>I suggest you give VirtualBox a go.  Very impressive performance, even
    on systems without hardware virtualisation support (like my AMD64 x2 3800 workstation)
    and recently (thanks to Sun) a friendly license...</p>
- id: 1769
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-07-28 09:55:55 -0700'
  date_gmt: ''
  content: <p>I actually explored this avenue partially. I just needed to get some
    Windows access, I didn't care how. I got VirtualBox installed and began the complicated
    process of converting a vmware image into a virtualbox image, when it became apparent
    that fixing vmware would be simpler. (And I already knew a fresh windows install
    would be more involved.) So trying out VirtualBox will have to wait.</p>
- id: 1770
  author: Mike Wilson
  author_email: mrw2006@googlemail.com
  author_url: http://whisperingwind.co.uk
  date: '2008-07-29 11:39:48 -0700'
  date_gmt: ''
  content: <p>Good tip -- thanks. I was stuck trying to install VMWare after upgrading
    to Hardy. Didn't have time to frig around, glad I found your page. Thanks, Mike
    Wilson</p>
- id: 1771
  author: boblemur
  author_email: ''
  author_url: ''
  date: '2008-08-13 00:00:36 -0700'
  date_gmt: ''
  content: |-
    <p>hey all, the copy is not a good solution because it means if the original gets updated then the updates wont be reflected in the copied one... also you are waseing space...</p>

    <p>firstmake an empty folder for the lib to go into:</p>

    <p>sudo mkdir /usr/lib/vmware/lib/libgcc_s.so.1</p>

    <p>then make a symbolic link from the real lib folder to the one vmware is looking for</p>

    <p>sudo ln -s /lib/libgcc<em>s.so.1 /usr/lib/vmware/lib/libgcc</em>s.so.1/</p>
- id: 1869
  author: Anthony
  author_email: honstain@gmail.com
  author_url: ''
  date: '2009-02-24 03:33:57 -0800'
  date_gmt: '2009-02-24 03:33:57 -0800'
  content: Amazing! The guide worked perfect!
---
<p>I had a heck of a time getting VMWare Server running on Ubuntu 8.04 (Hardy Heron). The problem is that the <code>vmmon</code> and <code>vmnet</code> modules fail to build against kernel 2.6.24. A little googling quickly reveals that you want the <a href="http://groups.google.com/group/vmkernelnewbies/files">any-any-update patch</a>, but that didn't work for me either. To be specific, <code>vmware-any-any-update117c.tar.gz</code> did not work. It turns out <a href="http://vmkernelnewbies.googlegroups.com/web/vmware-any-any-update-116.tgz?gda=7K82Ck4AAAB2kw0-pu_6aCQrwDif3FMaRxYRPEwLJKRUj3XRnFlkyWG1qiJ7UbTIup-M2XPURDSGXdvV5n_wsDUmPsx7kjwlI6ntQuOhZp5frm-yOmhQvw"><code>vmware-any-any-update-116.tgz</code></a> works great. Maybe 117 is for the 2.6.25 kernel or something.</p>

<p>So, you do the vmware installation except for the <code>vmware-config.pl</code> step. Then you download and extract the above tarball and run <code>runme.pl</code>. Simple enough.</p>

<p>But when you try to run it, you get errors like this:</p>

<pre><code>/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_3.4' not found (required by /usr/lib/libcairo.so.2)
/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_4.2.0' not found (required by /usr/lib/libstdc++.so.6)
/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_3.4' not found (required by /usr/lib/libcairo.so.2)
/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_4.2.0' not found (required by /usr/lib/libstdc++.so.6)
/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_3.4' not found (required by /usr/lib/libcairo.so.2)
/usr/lib/vmware/bin/vmware: /usr/lib/vmware/lib/libgcc_s.so.1/libgcc_s.so.1: version `GCC_4.2.0' not found (required by /usr/lib/libstdc++.so.6)
</code></pre>

<p>I'm not sure what the <em>right</em> way to fix this is, but <a href="http://my.opera.com/scrface/blog/2008/06/29/installing-vmware-server-in-hardy-heron">this way</a> works for me.</p>

<pre><code>sudo cp /lib/libgcc_s.so.1 /usr/lib/vmware/lib/libgcc_s.so.1/
</code></pre>
