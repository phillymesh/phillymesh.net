---
title: Installing Yggdrasil – A Toy Implementation of an Encrypted IPv6 Network
author: Mike Dank (Famicoman)
type: post
date: 2018-01-05T14:46:04+00:00
url: /2018/01/05/installing-yggdrasil-a-toy-implementation-of-an-ecrypted-ipv6-network/
categories:
  - Tutorial
tags:
  - cjdns
  - go
  - ipv7
  - Yggdrasil

---
_**2018-08-29 Update: This tutorial is now very out of date. The Yggdrasil team now maintains great installation guides [here][1].**_

At Philly Mesh, we like to play around with pieces of technology that aren't directly related to our core software stack. One such piece of software is [Yggdrasil][2], an encrypted IPv6 networking implementation developed by [Arceliar][3]. Yggdrasil borrows many ideas from [cjdns][4], but was primarily written to test a new routing scheme developed by Arceliar. While it is not production-ready software, Yggdrasil is an interesting foray into encrypted networking and fun to experiment with.

For this installation guide, we assume a Debian Stretch (or similar) Linux system with a non-root, sudo user.

First, we need to make sure we have a recent version of `go`. We can check our version using the following command:

```
$ go --version
go version go1.9.2 linux/amd64
```

Yggdrasil is built with Go 1.9. At the time of writing, Debian Stretch only comes with Go 1.3. If you need to install a more recent version of Go, you can do so manually. Below is an example installing Go 1.9.2 for the amd64 architecture using a download link from https://golang.org/dl/:

```
$ sudo apt-get remove golang
$ cd /usr/local
$ sudo wget https://redirector.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz
$ sudo tar -xzf go1.9.2.linux-amd64.tar.gz
$ sudo ln -s /usr/local/go/bin/go /usr/local/bin/go
```

Now we will set up some environment variables to use Go:

```
$ mkdir ~/go
$ export GOROOT=/usr/local/go
```

Now we are ready to install Yggdrasil:

```
$ cd ~
$ git clone https://github.com/Arceliar/yggdrasil-go.git
$ cd yggdrasil-go/
$ ./build
```

If all goes well, Yggdrasil will have built successfully with no errors. Now we are ready to generate a config file:

```
$ ./yggdrasil --genconf > conf.json
```

The config file is pretty basic and allows for some customization:

```
$ cat conf.json
{
  "Listen": "[::]:0",
  "Peers": [],
  "BoxPub": "46d18cbcfa0d510fcd226f323efe279525c50eb15db925d4879ee675b99b0724",
  "BoxPriv": "727213ecb3caf601ee49596fa77469674bed177f10d8607ee76ec1f35e942310",
  "SigPub": "08565493e805e905dbcc22cdaa7e60bd6cb6fc1df21d1b807b46f6285f8b86fd",
  "SigPriv": "4173f91e08ab2b6f7c5ae96cf9d61f7ac30b36be7a5eff298e00e0d08f6f5c9608565493e805e905dbcc22cdaa7e60bd6cb6fc1df21d1b807b46f6285f8b86fd",
  "Multicast": true
}
```

If you want Yggdrasil to listen on a static port, you can change the `Listen` attribute to use an IP and/or port of your choosing like `"12.34.57.78:1234"`. You can add entries to the `Peers` attribute by listing them as strings (IP:PORT) in the array (comma-separated). The `Multicast` attribute is currently set to `true`, but you could set this to `false` if you didn't want to auto-peer for some reason.

Here is a sample config that listens on port `1234` on all interfaces and connects to a peer at `12.34.57.78:1234`:

```
cat conf.json
{
  "Listen": "[::]:1234",
  "Peers": ["12.34.57.78:1234"],
  "BoxPub": "46d18cbcfa0d510fcd226f323efe279525c50eb15db925d4879ee675b99b0724",
  "BoxPriv": "727213ecb3caf601ee49596fa77469674bed177f10d8607ee76ec1f35e942310",
  "SigPub": "08565493e805e905dbcc22cdaa7e60bd6cb6fc1df21d1b807b46f6285f8b86fd",
  "SigPriv": "4173f91e08ab2b6f7c5ae96cf9d61f7ac30b36be7a5eff298e00e0d08f6f5c9608565493e805e905dbcc22cdaa7e60bd6cb6fc1df21d1b807b46f6285f8b86fd",
  "Multicast": true
}
```

Now, we can start Yggdrasil in the background:

```
sudo ./yggdrasil --useconf < conf.json &
```

You should now have a `tun` interface up for your Yggdrasil node:

```
$ ip a 
43: tun1: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1280 qdisc pfifo_fast state UNKNOWN group default qlen 500
    link/none
    inet6 fd00:4645:d147:7c16:98f2:20ea:d0ba:7174/8 scope global
       valid_lft forever preferred_lft forever
```

Now, you can ping other Yggdrasil nodes on the network:

```
$ ping6 -c4 fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e
PING fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e(fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e) 56 data bytes
64 bytes from fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e: icmp_seq=1 ttl=64 time=14.4 ms
64 bytes from fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e: icmp_seq=2 ttl=64 time=12.6 ms
64 bytes from fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e: icmp_seq=3 ttl=64 time=15.1 ms
64 bytes from fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e: icmp_seq=4 ttl=64 time=12.9 ms

--- fd1f:dd73:7cdb:773b:a924:7ec0:800b:221e ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 12.673/13.783/15.105/1.017 ms
```

Further documentation for Yggdrasil is available [here][5], and a whitepaper draft is available [here][6].

 [1]: https://yggdrasil-network.github.io/platforms.html
 [2]: https://github.com/Arceliar/yggdrasil-go
 [3]: https://github.com/Arceliar
 [4]: https://github.com/cjdelisle/cjdns
 [5]: https://github.com/Arceliar/yggdrasil-go/blob/master/doc/README.md
 [6]: https://github.com/Arceliar/yggdrasil-go/blob/master/doc/Whitepaper.md