---
layout: post
status: publish
published: true
title: Sensible Graphs with Cacti
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1034
wordpress_url: urn:uuid:aa35c0e8-90ef-4852-9220-73e9d37df933
date: 2009-01-10 05:06:00.000000000 -08:00
tags:
- linux
- statistics
- graph
- data
- cacti
- snmp
- load
- average
- template
- memory
- cdef
- rrdtool
comments:
- id: 1878
  author: Slavko
  author_email: cacti@slavino.sk
  author_url: http://slavino.sk
  date: '2009-03-01 20:33:45 -0800'
  date_gmt: '2009-03-01 20:33:45 -0800'
  content: in your template cacti_graph_template_ucdnet_-_memory_usage_hans.xml is
    an error in CDEF's custom string definition...
- id: 1893
  author: Pia
  author_email: papia_rahman2002@yahoo.com
  author_url: ''
  date: '2009-03-04 16:07:29 -0800'
  date_gmt: '2009-03-04 16:07:29 -0800'
  content: "Hi,\r\nI have memory graph but it is showing NAN value for \"Swap Current\".
    by any chance can you tell me what is wrong and why it is not showing any value
    for the \"Swap\"?\r\nThanks \r\nPapia Rahman"
- id: 1894
  author: Pia
  author_email: papia_rahman2002@yahoo.com
  author_url: ''
  date: '2009-03-04 18:30:30 -0800'
  date_gmt: '2009-03-04 18:30:30 -0800'
  content: what kind of definition "CDEF" will be expecting?
- id: 1934
  author: Dhanil Shah
  author_email: dhandip@yahoo.com
  author_url: ''
  date: '2009-04-06 06:36:37 -0700'
  date_gmt: '2009-04-06 06:36:37 -0700'
  content: "Hi,\r\nI have imported template that you have provided on your site. But
    when I try to plot graph using your template it does not reflect memory usage
    properly. I created New host with Local Linux host, I also tried by creating host
    with Generic SNMP Host template &amp; apllied your template but it shows only
    Buffer memory &amp; Swap memory. It does not show Used, Cache &amp; Free Memory.
    Where am I missing to get the graphs? \r\nDhanil"
- id: 1935
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-06 12:51:51 -0700'
  date_gmt: '2009-04-06 12:51:51 -0700'
  content: "I have received a few emails as well from people who have tried this template.
    All I can say is that this sort of thing in cacti is a bit fragile and I can't
    know where you went wrong. I did my best to make the template as portable as possible,
    but it's going to take some thought and effort on your part unless you're quite
    lucky. \r\n\r\nThat said, I'm happy to go on the clock at my going rate and help
    anyone out, if you can give me (temporary) access to your cacti installation."
- id: 1938
  author: Tarique
  author_email: sjtarique@gmail.com
  author_url: http://tarique21.wordpress.com
  date: '2009-04-08 04:35:15 -0700'
  date_gmt: '2009-04-08 04:35:15 -0700'
  content: "Hi,\r\nI have imported your graph. But it only show me the Swap and Free
    field and rest 3 gives -NaN. I configured this to pull info of a Solaris x86 box.
    Any idea why this happening?? Thank you."
- id: 1957
  author: ''
  author_email: ''
  author_url: ''
  date: '2009-04-28 10:39:54 -0700'
  date_gmt: '2009-04-28 10:39:54 -0700'
  content: The problem with the template xml is that the data source for graph template
    item 1-4, 17-22 falls away.
- id: 1958
  author: daniel
  author_email: daniel@yahoo.com
  author_url: ''
  date: '2009-04-28 10:40:10 -0700'
  date_gmt: '2009-04-28 10:40:10 -0700'
  content: The problem with the template xml is that the data source for graph template
    item 1-4, 17-22 falls away.
- id: 1959
  author: daniel
  author_email: daniel@yahoo.com
  author_url: ''
  date: '2009-04-28 11:36:28 -0700'
  date_gmt: '2009-04-28 11:36:28 -0700'
  content: I think there is something wrong with the CDEF:s. Even if i change the
    rrd file behind the data, i get no graphs.
