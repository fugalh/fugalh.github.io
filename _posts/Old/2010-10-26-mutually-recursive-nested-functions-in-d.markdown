---
layout: post
status: publish
published: true
title: Mutually-recursive Nested Functions in D
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1233
wordpress_url: http://hans.fugal.net/blog/?p=1233
date: '2010-10-26 03:24:41.000000000 -07:00'
tags:
- cs
- d
- anonymous
- language
- function
- delegate
- first-class
comments: []
---
From <a href="http://digitalmars.com/d/2.0/function.html">http://digitalmars.com/d/2.0/function.html</a>:


<blockquote>
Unlike module level declarations, declarations within function scope are processed in order. This means that two nested functions cannot mutually call each other:

<pre><code>void test()
{
    void foo() { bar(); }	// error, bar not defined
    void bar() { foo(); }	// ok
}
</code></pre>

The solution is to use a delegate:

<pre><code>void test()
{
    void delegate() fp;
    void foo() { fp(); }
    void bar() { foo(); }
    fp = &bar;
}
</code></pre>

Future directions: This restriction may be removed.
</blockquote>

You can also do away with the useless name, e.g.
<pre><code>void test()
{
    void delegate() bar;
    void foo() { bar(); }
    bar = delegate void() { foo(); };
}</code></pre>
