---
title: State of the Network
author: Mike Dank (Famicoman)
type: page
date: 2017-11-24T16:01:53+00:00
draft: true
#cspell:ignore FOSSCON
---
*This is an organic page that reflects the current state of Philly Mesh and the growing network it maintains. This page is subject to change as the project advances. Last updated: 2020-04-29.*

### Network State {#networkstate}

_Philly Mesh_ is working to build a robust mesh network using easy-to-deploy, off-the-shelf hardware that is commonly purchased as for wireless routing in homes and businesses. **We currently have no infrastructure active, or concrete plans for building up the network. We are looking for people to try things out, see what works, and and collaborate with other enthusiasts to set nodes up.**

&#8212;

Many off-the-shelf these devices are capable of running a custom, free firmware package known as [OpenWRT][1] that can open up the hardware to utilize software not (usually) supported by manufacturers. The OpenWRT project supports a myriad of devices; the wireless router in your home right now is even likely compatible!

Similar to how mesh networks like the popular [Freifunk][2] project in Germany operate, Philly Mesh has been considering using layer 2 meshing with [batman-adv][3], a mesh routing protocol primarily built for Linux-based operating system or layer 3 meshing with [bmx7][4]. The aforementioned Freifunk uses batman-adv and bmx6/bmx7 in addition to older protocols in the same family such as [OLSR][5]. Other similar mesh networking protocols like the [IEEE 802.11s][6] protocol amendment for wireless mesh networking may be used in specific cases for ad hoc network creation.

On top of the  mesh network, we may ultimately want to run something like [Yggdrasil][7], an early-stage implementation of a fully end-to-end encrypted IPv6 network. Yggdrasil handles routing and addressing through its own secure network implementation, in OSI layer 3, that will allow any IPv6-capable web service to be accessible to users of the network. Yggdrasil doesn't care what interface you run it on, and will create networks over wireless links, ethernet, fiber, and even the existing Internet, making it incredibly flexible for many types of deployments.

Many other localized mesh groups (or "meshlocals") are also working on networking solutions, and our ultimate goal is interoperability with other groups. While mesh networks are currently physically contained to certain geographic regions, we hope to see the distance between them shorten over time. One group we collaborate with extensively is [Toronto Mesh][8], though there are roughly a dozen other groups we are in regular contact with.

Within Philadelphia and the surrounding area, we are recruiting as many people as possible to come up with a network plan and ultimately set up nodes they can run perpetually at their residence, place of business, or community centers. In these early days of creating a physical network, those who want to join might not be able to find other node operators physically close by. Don't let this be a deterrent! We can experiment with technologies like Yggdrasil, that allow you to tunnel your mesh traffic over your existing Internet connection and test out network creation while also cementing a location for other mesh enthusiasts in the greater Philadelphia area to easily connect to. Once two or more people running nodes are physically close enough to connect wirelessly, the Internet tunnel connection can be dropped in favor of wireless links (or added in addition to it, the choice is yours)! While we are called _Philly Mesh_, we don't discriminate geographically. We have members in the city, the suburbs, and surrounding states. Come say hi!

We are currently looking at ways to expand the network and make network access easier for an end user. This includes documenting our progress, getting custom firmware built and distributed, and making links between people where possible.

If any of this interests you, or you would like to learn more, [get in touch][9]!

### Next Steps {#nextsteps}

There are a lot of things that are being discussed or considered for improving the network. A sample of them are listed below, in no particular order.

  * Come up with a good plan! We need to decide on software, build firmware images, etc. It all starts here.
  * Grow the network. After we can easily create nodes and have a documented process, we need to get more people setting them up and keeping them up.
  * Make connecting to the network easier for less-technical enthusiasts.
  * Enhance community outreach! 
      * More people representing Philly Mesh at local groups like [PLUG][10], [Philly 2600][11], [Security Shell][12], and [Philly Sec][13]
      * Have ambassadors at local universities like Drexel (Are you a member of the [CyberDragons][14]?), Temple (Member of [TUSec][15]?), and UPenn (Member of [Penn for Privacy][16]?). Do you attend or work at one of these schools and have interest in organizing a group there?
      * Have a presence or give a presentation at a local event like [BSides Philly][17], [BSides Delaware][18], [FOSSCON][19], [PumpCon][20], or [CryptoParty][21].
      * Have ambassadors at local hackerspaces. Are you a member or organizer at [NextFab][22] or [Hive76][23]? Getting mesh nodes set up at these places would be huge.
  * Devise a wireless backbone. Do you like playing with powerful wireless radios and creating point-to-point links to buildings around the city? How about worrying about all the fun stuff like signal strength, line-of-sight obstruction, or grounding? Do you have access to a rooftop where you can run hardware?
  * Design the next generation of turn-key nodes. Let&#8217;s create packaged devices that are as easy to use as plugging in and turning on.
  * Standardize our egress traffic. We&#8217;d likely want to allow for Internet traffic to exit the mesh network, but it would be ideal to not depend on local ISPs to get those done. Do you know of or have connections to and IXPs (Internet Exchange Points) in the area? Maybe you operate a datacenter in the area and have bandwidth to spare?
  * Experiment with other mesh networking technologies. Maybe you&#8217;d like the experiment with [Hamnet][24], [AltheaMesh][25], or [Libremesh][26]. Not only is it good to approach mesh networking from other perspectives, but research here could help with interoperability down the road.

### Further Reading {#furtherreading}

As always, there is a lot you can do to learn more about mesh networking or networking in general. Here are a few selections:

  * [Building DIY Community Mesh Networks][27] &#8211; Read my primer on getting a community mesh network started.
  * [Networks.land][28] &#8211; Learn how the existing Internet works from the ground up.
  * [Homenet Howto][29] &#8211; A guide for understanding home networking, from basic topics through advanced.
  * [tomesh.101 Glossary][30] &#8211; Learn some of the common domain-specific language we use when describing mesh networks.

 [1]: https://openwrt.org/
 [2]: https://en.wikipedia.org/wiki/Freifunk
 [3]: https://www.open-mesh.org/projects/batman-adv/wiki
 [4]: https://github.com/bmx-routing/bmx7
 [5]: https://en.wikipedia.org/wiki/Optimized_Link_State_Routing_Protocol
 [6]: https://en.wikipedia.org/wiki/IEEE_802.11s
 [7]: https://yggdrasil-network.github.io/
 [8]: https://tomesh.net/
 [9]: https://phillymesh.net/contact/
 [10]: http://www.phillylinux.org/
 [11]: http://philly2600.net/
 [12]: https://twitter.com/SecShellPhilly?lang=en
 [13]: https://twitter.com/phillysec?lang=en
 [14]: http://drexel.edu/cybersecurity/education/cyberdragons/
 [15]: https://twitter.com/TUsecOrg
 [16]: https://twitter.com/PennforPrivacy
 [17]: https://www.bsidesphilly.org/
 [18]: http://www.bsidesdelaware.com/
 [19]: https://fosscon.us/
 [20]: http://pumpcon.org/
 [21]: https://www.cryptoparty.in/university_of_pennsylvania?s[]=philadelphia
 [22]: https://nextfab.com/
 [23]: https://www.hive76.org/
 [24]: http://www.broadband-hamnet.org/
 [25]: http://altheamesh.com/
 [26]: http://libremesh.org/
 [27]: https://phillymesh.net/2016/12/21/building-diy-community-mesh-networks-2600-article/
 [28]: http://networks.land/
 [29]: https://www.homenethowto.com/
 [30]: https://github.com/tomeshnet/tomesh.101/blob/master/glossary/glossary.md