- id: 1961
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-28 12:52:37 -0700'
  date_gmt: '2009-04-28 12:52:37 -0700'
  content: "I don't know what you're trying to say about things falling away, Daniel.\r\n\r\nCacti
    templates in general are very fragile. Frequently while testing these there would
    be a problem with CDEFs or data sources even on the same system they originated
    on. I did due diligence to make sure they were generic, and tested on several
    other cacti installations to make sure they were generic. \r\n\r\nIf they don't
    work for you, the problem is most likely on your end. Which isn't to say you've
    done anything wrong, it's just the nature of the beast. I can't troubleshoot it
    over email or blog comments, but if you want to hire me to get in your installation
    and troubleshoot do drop me a line. Otherwise, stick at it—I'm sure you'll figure
    it out. Feel free to leave notes on what you had to do here for posterity. And
    if you do find something wrong with my templates, I accept patches."
- id: 1962
  author: daniel
  author_email: daniel@yahoo.com
  author_url: ''
  date: '2009-04-28 13:52:28 -0700'
  date_gmt: '2009-04-28 13:52:28 -0700'
  content: "I mean that the data sources for those items hadnt been registered. It
    would help me a lot if you could post  the names of those. \r\nThat cacti is fragile
    is sadly something i have seen lots of times and im beggining to think about switching
    to zenoss or something else."
- id: 1963
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-28 14:07:52 -0700'
  date_gmt: '2009-04-28 14:07:52 -0700'
  content: "Here's an excerpt from my graph, when I select \"Graph Debug\"\r\n\r\n<code>DEF:a=\"/var/lib/cacti/rra/gwythaint_mem_buffers_145.rrd\":mem_buffers:AVERAGE
    \\\r\nDEF:b=\"/var/lib/cacti/rra/gwythaint_mem_buffers_145.rrd\":mem_buffers:MAX
    \\\r\nDEF:c=\"/var/lib/cacti/rra/gwythaint_mem_cache_146.rrd\":mem_cache:AVERAGE
    \\\r\nDEF:d=\"/var/lib/cacti/rra/gwythaint_mem_cache_146.rrd\":mem_cache:MAX \\\r\nDEF:e=\"/var/lib/cacti/rra/gwythaint_mem_free_147.rrd\":mem_free:AVERAGE
    \\\r\nDEF:f=\"/var/lib/cacti/rra/gwythaint_mem_free_147.rrd\":mem_free:MAX \\\r\nDEF:g=\"/var/lib/cacti/rra/gwythaint_mem_total_148.rrd\":mem_total:MAX
    \\\r\nDEF:h=\"/var/lib/cacti/rra/gwythaint_swap_free_149.rrd\":swap_free:MAX \\\r\nDEF:i=\"/var/lib/cacti/rra/gwythaint_swap_total_150.rrd\":swap_total:MAX
    \\\r\nDEF:j=\"/var/lib/cacti/rra/gwythaint_swap_free_149.rrd\":swap_free:AVERAGE
    \\\r\n</code>"
- id: 1965
  author: daniel
  author_email: daniel@yahoo.com
  author_url: ''
  date: '2009-04-29 07:31:33 -0700'
  date_gmt: '2009-04-29 07:31:33 -0700'
  content: "well my graph look like this:\r\nDEF:a=\"/var/www/html/cacti/rra/mysql_optest_mem_buffers_301.rrd\":mem_buffers:AVERAGE
    \\\r\nDEF:b=\"/var/www/html/cacti/rra/mysql_optest_mem_cache_302.rrd\":mem_cache:AVERAGE
    \\\r\nDEF:c=\"/var/www/html/cacti/rra/mysql_optest_mem_free_303.rrd\":mem_free:AVERAGE
    \\\r\nDEF:d=\"/var/www/html/cacti/rra/mysql_optest_swap_free_1338.rrd\":swap_free:AVERAGE
    \\\r\nDEF:e=\"/var/www/html/cacti/rra/mysql_optest_swap_total_1339.rrd\":swap_total:AVERAGE
    \\\r\n\r\ni have tried to restore your settings by checking in the database, but
    failed.\r\nwhat i want is for you to go in i \"Graph templates\" and choose your
    memory usage template. There you will see graph template items. If you click the
    items you will see what data sources is behind the items.\r\nI want the name of
    the data sources for the items 1-4, 17-22."
