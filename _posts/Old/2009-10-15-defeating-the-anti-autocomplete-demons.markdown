---
layout: post
status: publish
published: true
title: Defeating the Anti-Autocomplete Demons
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1196
wordpress_url: http://hans.fugal.net/blog/?p=1196
date: '2009-10-15 05:18:32.000000000 -07:00'
tags:
- javascript
- firefox
- greasemonkey
- autocomplete
comments: []
---
There are demons out there. They have sent their evil henchbugs to make my life difficult. The Santa Clara library login page for some unfathomable reason doesn't trigger Firefox's autocomplete. No, the HTML form doesn't specify "autocomplete=off". As far as I can tell, it's just that Firefox doesn't seem to think that my library barcode is worth remembering. Which is a real bummer because it's impossible to remember and about as sensitive as the callus on my big toe.

So I got jiggy with <a href="https://addons.mozilla.org/en-US/firefox/addon/748">GreaseMonkey</a> and made my own autofill script:

<code>// ==UserScript==
// @name           Santa Clara Library Autocomplete
// @namespace      http://hans.fugal.net/
// @include        https://sccl.santaclaraca.gov/patroninfo*
// ==/UserScript==
name = document.getElementsByName('name')[0];
code = document.getElementsByName('code')[0];
name.value = 'Fred Flintstone';
code.value = 'Your impossible-to-remember-barcode goes here';</code>
