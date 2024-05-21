---
layout: post
status: publish
published: true
title: Asynchronous Kindle Transfer
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 1242
wordpress_url: http://hans.fugal.net/blog/?p=1242
date: '2010-12-28 18:58:59.000000000 -08:00'
tags:
- osx
- automation
- bash
- usb
- kindle
- automator
- ebook
comments:
- id: 2327
  author: tuxgirl
  author_email: TuxGirl@gmail.com
  author_url: ''
  date: '2010-12-30 18:40:45 -0800'
  date_gmt: '2010-12-30 18:40:45 -0800'
  content: "congrats on the kindle! i love mine!\r\n\r\nmobileread has better versions
    of most PD classics than gutenberg does.  \r\n\r\nbtw, if you're loving gutenberg,
    please check out pgdp and become a proofreader. it's totally worth-it to help
    preserve books for the future generations. \r\n\r\nanother option for staging
    books is calibre. it's great OSS that can be found at calibre-ebook.com. It can
    even do conversions from a bunch of other formats for you."
---
I got a Kindle for Christmas, and it's pretty cool. Project Gutenberg never looked so nice. Getting ebooks onto it is pretty simple, just drag and drop. But that only works when the Kindle is plugged in, and I know I will think to download a book usually when the Kindle is not plugged in. Then I have to dig through my downloads folder (which makes a teenager's room look tidy) and find the ebook(s) and drag onto the Kindle. This needs to be automated.

It's actually pretty simple. First, make a "staging" folder. I put mine at ~/Desktop/Kindle. Then, fire up Automator and create a new "Folder Action". Choose /Volumes: whenever anything is added to /Volumes (e.g. when mounting a drive like the Kindle) it will execute. Add the action "Run a Shell Script". Here is my script:
<pre><code>src=$HOME/Desktop/Kindle
dst=/Volumes/Kindle

cd "$src"
while read item; do
  if [ "$item" = "$dst" ]; then
    rsync -av --remove-source-files "$src"/ "$dst"/ | logger -t Kindle
  fi
done

</code></pre>

The --remove-source-files option to rsync makes this essentially a recursive move operation. So your staging folder will be empty once it has successfully synced—if you want to keep an off-Kindle backup of your ebooks you won't keep them in the staging folder. (You could omit --remove-source-files, but then if you deleted a book from your kindle it would just be put back the next time you plugged it in which would be annoying.)

The staging folder has the same directory structure as the Kindle, so put the documents you want to copy over into ~/Desktop/Kindle/documents/.
