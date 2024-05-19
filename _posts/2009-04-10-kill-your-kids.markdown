---
layout: post
status: publish
published: true
title: Kill your Kids
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1132
wordpress_url: http://hans.fugal.net/blog/?p=1132
date: '2009-04-10 17:57:28.000000000 -07:00'
tags:
- cs
- linux
- bash
- shell
- child
- kid
- propagate
- signal
- sigint
- interrupt
- ctrl-c
- kill
- exit
comments:
- id: 2056
  author: Chris
  author_email: chris@roaima.co.uk
  author_url: ''
  date: '2009-07-06 13:00:17 -0700'
  date_gmt: '2009-07-06 13:00:17 -0700'
  content: "This is another situation where \" isn't the same as '\r\n\r\nIf you define
    your trap with \"...\" then the variables will be evaluated during the definition.
    If, instead, you use '...' then the variables (i.e. your list of children) will
    be evaluated only when the trap fires.\r\n\r\nThis snippet shows the trivial case.
    Use kill to send either 1, 2, or 15 to show the point.\r\n\r\nS=0\r\ntrap 'echo
    trap 1 with S=$S - delayed' 1\r\ntrap \"echo trap 2 with S=$S - immediate\" 2\r\n\r\nS=1\r\nwhile
    :\r\ndo\r\n  echo pid \$$ waiting for signal 1, 2, or 15\r\n  sleep 2\r\n  S=$((S+1))\r\ndone"
---
Not literally, of course. This is programming talk, those of you who aren't programmers can let your eyes glaze over.

I wanted a script to start a bunch of little servers, then wait around for them to finish or when the user interrupts with Ctrl-C, clean up the servers instead of orphaning them.  I wanted to propagate the SIGINT to the child processes. I wanted to kill the kids.

The simple way, if you just want to make sure the kids are killed and you don't care how:
<code>
sleep 300 &
# etc.
trap "kill $(echo $(jobs -p)) 2>/dev/null" EXIT
wait</code>

If you only want to trap SIGINT and want to make sure you send SIGINT (not SIGKILL) to the children, then you want to do something like:
<code>
trap "kill -INT $(echo $(jobs -p)) 2>/dev/null" INT
wait</code>

<strong>Update</strong>: I was asked by <a href="http://www.buscaluz.org/">a shell scripting guru</a> why I needed to do <code>$(echo $(jobs -p))</code> and not just <code>$(jobs -p)</code>. I intended to cover that but forgot. The reason is that <code>$(jobs -p)</code> has newlines and while that's not usually a problem it is in a trap statement, because it's evaluated at creation time not at run time. It also means that processes created after you create the trap wouldn't be killed. Then, he suggested a function instead. Pure brilliance. Where does he come up with these things? Here's the improved version:

<code>function killkids() { kill $(jobs -p); }
trap "killkids" EXIT</code>

You can still redirect stderr if you want to, but the reason I was directing stderr was because some of the kids may have already died (early evaluation remember) and then kill would needlessly complain. This way, it kills all the kids that are still alive, none more none less.
