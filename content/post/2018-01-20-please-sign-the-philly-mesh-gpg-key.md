---
title: Please Sign the Philly Mesh GPG Key!
author: Mike Dank (Famicoman)
type: post
date: 2018-01-21T00:01:22+00:00
url: /2018/01/20/please-sign-the-philly-mesh-gpg-key/
draft: true
categories:
  - Philly Mesh
  - Tutorial
tags:
  - gpg
  - keys
  - keyserver
  - openpgp
  - pgp
  - sign
  - sks
  - web of trust

---
Now that we have erected an [SKS keyserver][1], I invite everyone to sign the [Philly Mesh GPG key][2] to help verify our identity. There are many GPG/PGP applications out there, but below I will provide steps for the `gpg` utility available on many POSIX systems (Linux, Darwin, etc.). Ideally, with enough signatures, the Philly Mesh key has a higher probability of entering the [Web of Trust strong set][3], the largest collection of strongly-connected gpg keys.

## Receive the Philly Mesh Key

Before you can sign the Philly Mesh key, you will need to download it to your system via a keyserver. Here is an example using the SKS server pool:

```
$ gpg --keyserver pool.sks-keyservers.net --recv-keys 0x8f5b291d3a3ca65a
gpg: requesting key 3A3CA65A from hkp server pool.sks-keyservers.net
gpg: no ultimately trusted keys found
gpg: Total number processed: 1
gpg:               imported: 1
```

Now, you should be able to list the Philly Mesh key in your public keyring. Make sure that the key has not been revoked and is not expired:

```
$ gpg --list-keys 0x8f5b291d3a3ca65a
pub   4096R/3A3CA65A 2017-11-25 [expires: 2027-11-23]
uid                  Philly Mesh <phillymesh@protonmail.ch>
uid                  Philly Mesh <hello@phillymesh.net>
uid                  Mike Dank <mike@phillymesh.net>
sub   4096R/1744B74A 2017-11-25 [expires: 2027-11-23]
```

## Bootstrapping Trust

Before you sign the Philly Mesh key, you want to make sure that it is actually owned by Philly Mesh. For some people, this is as easy as asking me online somewhere or in person. For others, you might want to check [the verifications for Philly Mesh on Keybase][4] which shows that this key has been verified by the `phillymesh.net` domain. For those who want some instant verification that this key is associated with the domain `phillymesh.net`, you can query against a DNS record on the domain which holds the key's fingerprint.

First, let's see the fingerprint for the key you have just received:

```
$ gpg --fingerprint 0x8f5b291d3a3ca65a
pub   4096R/3A3CA65A 2017-11-25 [expires: 2027-11-23]
      Key fingerprint = C58B 0431 C815 F315 7310  0959 8F5B 291D 3A3C A65A
uid                  Philly Mesh <phillymesh@protonmail.ch>
uid                  Philly Mesh <hello@phillymesh.net>
uid                  Mike Dank <mike@phillymesh.net>
sub   4096R/1744B74A 2017-11-25 [expires: 2027-11-23]
```

Now, let's query against `fingerprint.phillymesh.net`, which pulls a live `TXT` record set up on the domain housing the trusted fingerprint:

```
$ dig +short -t txt fingerprint.phillymesh.net
"C58B 0431 C815 F315 7310  0959 8F5B 291D 3A3C A65A"
```

The fingerprint from the `gpg --fingerprint` command should match the result from the `dig` command. **If it doesn't match, don't trust the key**. Someone may be in control of the `phillymesh.net` domain and try to get you to trust their false key.

## Sign the Key

Now, you are ready to sign the Philly Mesh key. At this point, we assume that you have already [created a key of your own][5]. While receiving the key in the initial section above, we also assume you have made sure the key has not expired or been revoked.

Sign the Philly Mesh key with your own key, following the prompts as they come up. At the time of this writing there are 3 uids (email addresses) associated with this key (listed below in the command output). They can each safely be signed:

```
$ gpg --sign-key 0x8f5b291d3a3ca65a
gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: next trustdb check due at 2027-11-23
pub  4096R/3A3CA65A  created: 2017-11-25  expires: 2027-11-23  usage: SC
                     trust: ultimate      validity: ultimate
sub  4096R/1744B74A  created: 2017-11-25  expires: 2027-11-23  usage: E
[ultimate] (1). Philly Mesh <phillymesh@protonmail.ch>
[ultimate] (2)  Philly Mesh <hello@phillymesh.net>
[ultimate] (3)  Mike Dank <mike@phillymesh.net>

Really sign all user IDs? (y/N) y
```

After signing, send the key back to the keyserver so the signature is recorded:

```$ gpg --keyserver pool.sks-keyservers.net --send-key 0x8f5b291d3a3ca65a
gpg: sending key 3A3CA65A to hkp server pool.sks-keyservers.net
```

That's all it takes! Your signature will now be recorded and the record will update across all keyservers in the SKS pool. You can check that your signature has been recorded [here][2] (it might take a few minutes to populate).

{{< figure src="/images/uploads/2018/01/phillymesh_key_full_info_2.png" caption="The Philly Mesh key has been signed by [0x1619ae4d7cf2a8f7](https://gpg.phillymesh.net/pks/lookup?op=vindex&hash=on&fingerprint=on&search=0x1619AE4D7CF2A8F7)" link="/images/uploads/2018/01/phillymesh_key_full_info_2.png">}}

 [1]: https://phillymesh.net/2018/01/05/philly-mesh-openpgp-sks-keyserver-now-online/
 [2]: https://gpg.phillymesh.net/pks/lookup?search=0x8f5b291d3a3ca65a&fingerprint=on&hash=on&op=vindex
 [3]: https://en.wikipedia.org/wiki/Web_of_trust#Strong_set
 [4]: https://keybase.io/phillymesh
 [5]: https://help.ubuntu.com/community/GnuPrivacyGuardHowto