- id: 1967
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-04-29 14:06:00 -0700'
  date_gmt: '2009-04-29 14:06:00 -0700'
  content: "There aren't any data sources for items 1-4, 17-22. They are calculated
    by CDEF from the data sources for the other items. That's because there is no
    memory used data source, or swap used data source. (Which is why the cacti default
    graphs are so silly—they took the easy road.)\r\n\r\nOrder is important for the
    CDEFs, which just go by letters. So when you create the graph make sure your data
    sources are, in this order: mem_buffers, mem_cache, mem_free, mem_total, swap_free,
    swap_total."
- id: 1977
  author: jnojr
  author_email: jnojr@yahoo.com
  author_url: ''
  date: '2009-05-11 16:37:29 -0700'
  date_gmt: '2009-05-11 16:37:29 -0700'
  content: "RRDTool Command:\r\n\r\n/usr/bin/rrdtool graph - \\\r\n--imgformat=PNG
    \\\r\n--start=-86400 \\\r\n--end=-300 \\\r\n--title=\"mda-vm1a - Memory Usage\"
    \\\r\n--base=1000 \\\r\n--height=120 \\\r\n--width=500 \\\r\n--alt-autoscale-max
    \\\r\n--lower-limit=0 \\\r\n--vertical-label=\"\" \\\r\n--slope-mode \\\r\n--font
    TITLE:12: \\\r\n--font AXIS:8: \\\r\n--font LEGEND:10: \\\r\n--font UNIT:8: \\\r\nDEF:a=\"/var/www/cacti/rra/mda-vm1a_mem_buffers_88.rrd\":mem_buffers:AVERAGE
    \\\r\nDEF:b=\"/var/www/cacti/rra/mda-vm1a_mem_cache_89.rrd\":mem_cache:AVERAGE
    \\\r\nCDEF:cdefa=g,a,-,c,-,e,-,1024,* \\\r\nCDEF:cdefe=a,1024,* \\\r\nCDEF:cdefi=b,1024,*
    \\\r\nCDEF:cdefbc=a,1024,* \\\r\nCDEF:cdefbg=i,h,-,1024,* \\\r\nCDEF:cdefcc=a,1024,*
    \\\r\nCDEF:cdefcd=a,1024,* \\\r\nAREA:cdefa#FF4105FF:\"Used\"  \\\r\nGPRINT:cdefa:LAST:\"
    \  Current\\:%8.2lf%s\"  \\\r\nGPRINT:cdefa:AVERAGE:\"Average\\:%8.2lf%s\"  \\\r\nGPRINT:cdefa:MAX:\"Max\\:%8.2lf%s\\n\"
    \ \\\r\nAREA:cdefe#00FF004C:\"Buffers\":STACK \\\r\nGPRINT:cdefe:LAST:\"Current\\:%8.2lf%s\"
    \ \\\r\nGPRINT:cdefe:AVERAGE:\"Average\\:%8.2lf%s\"  \\\r\nGPRINT:cdefe:MAX:\"Max\\:%8.2lf%s\\n\"
    \ \\\r\nAREA:cdefi#0000FF4C:\"Cache\":STACK \\\r\nGPRINT:cdefi:LAST:\"  Current\\:%8.2lf%s\"
    \ \\\r\nGPRINT:cdefi:AVERAGE:\"Average\\:%8.2lf%s\"  \\\r\nGPRINT:cdefi:MAX:\"Max\\:%8.2lf%s\\n\"
    \ \\\r\nAREA:cdefbc#FF39324C:\"Free\":STACK \\\r\nGPRINT:cdefbc:LAST:\"   Current\\:%8.2lf%s\"
    \ \\\r\nGPRINT:cdefbc:AVERAGE:\"Average\\:%8.2lf%s\"  \\\r\nGPRINT:cdefbc:MAX:\"Max\\:%8.2lf%s\\n\"
    \ \\\r\nAREA:cdefbg#0000007F:\"Swap\":STACK \\\r\n \\\r\n \\\r\nGPRINT:cdefbg:LAST:\"
    \  Current\\:%8.2lf%s\"  \\\r\nGPRINT:cdefbg:AVERAGE:\"Average\\:%8.2lf%s\"  \\\r\nGPRINT:cdefbg:MAX:\"Max\\:%8.2lf%s\"
    \ \\\r\n \\\r\nAREA:cdefcd#00000019:\"\":STACK\r\n\r\nRRDTool Says:\r\n\r\nERROR:
    invalid rpn expression in: g,a,-,c,-,e,-,1024,*\r\n\r\n\r\nMaybe this could be
    fixed in your template?  It's Greek to me, so I don't have an answer unfortunately
    :-)"
