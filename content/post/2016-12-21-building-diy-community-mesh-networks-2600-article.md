---
title: Building DIY Community Mesh Networks (2600 Article)
author: Mike Dank (Famicoman)
type: post
date: 2016-12-21T23:08:09+00:00
url: /2016/12/21/building-diy-community-mesh-networks-2600-article/
categories:
  - Philly Mesh
  - Tutorial
tags:
  - 2600
  - cjdns
  - hyperboria
  - mesh
  - openwrt
#cspell:ignore Guifi
---
_Now that the article has been printed in [2600 magazine, Volume 33, Issue 3](https://www.amazon.com/2600-Magazine-Hacker-Quarterly-ebook/dp/B01M1NJI3U/2600magazi-20) (2016-10-10), I’m able to republish it on the web. The article below is my submission to 2600 with some slight formatting changes for hyperlinks._

# Building DIY Community Mesh Networks  
By Mike Dank  
Famicoman@gmail.com  

Today, we are faced with issues regarding our access to the Internet, as well as our freedoms on it. As governmental bodies fight to gain more control and influence over the flow of our information, some choose to look for alternatives to the traditional Internet and build their own networks as they see fit. These community networks can pop up in dense urban areas, remote locations with limited Internet access, and everywhere in between.Whether you are politically fueled by issues of net neutrality, privacy, and censorship, fed up with an oligarchy of Internet service providers, or just like tinkering with hardware, a wireless mesh network (or “meshnet”) can be an invaluable project to work on. Numerous groups and organizations have popped up all over the world, creating robust mesh networks and refining the technologies that make them possible. While the overall task of building a wireless mesh network for your community may seem daunting, it is easy to get started and scale up as needed.

## What Are Mesh Networks?

Think about your existing home network. Most people have a centralized router with several devices hooked up to it. Each device communicates directly with the central router and relies on it to relay traffic to and from other devices. This is called a hub/spoke topology, and you’ll notice that it has a single point of failure. With a mesh topology, many different routers (referred to as nodes) relay traffic to one another on the path to the target machine. Nodes in this network can be set up ad-hoc; if one node goes down, traffic can easily be rerouted to another node. If new nodes come online, they can be seamlessly integrated into the network. In the wireless space, distant users can be connected together with the help of directional antennas and share network access. As more nodes join a network, service only improves as various gaps are filled in and connections are made more redundant. Ultimately, a network is created that is both decentralized and distributed. There is no single point of failure, making it difficult to shut down.

When creating mesh networks, we are mostly concerned with how devices are routing to and linking with one another. This means that most services you are used to running like HTTP or IRC daemons should be able to operate without a hitch. Additionally, you are presented with the choice of whether or not to create a darknet (completely separated from the Internet) or host exit nodes to allow your traffic out of the mesh.

## Existing Community Mesh Networking Projects

One of the most well-known grassroots community mesh networks is [Freifunk](https://freifunk.net), based out of Germany, encompassing over 150 local communities with over 25,000 access points. [Guifi.net](https://guifi.net) based in Spain, boasts over 27,000 nodes spanning over 36,000 km. In North America we see projects like [Hyperboria](http://hyperboria.net) which connect smaller mesh networking communities together such as [Seattle Meshnet](https://www.seattlemesh.net), [NYC Mesh](https://nycmesh.net), and[Toronto Mesh](https://tomesh.net). We also see standalone projects like [PittMesh](http://www.pittmesh.net) in Pittsburgh, [WasabiNet](http://gowasabi.net) in St. Louis, and [People’s Open Network](https://sudoroom.org) in Oakland, California.

While each of these mesh networks may run different software and have a different base of users, they all serve an important purpose within their communities. Additionally, many of these networks consistently give back to the greater mesh networking community and choose to share information about their hardware configurations, software stacks, and infrastructure. This only benefits those who want to start their own networks or improve existing ones.

## Picking Your Hardware & OS

When I was first starting out with [Philly Mesh](http://mesh.philly2600.net), I was faced with the issue of acquiring hardware on a shoestring budget. Many will tell you that the best hardware is low-power computers with dedicated wireless cards. This however can incur a cost of several hundred dollars per node. Alternatively, many groups make use of SOHO routers purchased off-the-shelf, flashed with custom firmware. The most popular firmware used here is OpenWRT, an open source alternative that supports a large majority of consumer routers. If you have a relatively modern router in your house, there is a good chance it is already supported (if you are buying specifically for meshing, consider consulting [OpenWRT’s wiki](https://wiki.openwrt.org) for compatibility. Based on Linux, OpenWRT really shines with its packaging system, allowing you to easily install and configure packages of networking software across several routers regardless of most hardware differences between nodes. With only a few commands, you can have mesh packages installed and ready for production.

Other groups are turning towards credit-card-sized computers like the BeagleBone Black and Raspberry Pi, using multiple USB WiFi dongles to perform over-the-air communication. Here, we have many more options for an operating system as many prefer to use a flavor of Linux or BSD, though most of these platforms also have OpenWRT support.

There are no specific wrong answers here when choosing your hardware. Some platforms may be better suited to different scenarios. For the sake of getting started, spec’ing out some inexpensive routers (aim for something with at least two radios, 8MB of flash) or repurposing some Raspberry Pis is perfectly adequate and will help you learn the fundamental concepts of mesh networking as well develop a working prototype that can be upgraded or expanded as needed (hooray for portable configurations). Make sure you consider options like indoor vs outdoor use, 2.4 GHz vs. 5 GHz band, etc.

## Meshing Software

You have OpenWRT or another operating system installed, but how can you mesh your router with others wirelessly? Now, you have to pick out some software that will allow you to facilitate a mesh network. The first packages that you need to look at are for what is called the data link layer of the OSI model of computer networking (or OSI layer 2). Software here establishes the protocol that controls how your packets get transferred from node A to node B. Common software in this space is [batman-adv](https://www.open-mesh.org/projects/batman-adv/wiki) (not to be confused with the layer 3 [B.A.T.M.A.N. daemon](https://www.open-mesh.org/projects/batmand/wiki)), and [open80211s](https://www.open80211s.org/), which are available for most operating systems. Each of these pieces of software have their own strengths and weaknesses; it might be best to install each package on a pair of routers and see which one works best for you. There is currently a lot of praise for batman-adv as it has been integrated into the mainline Linux tree and was developed by Freifunk to use within their own mesh network.

Revisiting the OSI model again, you will also need some software to work at the network layer (OSI layer 3). This will control your IP routing, allowing for each node to compute where to send traffic next on its forwarding path to the final destination on the network. There are many software packages here such as [OLSR](http://www.olsr.org/mediawiki/index.php/Main_Page) (Optimized Link State Routing), B.A.T.M.A.N (Better Approach To Mobile Adhoc Networking), [Babel](https://www.irif.fr/~jch//software/babel/), [BMX6](https://github.com/bmx-routing/bmx6), and [CJDNS](https://github.com/cjdelisle/cjdns) (Caleb James Delisle’s Networking Suite). Each of these addresses the task in its own way, making use of a proactive, reactive, or hybrid approach to determine routing. B.A.T.M.A.N. and OLSR are popular here, both developed by Freifunk. Though B.A.T.M.A.N. was designed as a replacement for OLSR, each is actively used and OLSR is highly utilized in the Commotion mesh networking firmware (a router firmware based off of OpenWRT).

For my needs, I settled on CJDNS which boasts IPv6 addressing, secure communications, and some flexibility in auto-peering with local nodes. Additionally, CJDNS is agnostic to how its host connects to peers. It will work whether you want to connect to another access point over batman-adv, or even tunnel over the existing Internet (similar to Tor or a VPN)! This is useful for mesh networks starting out that may have nodes too distant to connect wirelessly until more nodes are set up in-between. This gives you a chance to lay infrastructure sooner rather than later, and simply swap-out for wireless linking when possible. You also get the interesting ability to link multiple meshnets together that may not be geographically close.

## Putting It Together

At this point, you should have at least one node (though you will probably want two for testing) running the software stack that you have settled on. With wireless communications, you can generally say that the higher you place the antenna, the better. Many community mesh groups try to establish nodes on top of buildings with roof access, making use of both directional antennas (to connect to distant nodes within the line of sight) as well as omnidirectional antennas to connect to nearby nodes and/or peers. By arranging several distant nodes to connect to one another via line of sight, you can establish a networking backbone for your meshnet that other nodes in the city can easily connect to and branch off of.

## Gathering Interest

Mesh networks can only grow so much when you are working by yourself. At some point, you are going to need help finding homes for more nodes and expanding the network. You can easily start with friends and family – see if they are willing to host a node (they probably wouldn’t even notice it after a while). Otherwise, you will want to meet with like-minded people who can help configure hardware and software, or plan out the infrastructure. You can start small online by setting up a website with a mission statement and making a post or two on Reddit ([/r/darknetplan](https://www.reddit.com/r/darknetplan/) in particular) or Twitter. Do you have hackerspaces in your area? Linux or amateur radio groups? A 2600 meeting you frequent? All of these are great resources to meet people face-to-face and grow your network one node at a time.

## Conclusion

Starting a mesh network is easier than many think, and is an incredible way to learn about networking, Linux, micro platforms, embedded systems, and wireless communication. With only a few off-the-shelf devices, one can get their own working network set up and scale it to accommodate more users. Community-run mesh networks not only aid in helping those fed up with or persecuted by traditional network providers, but also those who want to construct, experiment, and tinker. With mesh networks, we can build our own future of communication and free the network for everyone.