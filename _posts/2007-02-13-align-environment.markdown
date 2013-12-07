---
layout: post
status: publish
published: true
title: align Environment
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 787
wordpress_url: urn:uuid:add14b1a-6016-4199-8da1-63c8d3837fc0
date: '2007-02-13 19:53:00.000000000 -08:00'
tags:
- cs
- math
- latex
- align
- proof
- equation
comments: []
---
<p>How I managed to get along for so long without knowing this I don't know.
The align environment in LaTeX is very nice for typesetting a series of          equations, e.g. in a proof. Here is an example:</p>

<pre><code>\begin{align*}
P(A)\text{ and }P(\overline A\cap B)&amp;\text{ are mutually exclusive.}\
P(\overline A\cap B)+P(A\cap B) &amp;= P(B)\
P(A\cup(\overline A\cap B)) &amp;= P(A)+P(\overline A\cap B) &amp;\because           \text{Third axiom of probability}\
P(A)+P(\overline A\cap B) &amp;\le 1 &amp;\because \text{First axiom of probability}\
P(A)+P(\overline A\cap B)+P(A\cap B)-1 &amp;\le P(A\cap B)\
P(A)+P(B)-1 &amp;\le P(A\cap B)
\end{align*}
</code></pre>

<p>That will typeset a series of equations aligned by the &amp;s.</p>