- id: 1978
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-05-12 13:42:09 -0700'
  date_gmt: '2009-05-12 13:42:09 -0700'
  content: You're looking in the right place - you see that the problem is the lack
    of DEFs. You only have two. This isn't something that is handled in the template,
    but rather you hooking up the data sources to the graph.
- id: 1979
  author: jnojr
  author_email: jnojr@yahoo.com
  author_url: ''
  date: '2009-05-12 18:05:02 -0700'
  date_gmt: '2009-05-12 18:05:02 -0700'
  content: Sorry, I have no idea what you just said :-)  How does one "hook up a data
    source to a graph"?  It sounds like there are some extra steps to using your template
    than simply specifying it under Graph Management - Graph Template Selection.  What
    do I need to do to get the graphs drawn with your template?
- id: 1981
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-05-13 03:55:16 -0700'
  date_gmt: '2009-05-13 03:55:16 -0700'
  content: Unfortunately there's no subsitute here for a thorough understanding of
    Cacti concepts. Some quality time with the manual will be of great help.
- id: 1999
  author: charles
  author_email: megatron_007@yahoo.com
  author_url: ''
  date: '2009-05-23 02:31:37 -0700'
  date_gmt: '2009-05-23 02:31:37 -0700'
  content: "How can I run cacti verbose query locally in my cacti box command console?\r\nI
    want to make a script and place it in the cronjob so I wouldn't need to update
    it manually, by clicking on verbose query in cacti web interface, whenever I change
    any port names on the switch. Any one knows how?"
- id: 2013
  author: jnojr
  author_email: jnojr@yahoo.com
  author_url: ''
  date: '2009-06-03 23:22:58 -0700'
  date_gmt: '2009-06-03 23:22:58 -0700'
  content: "http://forums.cacti.net/viewtopic.php?t=32593&amp;highlight=\r\n\r\nAccording
    to one of the cacti developers:\r\n\r\n\"The given CDEF refers to other DEFs (data
    sources) by position (in this case: by letters &gt;= c). But those letters do
    not show up in that graph statement.\r\nWe recently fixed an error with 087b,
    where 087b unfortunately created a lot more DEFs than required. If the given template
    was tailored to 087b, it should be changed to 087d by the original author\"\r\n\r\nIs
    there any chance this can get fixed?  The whole purpose of a template is so that
    people who use cacti do not have to get a Ph.D in atomic rocket surgery to use
    it."
- id: 2014
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-06-03 23:52:39 -0700'
  date_gmt: '2009-06-03 23:52:39 -0700'
  content: That would explain the pain and frustration we're all feeling, thanks.
    I will happily post an updated template for it here if someone sends me one that
    works for 087d. When I end up upgrading to 087d I will do it myself - but when
    exactly I do that is unknown but probably at least October. (Ubuntu 9.04 appears
    to still have 087b, but if someone sends me a .deb or a link to a .deb for 087d
    that works with Ubuntu 8.10 or 9.04 I may be able to do it sooner.)
