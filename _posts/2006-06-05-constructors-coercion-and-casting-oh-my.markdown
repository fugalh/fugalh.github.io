---
layout: post
status: publish
published: true
title: Constructors, coercion and casting, oh my!
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 337
wordpress_url: urn:uuid:def97d37-9eaa-4952-85d5-a5da3e019513
date: 2006-06-05 13:08:18.000000000 -07:00
tags:
- C
- src
- cast
comments: []
---
<p>This little bit of C++ trivia I may have known once but had forgotten. If you
have the appropriate constructor, the compiler will happily coerce for you:</p>

<pre><code>class Foo
{
public:
Foo(int);
int i;
};

int bar(Foo f)
{
return f.i;
}

int main(void)
{
return bar(42);
}
</code></pre>

<p>You can also explicitly cast, which is useful when you are feeling explicit, or
want to cast to a subclass for polymorphic reasons.</p>
