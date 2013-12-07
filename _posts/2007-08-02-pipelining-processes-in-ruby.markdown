---
layout: post
status: publish
published: true
title: Pipelining Processes in Ruby
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 859
wordpress_url: urn:uuid:c648280b-4a34-4a6b-9083-349d2177e27d
date: '2007-08-02 15:58:00.000000000 -07:00'
tags:
- ruby
- shell
- pipe
comments:
- id: 1594
  author: Levi
  author_email: levi@cold.org
  author_url: http://lifeoflevi.com/blog/
  date: '2007-08-03 12:11:22 -0700'
  date_gmt: ''
  content: |-
    <p>If you want to look for some inspiration for metaprogramming constructs to do nifty shell-like things, look no further than <a href="http://www.scsh.net/" rel="nofollow">scsh</a>, the Scheme shell.  It also has the distinction of having the most hilarious <a href="http://www.scsh.net/docu/html/man.html" rel="nofollow">Acknowledgements</a> section of any reference manual I've ever seen.</p>

    <p>To run the equivalent of "foo   | bar  ", you'd do (| (foo arg1 arg2) (bar arg1 arg2)).  Your syntax seems pretty similar, except you have to manually parse the command lines into strings.  That's just the tip of the scsh iceberg, though, so I recommend taking a look at at least the <a href="http://www.scsh.net/docu/html/man-Z-H-1.html#node_toc_node_sec_2.2" rel="nofollow">Process Forms</a> section of the manual for inspiration.</p>
- id: 1595
  author: Ondemannen
  author_email: ''
  author_url: ''
  date: '2007-08-06 06:28:27 -0700'
  date_gmt: ''
  content: |-
    <p>Hiya, never used fork with Ruby before but I've done something similiar in Perl.</p>

    <p>FORK:<br />
    my $pid;<br />
    if ($pid = fork ) {<br />
        ... do stuff ...<br />
    } elsif (defined($pid) ) {<br />
        ... do more stuff ...<br />
    } elsif($! == EAGAIN) {<br />
        ... sleep and redo FORK ...<br />
    } else {<br />
        ... could not fork ...<br />
    }<br /></p>

    <p>Don't know if this will help you debug the open files ...</p>

    <p>cheers</p>
---
<p>I've occasionally needed to pipeline some processes in Ruby, especially when doing sysadmin-type tasks. You can always do:</p>

<pre><code>system "foo | bar"
</code></pre>

<p>but that gets interpreted by the shell. That can be a problem when you need to
include filenames that could have all kinds of nastiness including spaces,
semicolons, exclamation points, etc. You should be shaking in your boots about
now.</p>

<p>Well, for single processes, it's easy:</p>

<pre><code>system "foo", arg1, arg2
</code></pre>

<p>But if you want to pipe them together it's a bit more difficult. I came up with
this solution, and it seems to be working well in my "convert my cool music
collection into a lame (wink) format my car stereo can understand" script:</p>

<pre><code>  def pipeline(*args)
    pids, r = args.inject([[],nil]) do |memo, cmd|
      pids, rr = memo
      r,w = IO.pipe
      if (pid = fork)
        pids.push pid
        rr.close if rr
        w.close
        [pids, r]
      else
        r.close
        $stdin.reopen rr if rr
        $stdout.reopen w
        cmd = [cmd] if String === cmd
        exec *cmd
      end
    end
    r.close
    pids.each {|p| Process.waitpid(p)}
  end

  pipeline ['oggdec','-o','-',oldpath],['lame','-',newpath]
</code></pre>

<p>Do take the time to figure out what's going on, but don't do it without a piece
of paper handy or you might sprain something.</p>

<h2>Update</h2>

<p>I had an error in the original post—if you don't close rr in the parent of the fork you will end up with too many open files eventually.</p>
