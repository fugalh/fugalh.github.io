---
layout: post
status: publish
published: true
title: kernel-package, you've come a long way baby
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 813
wordpress_url: urn:uuid:e3fb6f07-f8f3-4676-b766-253dd82a3733
date: 2007-03-02 16:54:00.000000000 -08:00
tags:
- linux
- kernel
- debian
comments: []
---
<p>Back in the day, I cared about having my kernel as a Debian package. I used kernel-package, and I was happy. Then I started wanting to compile vanilla kernels and eventually the overhead just got to me and I stopped using it. I was not using kernel-package, and I was happy.</p>

<p>Recently, I revisited kernel-package for some reason I can't now remember. Wow,
it has come a long way. Now it works with vanilla kernels, no fuss. Now it
builds initrd images with a single command line option, no fuss. Now it is even
easier than just building the kernel by hand (because I don't have to
reconfigure the kernel from the stock kernel after <code>make oldconfig</code> due to the
lack of initrd (no, I will never even try doing an initrd by hand)).</p>

<p>Here's all you have to do:</p>

<pre><code># download kernel source
cd linux
make oldconfig
# make menuconfig
fakeroot make-kpkg --initrd kernel-image kernel-headers
sudo dpkg -i ../linux*deb&lt;tab&gt;
</code></pre>
