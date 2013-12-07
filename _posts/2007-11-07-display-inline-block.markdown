---
layout: post
status: publish
published: true
title: 'display: inline-block'
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 897
wordpress_url: urn:uuid:a0fa21eb-d01b-47ff-998c-f751349efdac
date: 2007-11-07 08:10:00.000000000 -08:00
tags:
- safari
- firefox
- css
- html
- ie
comments:
- id: 1640
  author: Jacob Fugal
  author_email: ''
  author_url: ''
  date: '2007-11-07 12:04:16 -0800'
  date_gmt: ''
  content: <p>Man, I hadn't been exposed to inline-block before. I wants it!</p>
---
<p>I'm not an HTML/CSS guru, but I do know my way around and I do try to use
"semantic HTML" and CSS for styling wherever possible. I hate tables for
layout, if for no other reason than they're a big mess and hard to read, and I
do all my HTML by hand (or generated programmatically, e.g. by
<a href="http://daringfireball.net/projects/markdown/">Markdown</a>,
<a href="http://code.whytheluckystiff.net/markaby/">Markaby</a>, or
<a href="http://haml.hamptoncatlin.com/">Haml</a>).</p>

<p>So I'm a little bit surprised that even lil' ol' dabbler me has more than once
wished to put blocks together in an inline-like flow, e.g. for a photo gallery
or other dynamic grid-based layout, and yet the big guys are content to fall
back on tables. Maybe I can afford to be more puritanical as a hobbyist.</p>

<p>I dug into the issue once again, determined to finally grok the CSS box model
and view model once and for all. I don't know if I got that far, but I do
understand enough about <code>display: block</code> and  <code>display: inline</code> to see why it
doesn't work the way I was hoping it would work. It boils down to a block
element will seek the left edge of its parent.</p>

<p>But, there *is* a way to do precisely what I want to do in CSS 2.1. It's called <code>display: inline-block</code>, and it says to layout block elements in the inline flow. If you're still lost about what I'm driving at, there's a nice live demo and screenshot of <code>display: inline-block</code> at <a href="http://www.quirksmode.org/css/display.html#inlineblock">quirksmode.org</a>. Alas, IE and Gecko (Firefox, Mozilla, Camino, etc.) <a href="http://www.quirksmode.org/css/display.html#t03">don't support this display mode</a>. But in browsers that do (e.g. KHTML-based browsers like Konq and Safari), it's a thing of beauty.</p>

<p>So we need a workaround for Firefox and IE. You could revert to tables if you detect those browsers, but I like to keep the HTML unchanged. You could use <code>float: left</code>, and that works very well unless your blocks are different heights. So you can force your blocks to be the same height, and possibly use <code>overflow: auto</code> to give scrollbars as needed (or hide the overflow or let it just overflow or whatever).</p>

<p>So here's a little example. The blue blocks use <code>display: inline-block</code> and the green blocks use <code>float: left</code>.</p>

<p><style type="text/css">
.inlineblock {display:inline-block; border: solid blue; width:150px;margin:5px;}
.floatleft {float:left; border: solid green; width:150px;margin:5px;}
</style></p>

<div class="inlineblock">Lorem<br/>ipsum</div>

<div class="inlineblock">dolor</div>

<div class="inlineblock">sit</div>

<div class="inlineblock">amet</div>

<div class="inlineblock">The</div>

<div class="inlineblock">quick</div>

<div class="inlineblock">brown</div>

<div class="inlineblock">fox</div>

<div></div>

<div class="floatleft">Lorem<br/>ipsum</div>

<div class="floatleft">dolor</div>

<div class="floatleft">sit</div>

<div class="floatleft">amet</div>

<div class="floatleft">The</div>

<div class="floatleft">quick</div>

<div class="floatleft">brown</div>

<div class="floatleft">fox</div>

<p style="clear:left">
Do play around with it by resizing your browser and dusting off that Konquerer or Safari browser to see how the blue blocks look when rendered correctly.</p>

<p>I think it's a crying shame that firefox doesn't render this properly. Maybe the complacent table-hugging masses haven't made enough noise. Let's make some noise.</p>

<p>While I'm on the subject, I highly recommend <a href="http://rafael.adm.br/css_browser_selector/"><code>css_browser_selector.js</code></a> method of doing browser-specific CSS.</p>