- id: 2015
  author: Billy
  author_email: billy@gunn.org
  author_url: ''
  date: '2009-06-04 17:01:08 -0700'
  date_gmt: '2009-06-04 17:01:08 -0700'
  content: "The article shows the correct cdef to use with 0.8.7d, its just not correct
    in the template. Editing the cdefs as follows seems to do the trick:\r\n\r\nMemory
    Used (Hans)\r\nitem1: d,a,-,b,-,c,-\r\n\r\nSwap Used (Hans)\r\nitem1: e,f,-"
- id: 2016
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2009-06-04 17:11:39 -0700'
  date_gmt: '2009-06-04 17:11:39 -0700'
  content: Thanks Billy. I've made that change blindly, if someone can redownload
    it and verify that it imports cleanly in 087d that would be great.
- id: 2019
  author: Kaan
  author_email: kaan.kivilcim@alluremedia.com.au
  author_url: ''
  date: '2009-06-10 05:27:35 -0700'
  date_gmt: '2009-06-10 05:27:35 -0700'
  content: "Hey Hans,\r\n\r\nThe updated templates work perfectly with 087d."
- id: 2020
  author: Jon Smith
  author_email: smithj@thelazysysadmin.net
  author_url: http://www.thelazysysadmin.net/
  date: '2009-06-11 06:02:41 -0700'
  date_gmt: '2009-06-11 06:02:41 -0700'
  content: Really simple change for the Load Avg graph. Never really thought of doing
    that way, always accepted the default. Thanks for the tip.
- id: 2073
  author: Martin W
  author_email: talisson@gmail.com
  author_url: ''
  date: '2009-07-16 20:56:29 -0700'
  date_gmt: '2009-07-16 20:56:29 -0700'
  content: 'The memory graph is a bit strange. First the cdef for the swap should
    be f,e,- otherwise it will become a negative value, it did here at least. Secondly
    item #24 in the graph template should be removed, because it fills no purpose
    and breaks the graph(it adds a stack with swap free). I''ve tried this in 087d
    btw.'
- id: 2079
  author: Mxx
  author_email: mxxcon@gmail.com
  author_url: ''
  date: '2009-07-22 16:39:42 -0700'
  date_gmt: '2009-07-22 16:39:42 -0700'
  content: "I confirm these changes work in 87d\r\n\r\nMemory Used (Hans)\r\nitem1:
    d,a,-,b,-,c,-\r\n\r\nSwap Used (Hans)\r\nitem1: f,e,-\r\n(not e,f,- otherwise
    swap is negative amount)"
- id: 2094
  author: Coert Waagmeester
  author_email: lgroups@waagmeester.co.za
  author_url: ''
  date: '2009-08-25 08:35:58 -0700'
  date_gmt: '2009-08-25 08:35:58 -0700'
  content: "Hello Hans,\r\n\r\nThanks for you awesome Graph Templates!\r\n\r\nRegards,
    Coert from South Africa"
- id: 2364
  author: BuggedTech
  author_email: ismael.angelo@casimpan.com
  author_url: http://www.buggedtech.com
  date: '2011-02-16 01:54:26 -0800'
  date_gmt: '2011-02-16 01:54:26 -0800'
  content: "I've been exposed to cacti but haven't tried configuring it yet. Good
    to know the graph is modifiable for usability specially for those who are new
    to it. I for one was misled at first on the stacked graph.\r\n\r\nThanks a lot
    :)"
- id: 2408
  author: ant
  author_email: ant@symons.net.au
  author_url: ''
  date: '2011-07-26 02:45:17 -0700'
  date_gmt: '2011-07-26 02:45:17 -0700'
  content: I have been finding on my cacti install that I get NaN for any new graph
    I add (including these ones) and need to go management-&gt;data sources then load
    each relevant source for the new graph and hit save without changing anything.
    I had to do this originally, and just do it again with these templates. Now things
    look nice and useful on my new server. Thanks for the templates!
