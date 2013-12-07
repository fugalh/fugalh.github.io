---
layout: post
status: publish
published: true
title: Pimping Screen
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1090
wordpress_url: http://hans.fugal.net/blog/?p=1090
date: '2009-02-05 23:26:21.000000000 -08:00'
tags: []
comments:
- id: 1905
  author: sc
  author_email: sirshane13@gmail.com
  author_url: http://sphericalcow.wordpress.com
  date: '2009-03-13 12:10:26 -0700'
  date_gmt: '2009-03-13 12:10:26 -0700'
  content: Great tips for screen - I've been putting off going through the man page
    for years to try and figure this stuff out!
- id: 2142
  author: ''
  author_email: ''
  author_url: ''
  date: '2009-10-30 13:20:22 -0700'
  date_gmt: '2009-10-30 13:20:22 -0700'
  content: PIMP YA SCREEN
- id: 2143
  author: KEITH BEAMON
  author_email: sax1step@gmail.com
  author_url: http://FACEBOOK
  date: '2009-10-30 13:21:22 -0700'
  date_gmt: '2009-10-30 13:21:22 -0700'
  content: PIMPYA SCREEN
- id: 2828
  author: tmux C-Left in Terminal.app &laquo; The Fugue
  author_email: ''
  author_url: http://hans.fugal.net/blog/2013/08/13/tmux-c-left-in-terminal-app/
  date: '2013-08-13 01:12:13 -0700'
  date_gmt: '2013-08-13 01:12:13 -0700'
  content: '[&#8230;] I use Terminal.app on OS X, and I want to bind ctrl-left/right
    to cycle through tmux windows (like I did with screen). [&#8230;]'
---
<a href="http://www.gnu.org/software/screen/">GNU Screen</a> is a fantastic tool. It gives you detachable terminal sessions with multiple screens. Most Linux types are familiar with that basic functionality, for which you need to know a very few things: <code>screen</code> starts a screen, <code>C-a c</code> to create a new screen, <code>C-a n</code> and <code>C-a p</code> to navigate,  <code>C-a d</code> to detach, and <code>screen -r</code> to reattach.

But when I'm really in the zone, <code>C-a n/p</code> is too many keystrokes. And I'd like to have a nifty "tab bar", and I'd like to not get lost. Well, I just pimped my screen and now I'll walk you through it.

First, let's get some status information to keep us from getting lost. Add this to <code>~/.screenrc</code>:
<code>
shelltitle "$ |bash"
hardstatus alwayslastline "%{= dg}%Lw%=%H"
</code>

The first line assumes your prompt ends in a '<code>$ </code>' like mine does. Now, to complete the effect, put this in ~/.bashrc:

<pre><code>export PROMPT_COMMAND='echo -ne "\ek\e\\"'</code></pre>

There, a nice "tab bar" that tells you your tabs and the host on which this screen session is running. And it's green. What else could you ask for?

Now, let's set up some awesome keybindings. We'll use <code>C-left</code> and <code>C-right</code>:

<code># ctrl-left/right to switch windows
bindkey "^[[5D" prev # osx
bindkey "^[[5C" next
bindkey "^[[1;5D" prev # linux
bindkey "^[[1;5C" next
# ctrl-T to start a new 'tab' (c-a c)
bindkey "^T" screen</code>

What would you expect to pay for a screen that can do all this? $50? $100? $19.95? But wait, there's more!

Now wouldn't it be nice if you knew which host you were ssh'd into (and your editor or some other program is running so there's no prompt to tell you)? Sure, and I'll show you how. I'll do better than that though. I'll also show you something else you didn't know you wanted:
<code>
# in ~/.ssh/config
Host *
  PermitLocalCommand yes
  LocalCommand /usr/bin/printf '\ek%h\e\\'
# in ~/.bashrc
alias ssh='screen -- ssh'
</code>

The alias causes us to start a new screen for any ssh connection, which keeps your local screen pristine. That's kind of neat.

Update: If you use the <code>LocalCommand</code> thing in ssh, it can break rsync with a cryptic message about protocol versions. The solution is to do this in <code>~/.bashrc</code>:
<code>export RSYNC_CONNECT_PROG='ssh -o PermitLocalOption=no '</code>
