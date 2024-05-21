---
layout: post
status: publish
published: true
title: Printing Hipster
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 919
wordpress_url: urn:uuid:d1cdeded-bf16-470e-81c7-c8bf1b34773f
date: '2008-01-29 13:29:16.000000000 -08:00'
tags:
- pda
- hipster
- index
- card
- multivalent
comments:
- id: 1677
  author: Mike
  author_email: ''
  author_url: ''
  date: '2008-01-30 08:56:48 -0800'
  date_gmt: ''
  content: <p>Hans - great posts as always, thanks for your ideas.  hipmod has been
    a hit here in the UK with my daughter!  So what make/model of guillotine do you
    recommend then, as scissors aren't cutting it?!</p>
- id: 1678
  author: Hans
  author_email: ''
  author_url: ''
  date: '2008-01-30 08:58:43 -0800'
  date_gmt: ''
  content: '<p>The one at the office. ;-) Yeah, I have access to one at school so
    I wouldn''t know. This guy has some good thoughts on the subject though: <a href="http://fullcontactgeek.com/page.php?2"
    rel="nofollow">http://fullcontactgeek.com/page.php?2</a></p>'
---
<p>So the <a href="http://hans.fugal.net/blog/2008/01/26/hipmod.html">hipmod</a> is too small for you? You want to use the regular-size hipster? But by golly your printer refuses to play nicely with index cards?</p>

<p>Here's a solution. Use <a href="http://multivalent.sourceforge.net/">Multivalent</a> to 4-up index cards onto regular paper, and cut them with a guillotine. You can use cardstock for the full effect.</p>

<p>The trick is in printing the cards at the original size, and optimizing for trimming. Something like this:</p>

<pre><code>./multivalent impose -nup 4 -sep 1 -paper 6x10in core.pdf
</code></pre>

<p>This gives you a 6x10-inch PDF (<code>core-up.pdf</code>). Now you need to print it without scaling it to letter size. That should be straightforward to figure out in your environment. Then take it to the guillotine and make your 6 cuts and pat yourself on the back. If you're really clever and your printer has &lt;= ⅛-inch margins you can get it down to 4 cuts.</p>

<p>If you want to make a lot of one card, you can do something like this:</p>

<pre><code>./multivalent impose -nup 4 -page 46,46,46,46 -sep 1 -paper 6x10in core.pdf
</code></pre>

<p>You can even get clever and take advantage of duplex printing if your printer supports it. Sky's the limit!</p>
