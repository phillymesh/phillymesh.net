---
title: Just Meshing Around
author: Mike Dank (Famicoman)
type: post
date: 2014-01-28T22:09:27+00:00
url: /2014/01/28/just-meshing-around/
draft: true
categories:
  - Philly Mesh
tags:
  - 802.11
  - 802.15.4
  - beaglebone
  - cantenna
  - cjdns
  - dd-wrt
  - fonera
  - hyperboria
  - linksys wrt54g
  - openwrt
  - pogoplug
  - raspberry pi
  - seattle wireless
  - tomato
  - tp-link
  - zigbee
#cspell:ignore fonera cantenna cantennas Linksys Seattleites
---
The first time I remember hearing about mesh networks was sometime around 2005. Through rigorous searches, I had finally tracked down a complete run of Seattle Wireless TV, a proto-podcast that ran from July of 2003 until June of 2004. This hunt was undergone for my own personal interests; I was and am something of an online-video-series junkie, and I have since [posted all the episodes for download on Archive.org](https://archive.org/details/seattlewirelesstv) where they will be preserved for anyone to watch for years to come. The topics of these episodes varied from interviews with operators, to wardriving tips, and even antenna creation. Pretty popular topics back then, but now the show serves as a fantastic time capsule from a technologically-simpler time. Even ten years ago, “getting into” wireless networking seemed radically different. Everyone tried their hand at wardriving, embraced 802.11g, and wired cantennas to their Orinoco cards. [Here](http://vilos.com/new_mast/) is a prime example of the times — some Seattleites setting up their own mesh network in 2002. Essentially, Wi-Fi was king and you could have it in your own home. I didn’t end up jumping into the mix until years later. I got my first laptop in 2006 and even then I usually embraced a wired connection. Watching these video shows was my own little outlet into what the cool kids were doing. It wasn’t until a little later that I decided it was time to play.

In 2007, I received a La Fonera router from Fon courtesy of a free giveaway (I actually managed to snag one on the very last day they offered the promotion). I thought it might be cool to join their Wi-Fi collective, but I was much more interested in what else I could do with the device. The day it came in the mail I promptly researched what others were doing with it and joined in on the popular act of flashing [dd-wrt](http://www.dd-wrt.com/site/index) firmware onto the little device to get some expanded functionality. This process was harder than I expected and my lack of knowledge on the subject at the time showed. After many frustrating hours--flipping back and forth between telnet, TFTP, and IRC chatter--I had a fully functioning dd-wrt router of my very own. While this was a feat all in itself, it went on to inspire me to see what I could do with other routers. I soon grew a little collection of second-hand Linksys WRT54G routers to tinker with and take up space on my work bench. I tried out different firmwares like [OpenWRT](https://openwrt.org/) and [Tomato](http://www.polarcloud.com/tomato) and always tried to keep something new running on a separate network for me to play with so I didn’t accidentally bring down the whole house’s internet access with a bad flash or misconfiguration.

Years later, I ended up working with wireless technology in a professional capacity. However, I was no longer handling everyone’s favorite suite of 802.11 protocols but the new-fangled 802.15.4 for low-rate wireless personal area networks. I focused on the ZigBee specification and its derivatives, which were and are a popular choice for technologies like home automation systems, wireless switches, electrical meters, etc. I spent months toying with the technology, working to understand the encryption, capture and dissect the traffic, and create and transmit my own custom packets. While the technology itself was enough to hold my interest, I felt a draw toward the technology’s use of wireless mesh networking to create expansive networks.

This wasn’t my first foray into the world of mesh networking per se. Prior to my work with ZigBee, I focused on meshing briefly to combat network interruption when creating the topology for a hobby-run IRC network I was administrating. This was, however, my first time applying mesh ideas wirelessly. I quickly learned the ins and outs of the Zigbee specification and the overarching 802.15.4 standard, but I couldn’t help thinking about how these technologies applied to Wi-Fi and how much fun an 802.11 mesh network would be.

Soon, I discovered the existence of Philly Mesh, a Philadelphia-based mesh network in its infancy that connected with [Hyperboria](http://hyperboria.net): a global decentralized network of nodes running [cjdns](http://cjdns.info). I made a few posts to its subreddit, added my potential node to the map, and ordered some TP-Link routers to play with. While the group seemed to be gathering support, it ultimately (and much to my dismay) stagnated. Expansion stopped and communication dwindled. People disappeared and services started to fall apart. Over the next year I tried to work through getting my own node up but hit several setbacks. I bricked a router, ran into configuration problems, suffered from outdated or missing documentation, and then bricked *another* router. Eventually, after a seemingly endless process of torment and discovery, I connected to the network using a Raspberry Pi. My first cjdns node was up.

After this, I made a push to revive the Philly Mesh project. I constructed a new website, revived some of the services, and started my push for finding community involvement. Though it stands to be a slow process, things are coming together and people are coming forward. Whether or not we will have a thriving mesh network in the future is unknown, but the journey in this case interests me just as much as the destination.

As of now, I’m embracing wireless mesh as a hobby. I still have a pile of routers to play with and test firmware on, and am getting new hardware every so often. As for the bricked TP-Links, I’ve picked up USB/TTL adapter in an attempt to correct my wrongdoings and get cjdns set up properly. I’m also constantly playing with my settings on the Raspberry Pi installation as I have to firewall things off, assure reliability for an application crash, and generally make sure things are running smoothly. Additionally, I’ve been toying around with different technologies to set up an access point through the Raspberry Pi such as a USB/Ethernet adapter to bridge a connection between an old router and the Pi, and a USB dongle to create an access point in a more direct model. Aside from the Raspberry Pi and assorted routers, I’m also interested in getting cjdns installed and configured on plug computers like the Pogoplug and single board computers like the BeagleBone Black.

Where will all of this take us? Hopefully this is a stepping stone on the way to building a thriving local mesh, but the future is unknown. I’d love to get some nodes set up wirelessly within the city, but I’m only one person out in the suburbs tinkering away. While I’m sitting here learning about setting up devices, I only hope to share what I find with others who might benefit from having someone else carve out an initial path. I, by myself, can work to build a local mesh but it wouldn’t be nearly as robust or expansive as if I worked within a team sharing ideas and experience.

If you’re reading this, you have the interest. You may not have the know-how, the money for high-tech equipment, or a location nearby other potential operators, but you have the desire. If there’s anything that I’ve learned throughout my ongoing mesh adventure, it’s that good things take time and nothing happens overnight.

Tomorrow, we can work to build a strong mesh for our city. As for today, why don’t we get started?
