---
layout: post
status: publish
published: true
title: ACPI and gcc
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 50
wordpress_url: urn:uuid:3cdc4e10-d889-4d10-a006-0a09ed5add21
date: '2004-09-11 13:23:20.000000000 -07:00'
tags:
- linux
comments: []
---
<p>I fussed and fussed with this Compaq Evo N150 laptop and ACPI. ACPI utterly
failed to report any useful information about the battery or anything else. No
matter what, my laptop was running at 71&deg;C, which was ridiculous.</p>

<p>I tried fixing the DSDT. I tried different versions of the kernel and different
versions of the ACPI tools. Nothing helped in the least.</p>

<p>Finally, I noticed that things seemed to work properly in Knoppix 3.4. So I
began whittling away at the differences between Knoppix and what I was doing. I
found the source for the knoppix kernel in <code>/usr/src</code>, and the knoppix README
said that knoppix used vanilla stable kernels. I compiled a
kernel with the knoppix config, which also did not work. I racked my brain and
finally realized that the only difference between knoppix and my kernel that
there could possibly be might be the compiler. Knoppix' patch did change gcc to
gcc-2.95. So I made that change in my makefiles, and lo and behold it worked.
So ACPI code has problems with gcc3.</p>

<p>The moral of the story is to compile the kernel with 2.95.x where x &ge; 3, until
the kernel documentation (<code>Documentation/Changes</code>) says it's time to use gcc3.</p>
