---
title: Browse the Philly Mesh Site from Hyperboria
author: Mike Dank (Famicoman)
type: post
date: 2017-03-14T18:23:59+00:00
url: /2017/03/14/browse-the-philly-mesh-site-from-hyperboria/
draft: true
categories:
  - Philly Mesh
tags:
  - certificates
  - cjdns
  - gpg
  - hyperboria
  - "let's encrypt"
  - ssl
  - tls

---
The Philly Mesh website is now available from Hyperboria. The new subdomain **h.phillymesh.net** will resolve to **[fc4a:cb93:88dc:32e1:43ec:e1b8:2b45:dd46]** and is available via both HTTP and HTTPS:

  * http://h.phillymesh.net
  * https://h.phillymesh.net

As cjdns encrypts traffic end-to-end, standard HTTP should be acceptable in most configurations. You will want to use the HTTPS link if you connect to Hyperboria via a cjdns gateway on a different machine or if you share the machine running cjdroute.
 

If you do use HTTPS, you will likely get a warning from the browser that the certificate is invalid as it is issued for an IP in a private address space (as all Hyperboria addresses are). Be aware, there should be no issue with [this certificate](https://www.ssllabs.com/ssltest/analyze.html?d=h.phillymesh.net). In the future, I may go through the process of configuring a CA for phillymesh.net (self-signing a cert for h.phillymesh.net and distributing the root cert, signed with my GPG key, but don't find it necessary right now. The current certificate is issued by Let's Encrypt.
 