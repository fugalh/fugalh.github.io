---
layout: post
status: publish
published: true
title: Daemonized Screen With Multiple Pages
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 64
wordpress_url: urn:uuid:69ecd2f1-bfe1-4f4d-a04c-32227875b698
date: '2004-06-28 15:43:58.000000000 -07:00'
tags:
- linux
comments: []
---
<p><p>So you want to start up a screen session with multiple processes running in multiple windows, e.g. for monitoring logs. And you want to do it on reboot.</p>

<pre>
# $HOME/backuplogs.screenrc
screen /opt/tivoli/tsm/client/ba/bin/dsmadmc
screen -t dsmserv ssh tea 'tail -f /var/log/dsmserv/current; bash -l'
screen -t tea ssh tea 'tail -f /var/log/dsmsched/current; bash -l'
screen -t marvin ssh marvin 'tail -f /var/log/dsmsched/current; bash -l'
screen -t vogon ssh vogon 'tail -f /var/log/dsmsched/current; bash -l'
screen -t dent ssh dent 'tail -f /var/log/dsmsched/current; bash -l'
screen -t prefect ssh prefect 'tail -f /var/log/dsmsched/current; bash -l'

# crontab entry
@reboot screen -dmS backuplogs -c $HOME/backuplogs.screenrc
</pre>