- id: 2419
  author: Chris
  author_email: chiestand@salk.edu
  author_url: ''
  date: '2011-08-17 18:55:47 -0700'
  date_gmt: '2011-08-17 18:55:47 -0700'
  content: Great work, these are very nice touches and thanks for sharing! They worked
    fine on my cacti server - I only got NaN before data was collected. If you get
    NaN try waiting 30 minutes or so.
- id: 2431
  author: Brian Candler
  author_email: b.candler@pobox.com
  author_url: ''
  date: '2011-10-18 12:59:12 -0700'
  date_gmt: '2011-10-18 12:59:12 -0700'
  content: "Excellent description, many thanks. There was one thing else I had to
    do: in Ubuntu 10.04 with Cacti 0.8.7e, the load average graph includes a fourth
    black line which is the total of all the other data sources:\r\n\r\nItem #7 (No
    task): Total  LINE1  000000\r\n\r\nYou just need to delete this by clicking the
    'X' on the right to get the correct finished graphs."
- id: 2437
  author: Glyn
  author_email: glyn@8kb.co.uk
  author_url: http://www.8kb.co.uk
  date: '2011-11-09 10:35:59 -0800'
  date_gmt: '2011-11-09 10:35:59 -0800'
  content: "Nice template Hans, thanks.\r\n\r\nIf anybody is using this to monitor
    a system with more than 100GB of memory and getting NaN values, you just need
    to alter the \"Data Source Item Maximum Value\" in the data template to the size
    you need, then either delete or use rrdtool to tune your rrd files."
- id: 2438
  author: Bastien Chong
  author_email: ''
  author_url: ''
  date: '2011-11-15 21:02:20 -0800'
  date_gmt: '2011-11-15 21:02:20 -0800'
  content: rrdtool tune xxx.rrd --maximum dataSource_name:200000000
- id: 2466
  author: Fernando
  author_email: fretagi@mcel.co.mz
  author_url: ''
  date: '2011-12-21 14:26:59 -0800'
  date_gmt: '2011-12-21 14:26:59 -0800'
  content: I am struggling to setup cacti in one of my solaris 10 servers.... pls
    help
- id: 2538
  author: Matrix Plus &raquo; cacti中mem数据为空的解决方案
  author_email: ''
  author_url: http://sealhuang.sinaapp.com/?p=16
  date: '2012-04-13 12:38:59 -0700'
  date_gmt: '2012-04-13 12:38:59 -0700'
  content: '[...]  由于cacti用户监控负载和内存的图可读性不是很好，这里推荐一个不错的模板。    分类: Linux 标签: cacti,
    Linux        评论 (0) Trackbacks (0) 发表评论 [...]'
- id: 2719
  author: asset management outsourcing
  author_email: kazukokeeling@gmx.de
  author_url: http://softwarelivre.org/susan07gas/bgboocro92055
  date: '2013-01-19 08:28:05 -0800'
  date_gmt: '2013-01-19 08:28:05 -0800'
  content: Very nice write-up. I absolutely appreciate this website. Keep writing!
- id: 2732
  author: tolaris.com Better Cacti memory usage graphs | tolaris.com
  author_email: ''
  author_url: https://www.tolaris.com/2013/02/28/better-cacti-memory-usage-graphs/
  date: '2013-02-28 22:39:51 -0800'
  date_gmt: '2013-02-28 22:39:51 -0800'
  content: '[...] data and do the math. This is unnecessary, and (slightly) slower
    than using Cacti CDEF functions. Hans Fugal used CDEF functions, but his graphs
    use an eye-searing colour scheme. He also uses the wrong base; [...]'
---
<p>I love <a href="http://www.cacti.net/">Cacti</a>. It's an excellent tool for visualizing interesting statistics like bandwidth usage, CPU and load average, memory usage, etc. It's relatively straightforward to set up, if slightly klunky, and it takes a lot of guesswork out of questions that are otherwise difficult to answer. (I should note here that Cacti is a sort of front-end to <a href="http://oss.oetiker.ch/rrdtool/">RRDtool</a> which does all the hard work as far as the visualization is concerned.)</p>

