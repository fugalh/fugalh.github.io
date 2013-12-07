---
layout: post
status: publish
published: true
title: TLS with OpenLDAP
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
wordpress_id: 61
wordpress_url: urn:uuid:09c02013-fd98-4774-880c-661a32521cb2
date: '2005-10-15 18:42:44.000000000 -07:00'
tags:
- linux
comments: []
---
<p>I just had a battle with OpenLDAP about TLS, and I lost miserably. </p>

<p>If you search google for this error, you will get a lot of hits and almost no
intelligent answers:</p>

<pre><code>ldap_start_tls: Connect error (-11)
        additional info: error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify failed
</code></pre>

<p>My certificates are perfectly valid certificates, signed by my own CA (not
precisely self-signed, but you'd have the same problem with those). OpenLDAP
clients apparently default (at least on RHEL, SLES, and Debian) to require that
LDAP server certificates be valid, including the "check against my local copy
of the CA cert" step.</p>

<p>There's two ways to get it to work, and they are both options that go in your
<code>ldap.conf</code> file: <code>TLS_REQCERT</code> and <code>TLS_CACERT</code>. See <a href="http://www.openldap.org/doc/admin23/tls.html">the OpenLDAP
Administrator's Guide</a> for more
information. </p>

<p>And a word to the wise: don't set your RHEL system that is authenticating with
LDAP to require TLS and then log out, until you've verified that it *actually
is working*. Why RHEL won't let root log in if LDAP isn't working is a bug I
still have to chase down, but it's sure made my afternoon stressful.</p>
