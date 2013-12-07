---
layout: post
status: publish
published: true
title: Postfix SMTP auth
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 938
wordpress_url: urn:uuid:3dd940c6-5022-4ed4-b9cf-515e463b2a4b
date: 2008-02-28 09:05:21.000000000 -08:00
tags:
- linux
- postfix
- smtp
- mail
- sasl
- tls
- ssl
comments:
- id: 1721
  author: Ajit
  author_email: aishwarya_aishwaryaa@yahoo.com
  author_url: http://www.correcty.org
  date: '2008-02-29 01:00:15 -0800'
  date_gmt: ''
  content: <p>Very good codes. Thank you for sharing this! Authentication and encryption
    should be very useful.</p>
---
<p><a href="http://www.postfix.org/">Postfix</a> is my <acronym title="Mail Transport Agent">MTA</acronym> of choice. Recently I had a second opportunity to set up relaying from Postfix to Postfix, with TLS and authorization. Seeing how I remembered precious little from the first time, I decided it would be a good thing to blog on.</p>

<p>The documentation on doing this is really quite good, but you have to get acclimated to the acronym soup before it makes any sense at all. The first and most mysterious acronym is <a href="http://asg.web.cmu.edu/sasl/"><acronym title="Simple Authentication and Security Layer">SASL</acronym></a>.</p>

<blockquote>
    <p>SASL is the Simple Authentication and Security Layer, a method for adding authentication support to connection-based protocols. To use SASL, a protocol includes a command for identifying and authenticating a user to a server and for optionally negotiating protection of subsequent protocol interactions. If its use is negotiated, a security layer is inserted between the protocol and the connection.</p>
</blockquote>

<p>If that's not a mouthful… Basically, SASL is a library and daemon that programs, like Postfix, can use to do authentication. The <a href="http://www.postfix.org/SASL_README.html">Postfix SASL Howto</a> tells you all you need to know about configuring Postfix for Cyrus or Dovecot SASL. It also tells you how to configure either Dovecot or Cyrus SASL for Postfix.</p>

<p>I'm using Debian stable (4.0), and this is what I did. On both the client and server you need the <code>postfix-tls</code> package which includes SASL and TLS support for Postfix. On the server I had to install the <code>sasl2-bin</code> package (this is not at all obvious at first pass—I was looking for a <code>saslauthd</code> package). Then I had to enable <code>saslauthd</code> by editing <code>/etc/default/saslauthd</code>. The <code>smtpd.conf</code> file is in <code>/etc/postfix/sasl</code> on Debian, and it looks like this:</p>

<pre><code>pwcheck_method: saslauthd
mech_list: PLAIN LOGIN
</code></pre>

<p>Here's the relevant snippet from <code>/etc/postfix/main.cf</code>:</p>

<pre><code>smtpd_sasl_auth_enable = yes
smtpd_sasl_application_name = smtpd
smtpd_sasl_security_options = noanonymous
smtpd_recipient_restrictions =
    permit_mynetworks
    permit_sasl_authenticated
    reject_unauth_destination
</code></pre>

<p>Now, there's a problem. Debian runs Postfix in a chroot jail by default, which means you need to make special provision for Postfix to be able to find the <code>saslauthd</code> socket. This can be as easy as </p>

<pre><code>mv /var/run/saslauthd/ /var/spool/postfix/var/run/
ln -s /var/spool/postfix/var/run/saslauthd/ /var/run/
</code></pre>

<p>You may also need to <code>adduser postfix sasl</code>, though I'm not sure if this is necessary.</p>

<p>That's it for the server. Now, on the client you need this in <code>/etc/postfix/main.cf</code>:</p>

<pre><code>smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
relayhost = [mail.example.com]
smtp_sasl_security_options = noanonymous
</code></pre>

<p><code>/etc/postfix/sasl_passwd</code> looks like this:</p>

<pre><code>[mail.example.com] username:password
</code></pre>

<p>You need to <code>postmap /etc/postfix/sasl_passwd</code> after changing it.</p>

<p>Now, authentication is well and good, but you don't want to be sending those passwords in the clear, especially when using the default PAM authentication source. So, you also need to configure TLS.</p>

<p>The <a href="http://www.postfix.org/TLS_README.html">Postfix TLS README</a> tells you all you need to know for this. You need to create a certificate for the server, enable the use of TLS on both sides, and tell the server not to accept authentication without TLS. That last bit is perhaps the most vital element for security, though of course it does nothing to help you get TLS actually working. Here's the config snippet:</p>

<pre><code># client
smtp_use_tls = yes # This option deprecated in later versions of Postfix

# server
smtpd_tls_CAfile = /etc/ssl/CA/cacert.pem
smtpd_tls_cert_file = /etc/ssl/certs/mail.pem
smtpd_tls_key_file = /etc/ssl/private/mail.pem
tls_random_source = dev:/dev/urandom
smtpd_tls_loglevel = 1
smtpd_use_tls = yes # also deprecated
</code></pre>

<p>Creating the certificates is nothing extraordinary, but this seems like a good time to post my <code>/etc/ssl/README</code> file:</p>

<pre><code>self-signed:
    openssl req -new -nodes -out newreq.pem
    openssl x509 -req -signkey privkey.pem -in newreq.pem -out cert.pem

create CA:
openssl req -nodes -new -x509 -days 3650
    -keyout CA/private/cakey.pem -out CA/cacert.pem

generate request:
openssl req -new -text -nodes -keyout newkey.pem -out newreq.pem

sign request:
openssl ca -in newreq.pem -out newcert.pem -days $((365*2))

Don't forget to keep private keys private.
</code></pre>

<p>So there it is. Authentication and Encryption at your fingertips.</p>