<p>But some of the default graphs that come with Cacti are absolute rubbish. I took it upon myself to fix the two worst offenders this week: the load average graph and the memory usage graph. Let's compare, shall we?</p>

<p>Here's the default load average graph:</p>

<p><img src="/cacti/loadavg-default.png" alt="default load average graph"/></p>

<p>This graph is just plain <em>wrong</em>. It stacks the load averages one on top of the other which makes it impossible to get a real reading for the 5 and 15 minute averages, and makes things look worse than they are. If that textual explanation went over your head, compare with this repaired load average graph and all will be made clear:</p>

<p><img src="/cacti/loadavg.png" alt="my load average graph"/></p>

<p>Wow, you can actually see how the averages are, well, averages. Funny thing about proper graphs.</p>

<p>This change is simple enough to do yourself so I won't provide a template download in the interest of expanding your mind (hopefully without exploding your skull). Right after I show you my pretty memory usage graph, that is.</p>

<p>First, let's see the default memory usage graph:</p>

<p><img src="/cacti/memory_usage-default.png" alt="default memory usage graph"/></p>

<p>If you can tell what that graph is saying at a glance, you're better than I. This one doesn't so much lie as beat around the bush. The vital information is there, if you know how to read it. The key is that the stuff you see totals the RAM that is available for programs to consume (free+buffers+cache), so the smaller the area of the graph, the less memory you have available. It also doesn't show swap. Swap is available on another graph (also in terms of free swap not swap used), but on a separate graph you miss out on the relative comparison.</p>

<p>Here's the memory graph I came up with:</p>

<p><img src="/cacti/memory_usage.png" alt="my memory usage graph"/></p>

<p>I think it is self-explanatory and that it has all the information you could ask of a memory usage graph presented in the clearest possible way. Maybe I'm a bit biased, but you have to admit it's better.</p>

<p>So how do we modify and create graphs in Cacti for fun and profit? Let's begin with the load average graph. No, scratch that. Let's begin with some terminology.</p>

<p>Cacti has graph templates that define what the graph will look like. We'll spend a lot of time creating and modifying those. It also has data templates for telling it how to get the data (e.g. the SNMP OID or the script to run). You use a data template to create a data source which actually fetches and stores that data, and you use a graph template to create a graph that is associated with a device (host) and its data sources. Data sources are usually created automatically when you create a graph. There's one more oddball thing called a <a href="http://oss.oetiker.ch/rrdtool/tut/cdeftutorial.en.html">CDEF</a> which is basically a rudimentary <acronym title="Reverse Polish Notation">RPN</acronym> calculator that you have to define the expressions for ahead of time in the most excruciatingly painful way. But we'll need a couple for the memory usage graph.</p>

<p>SNMP stands for Simple Network Management Protocol, which naturally means that it's the antithesis of simple and that it is mostly used for monitoring instead of management (though you can indeed use it for management, which is way beyond the scope here). The short of it is, you have devices that talk SNMP and you can get info about interesting things that you'd like to graph with Cacti over the network. If you have a linux box, it can be made to talk SNMP by installing <a href="http://www.net-snmp.org/">Net-SNMP</a> and configuring it. </p>

