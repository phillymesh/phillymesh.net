---
title: OpenNIC DNS Server Now Online
author: Mike Dank (Famicoman)
type: post
date: 2017-05-17T21:11:46+00:00
url: /2017/05/17/opennic-dns-server-now-online/
draft: true
categories:
  - Philly Mesh
tags:
  - cryptography
  - dns
  - dnscrypt
  - hyperboria
  - opennic
#cspell:ignore opennic dnscrypt ICANN
---
I've recently configured a public DNS server in Amsterdam that resolves domains within the [OpenNIC][1] root, as well as the traditional ICANN registry. This means you can resolve domains using free OpenNIC TLDs (such as .geek, .null, and .pirate) as well as all of your old favorites (you know, those sites on .com, .net, and all the others).

My DNS server is available on the clearnet via IPv4 (at **146.185.176.36**) and IPv6 (at **2a03:b0c0:0:1010::1a7:c001**) on port **53**. Additionally, you can also access the server via _Hyperboria_ with the address **fc16:b44c:2bf9:467:8098:51c6:5849:7b4f**, also on port **53**.

I have also added [DNSCrypt][2] support on port **5353** for all of the addresses above, which allows for authentication between client and server using cryptographic signatures. To connect using DNSCrypt, you will have to install the client and authenticate with the _DNSCrypt-Name_, **2.dnscrypt-cert.opennic.peer3.famicoman.phillymesh.ne**t, and the _DNSCrypt-Key_, **B88F:4860:5517:3696:A3D2:BFE0:ECC7:6175:198F:E012:E101:B4FE:869C:1E9C:4C35:E74F**.

I perform no logging on the server, so you don't have to worry about your queries being cached!

Feel free to try it out, or check the health of the server [here][3].

 [1]: https://www.opennic.org/
 [2]: https://dnscrypt.org/
 [3]: https://servers.opennicproject.org/edit.php?srv=ns7.nh.nl.dns.opennic.glue