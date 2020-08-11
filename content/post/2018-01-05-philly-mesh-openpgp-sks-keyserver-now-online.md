---
title: Philly Mesh OpenPGP SKS Keyserver Now Online
author: Mike Dank (Famicoman)
type: post
date: 2018-01-05T18:26:37+00:00
url: /2018/01/05/philly-mesh-openpgp-sks-keyserver-now-online/
draft: true
categories:
  - Philly Mesh
tags:
  - cjdns
  - encryption
  - gnupg
  - gpg
  - hkp
  - hkps
  - hyperboria
  - key
  - keyserver
  - openpgp
  - pgp
  - sks
  - tor

---
Hey all,

After a trial run of setting up a keyserver over the summer, I am now making the [Philly Mesh OpenPGP Keyserver][1] public for all to use. 

The keyserver currently runs [SKS][2], and is ideal for uploading or downloading [gpg/pgp][3] keys. A great feature of SKS is that it has what are known as "gossip peers." Gossip peers help with the transmission of keys uploaded on each node by sending them to all other nodes they gossip with. This creates a web that allows all nodes to communicate and transfer keys through one another. Ultimately, if a key is uploaded to one node, it will end up on all of the others in the network.

The Philly Mesh keyserver, available at [gpg.phillymesh.net][4], is now part of several official server pools run by [sks-keyservers.net][5]. If you currently use the `gpg` utiliy, you may already be accessing it!

Of course, you can always use **gpg.phillymesh.net** specifically instead of via a server pool. The server has unencrypted HKP available on ports 80 and 11371, and encrypted HKPS available on ports 443 and 11372.

Additionally, this keyserver is available with HKP access over Hyperboria at the address **h.gpg.phillymesh.net**, and over the Tor network at the address **phillygoh7mkcb44.onion**. HKPS is not necessary over these networks as they are already end-to-end encrypted.

Here are some examples of how to access the keyserver:

```
# Clearnet access over HKP (IPv4/IPv6)
$  gpg --keyserver gpg.phillymesh.net --recv-keys 3A3CA65A

# Clearnet access over encrypted HKPS (IPv4/IPv6)
# Note, you may need gnupg-curl, not just gnupg
# Do: sudo apt-get install gnupg-curl
$  gpg --keyserver 'hkps://gpg.phillymesh.net' --recv-keys 3A3CA65A

# Hyperboria access over HKP
$  gpg --keyserver h.gpg.phillymesh.net --recv-keys 3A3CA65A

# Tor access over HKP
$  gpg --keyserver phillygoh7mkcb44.onion --recv-keys 3A3CA65A
```

 [1]: https://gpg.phillymesh.net/
 [2]: https://bitbucket.org/skskeyserver/sks-keyserver/wiki/Home
 [3]: https://www.gnupg.org/
 [4]: https://gpg.phillymesh.net
 [5]: https://sks-keyservers.net/status/ks-status.php?server=gpg.phillymesh.net