<p>SNMP version 3 is a complicated mess to configure because you have to have a PhD in network security to understand its authentication schemes (in which case you might conclude that it's not secure enough). Versions 1 and 2c are both sufficient for my needs, and from our point of view they're essentially identical and simple enough to explain. I'll assume you use version 2c. There's a cleartext password for read-only access and optionally one for read-write access (for that management thing that we don't do). In order to keep things (anti)simple, they're not called passwords but rather "community strings". The default community strings for when you really can't be bothered to change them are "public" and "private", and most SNMP devices come with these defaults preset. What's that? You didn't realize you had several (dozens?) of devices on your network just waiting for some bored employee to start playing with its settings from the comfort of his workstation because you didn't change the default read-write community string? Well, you do.</p>

<p>Here's the snmpd config file I use, which I don't mind sharing because the only way you can get to it is over my LAN or my VPN, and it's read-only anyway and I have no secrets about my host stats.</p>

<pre><code>rocommunity  yoursecrethere
syslocation  "Las Cruces"
syscontact  hans@fugal.net
sysservices 79
</code></pre>

<p>If you can't figure out how to tweak the configuration file included with your distro (which is no doubt hundreds of lines long with loads of comments), you can replace it with something like that and you'll be up and running with SNMP version 2c.</p>

<p>Ok, now you can install Cacti. Then create a device using the ucd/net SNMP device template for the host you want to monitor (you don't technically have to do that with localhost but you'd have to modify my graphs to use the non-SNMP data sources). When the device is created and it says it was able to connect to it ok, then you can create graphs for the device. Go ahead and create the "ucd/net - Load Average" graph. Then you'll no doubt dash over to the graphs "tab" and be totally dismayed that the graph seems broken. Fear not, it'll show up once it's had some time to gather data (check back in 5 minutes).</p>

<p>In the meantime we can go fix the load average graph template. Any changes we make will apply to the graph we just created as well as any new graphs we create with that template. Go to "Graph templates" on the left then find the graph of interest and click on its name. Take a moment familiarizing yourself with this page, then click on the 5 minute average item to edit it. Here you change the graph item type from STACK to LINE1. I also changed the color to 002ABF which shows up better. Do the same for the 15 minute average item (LINE1, I left the color alone). Now go refresh your graph and you'll see the changes. Et voilà, you are a Cacti graph template hacker. At this point you may feel the irresistable urge to change the colors of some of the more ugly but functional graphs, and I won't hinder you. I'll wait right here.</p>

<p>Ok, the memory usage graph is a bit more work. I won't take you through it step by step but I'll point out a couple of gotchas that I encountered when creating it. First, I realize that others have made memory usage graphs and provided them on forums and such to download. After the third one failed to work I decided it was better to just make my own. Hopefully mine will work for you—I put a bit of effort into making sure it would import cleanly.</p>

<p>There's actually a reason why the memory usage graphs are so backwards: because most devices provide total and free stats but not used stats. Obviously they expect you to calculate used yourself. So directly graphing the bits provided by SNMP was the easy way out.</p>

<p>We, on the other hand, have chosen the path of pain. We need to calculate memory used (which is total-(free+cache+buffers)). We could do this with a script but that's sticky and not very portable (depending on the target distro, version of Cacti, etc.). The better thing is to use a CDEF. If you click on graph management the CDEFs link is revealed. We want a CDEF that calculates (total-free-cache-buffers)*1024 (the sources are kilobytes). Now, a CDEF uses a positional reference system. The first data source used by your graph is a, the second is b, and so on. So the CDEF string will look something like <code>d,a,-,b,-,c,-,1024,*</code>. But here's where things get dodgy—it's hard to know what order the data sources will settle on until after you've created the graph. If you create the graph in the right order (no shuffling) and you realize that the AVERAGE and MAX consolidation functions create separate data source (but not LAST), and who-knows-what other pitfalls, then you can be confident ahead of time. Or, you can just create the template, create a graph using the template, and look at the graph debug output to figure out which source is which. </p>

<p>So now you create a new graph template, and referring to a template similar to what you want you fill in all the right fields, leave most at their defaults, add graph items, tweak and refresh a sample graph using your template a gazillion times, go back and forth with the CDEFs getting things right, then create new (temporary) graphs to make sure it works.</p>

<p>Luckily for you, if all you want is a cool memory graph, I did all this for you. <a href="/cacti/cacti_graph_template_ucdnet_-_memory_usage_hans.xml">Download</a> and <a href="http://www.cacti.net/downloads/docs/html/template_import.html">import</a> my memory usage graph template, create a graph, and in a day or so you'll have a memory usage graph as pretty as mine. Oh, alright, I'll provide a <a href="/cacti/cacti_graph_template_ucdnet_-_load_average_hans.xml">load average template</a> for you as well.</p>
