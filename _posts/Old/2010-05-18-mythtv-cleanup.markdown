---
layout: post
status: publish
published: true
title: Mythtv Cleanup
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1217
wordpress_url: http://hans.fugal.net/blog/2010/05/18/mythtv-cleanup/
date: '2010-05-18 08:01:22.000000000 -07:00'
tags:
- mythtv
comments:
- id: 2251
  author: aflores3
  author_email: afloresiii@gmail.com
  author_url: ''
  date: '2010-05-18 21:43:03 -0700'
  date_gmt: '2010-05-18 21:43:03 -0700'
  content: "Thanks for the write-up. I started mucking around with my install and
    created a few orphans. \r\n\r\nWould you mind explaining \"grep 'should be local'
    /var/log/mythtv/mythbackend.log | egrep -o \"[0-9_]*\\.(mpg|nuv)\" | xargs touch\"
    more in detail?"
- id: 2252
  author: Hans
  author_email: hans@fugal.net
  author_url: http://hans.fugal.net/
  date: '2010-05-18 21:54:52 -0700'
  date_gmt: '2010-05-18 21:54:52 -0700'
  content: "Sure. \r\n\r\nFirst we grep for 'should be local' to filter out all lines
    except ones that look something like\r\n \r\n<pre>2010-05-04 07:00:04.494 ProgramInfo,
    Error: GetPlaybackURL: '1119_20100503193200.mpg' should be local, but it can not
    be found.</pre>\r\n\r\nThen we pipe that into a second grep that greps for the
    filename. The -o flag means print only the matching part, and the result is a
    list of filenames.\r\n\r\nFinally, we create empty files with those names using
    touch. Once those files exist, though they're just empty files, MythTV will find
    them and will know how to delete them.\r\n\r\nYou don't want to do this for files
    that are just temporarily missing e.g. in a secondary storage directory that's
    offline at the moment. That could result in MythTV orphaning those files and it
    would never delete them and they'd just sit there taking up space. (Which brings
    us full circle to the first part of my post.)"
---
A couple tricks on manually cleaning up the mess if mythtv gets screwed up.

First, go into your recording directory and "rm *.png". This will remove all the preview images. Now page through the list of recordings and they'll all be rebuilt (this step may require some patience). Now look in the directory again (ls) and notice if there are any video files not accompanied by a .png file—if there are then they're orphaned and you can delete them (or move them somewhere where you can watch them by hand later).

Now pull up your recordings in mythweb and sort by size. Any that are 0 bytes, you should delete (no, I don't know a faster way than clicking and confirming each one).

Finally, if mythtv has something in its db that isn't on disk, it can cause trouble when it's trying to autoexpire. So do this in your recording directory:
<pre>grep 'should be local' /var/log/mythtv/mythbackend.log | egrep -o "[0-9_]*\.(mpg|nuv)" | xargs touch</pre>
