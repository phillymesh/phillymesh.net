---
title: Getting Started with Meshtastic in Philly
author: Emily Boda
type: post
date: 2025-06-16
url: /2025/06/16/getting-started/
categories:
  - Philly Mesh
tags:
  - meshtastic

---

So you're interested in getting started with Meshtastic and you live in or around Philly. There are plenty of resources online to help you get started, but this article will walk you through some things that are specific to our area.

## Local Online Meshtastic Communities

[Phillymesh.net](phillymesh.net) has been around forever, focused on Mesh networks in Philly, but has recently been revived as a hub for Meshtastic enthusiasts in the area. We generally congregate in our [Philly Radio & Meshtastic (PRM) Discord](https://discord.gg/MWWbAkRR9v) server. If you have any questions or want to get connected with other users, please join!

The official Meshtastic Discord has a [PA/Delaware Valley channel](https://discord.com/channels/867578229534359593/1280671409995255809). It has mostly been superseded by the above PRM Discord, but is still used infrequently by people in Central-Eastern PA. Depending on how far west your suburb lies, you may find some local friends in that channel.

If you're south of Philly, you may be interested in the [Delaware Meshtastic Facebook group](https://www.facebook.com/share/g/15fKQpacWR/?mibextid=wwXIfr). The Philly mesh gets connected to nodes in Delaware about once a month through either weird weather propagation or node flyovers, so we're familiar with them.

## Local Meshtastic Events

The wonderful hacker and solar punk bookstore Iffy Books has regular [Meshtastic 101 events](https://iffybooks.net/series/%F0%9F%93%A1-meshtastic-101/) that are great for beginner and intermediate Meshtastic users.

A few times a year there are also Meshtastic meetups or events hosted by groups like [DC215](https://dc215.org/) or others. These events are usually announced in the #meetups channel of the PRM Discord. We make an effort to announce meetups in advance over the mesh as well.

## Buying Locally

Iffy Books sells Heltec V3s (and maybe other hardware, too) for a reasonably low price. They generally include a basic case and an antenna, and if you buy them during a Meshtastic 101 event they also include a personal "getting started" session from Steve!

It is not uncommon for new Meshtastic users to be unsure if they haven't set up their device correctly, or if there just aren't any nodes nearby. By setting up your device up at Iffy you can guarantee you'll be within range of other nodes, and skip that part of the troubleshooting process.

## Where do I start?

First read the [Meshtastic.org Getting Started](https://meshtastic.org/docs/getting-started/) docs. This will always be up-to-date and have the most accurate information. Then come back here and read our take on how to getting started with local flair.

### First step: a window node

For your very first node, I recommend the cheapest possible hardware. This is usually a Heltec V3 (see the "Buying Locally" section!). Around here these are the most popular devices by far, making up almost 30% of all devices on the Philly Mesh\*.

Tape it up in the highest window you have and plug it in to a wall outlet. For best results, make sure your antenna is vertical. Leave it there for several hours and see what kind of range you're getting. Not seeing any nodes? Try a window facing in a different direction. Remember, Meshtastic is a mesh! You only need to reach one other node on the mesh to see the whole mesh!

#### Where should I point my node?

Philly's Center City is saturated with very high nodes. If you have line of sight to any of the tall buildings in Center City, you'll likely be able to connect to the larger Philly mesh. If you're unsure if your node is working properly, bringing it to Iffy Books is a great option. There is always a node there that you should be able to interface with, and if your hardware is faulty they have devices, antennas, and maybe some connectors on hand for purchase.

Below are some more specific of antennas to target if you can't get line of sight to Center City. These recommendations are from June 2025 and may or may not be valid after that date.

| Neighborhood  | High Antenna Locations           |
| ------------- | -------------------------------- |
| Center City   | Comcast Technology Center (PM01) |
| Rittenhouse   | 17th and Lombard (SDRH)          |
| South Philly  | 12th and Shunk (JPF)             |
| West Philly   | no antennas here                 |
| Manayunk      | no antennas here                 |
| Port Richmond | no antennas here                 |
| North Philly  | no antennas here                 |

_If you have access to the roof of any tall buildings in the neighborhoods listed above with no antennas, PRM would love to collaborate with you on getting a rooftop node set up!_

### Second step: a mobile node

Once you've experienced the thrill of connecting to a few nodes, you may find that unless you live in a studio, your phone's Bluetooth won't always reach the node and you'll miss the messages from the mesh in real time.

Your next purchase should be a battery powered mobile node. There are lots of DIY versions with a 3D printed case and a battery that use Heltec V3s, however the Heltec V3s (and other ESP32-based nodes) use a lot of power and will die quickly. Mobile/handheld nodes also generally don't get as good range as a stationary node. If it's in your pocket, the antenna will need to be smaller and it won't always be in the optimal orientation. For best results, you'll want to keep your stationary window node in place and use it as a relay to receive messages from the rest of the mesh on your pocket device.

If you want a pocket node that "just works", try a Seeed Studio T1000-e. These are newer devices, but have quickly been gaining popularity, making up almost 10% of devices in Philly\*. The battery on these generally lasts between 2-4 days. They're also more subtle than a DIY device with an antenna poking out, so you can pretty much take them anywhere. On the Seeed Studio website they're branded as "trackers" so you can describe them as "open source air tags" to any curious museum or stadium security guards.

If you want to DIY a pocket node, I recommend a nRF-based device. These have great battery life compared to the ESP32-based nodes. The RAK4631 is a great option; these make up around 20% of the devices in Philly\*.

You may also want to upgrade the antenna on your window node at this point. For a window node, you don't need to spend a lot, you just need to buy a node from a reputable source. Check out the [Meshtastic antenna reports](https://github.com/meshtastic/antenna-reports) page for recommended brands. In Philly we have found that you don't need a high gain (high dBi value) antenna in your window or on the roof of your townhouse, and in fact a high gain antenna might actually perform worse in our urban environment.

#### Should I change my window node's role to a Router?

NO! Keep your window node as the default role: Client. It might seem like Router would make sense, however that role was designed for nodes that are in extremely advantageous locations and by switching your node to that role you might actually be hurting the performance of the mesh. If you think you might have a good location for a router, bounce your ideas against others by engaging with the rest of the mesh community. Unnecessary Router devices are generally seen as a nuisance. Learn more about the Meshtastic Roles [here](https://meshtastic.org/blog/choosing-the-right-device-role/).

You may want to change the role of your pocket node to Client Mute. Since your pocket node likely doesn't have a lot of range and won't be bridging any new connections on the mesh (just interfacing with whatever is the closest high-up node) you can change your node to a role that won't unnecessarily repeat messages and clog up the mesh. However, with only two nodes on a large mesh you likely won't make any meaningful detrimental impact by leaving both of your clients in the Client role.

### Third step: a roof node

After you've mastered the experience of operating a window node and a mobile node, you're likely up for a new challenge. For most people, this is a rooftop node!

At minimum, this node must be waterproof. In most cases this will also need to be solar powered. It's much easier to convince a friend, landlord, or the maintenance manager at work to let you drop a node on their roof if you tell them it won't require any human intervention or external power.

You'll need to consider:

- **Mounting**: make sure it won't fly away in a hurricane.
- **Waterproofing**: even if it's completely sealed, you may still want a weep valve since Philly is a very humid environment.
- **Device management**: make sure you can remotely administer the device if you're not able to get your phone near it to connect via Bluetooth. More on that [here](https://meshtastic.org/docs/configuration/remote-admin/).
- **Testing**: make sure you test this on the ground for a few weeks before mounting it somewhere that's difficult to reach.
- **Updating**: this will be difficult without connecting your device to a computer. Technically nRF nodes can be updated over Bluetooth, however this method isn't very reliable and a failure can result in a device that is bricked until you can connect it to a computer again.

Check out the article on this site on [a Medium Priced Solar Node](https://phillymesh.net/2025/05/14/medium-priced-solar-node/) for one example and lessons learned making a solar node in Philly.

AustinMesh.org also has a great article on [Lessons Learned Building Solar Nodes](https://www.austinmesh.org/devices/#solar) in their area. They have a lot more experience than we at PhillyMesh.org.

#### Placement

As you might have gathered from looking at the map in the Meshtastic app, there are many high nodes in Center City. The PRM community is actively trying to expand the mesh's reach to other neighborhoods. We have lots of knowledge and even some nodes ready to deploy, but we're lacking connections to people who have access to the few tall buildings that exist in neighborhoods like West Philly, Manayunk, the Stadium District/Navy Yard, Port Richmond, Bridesburg, North Philly, Camden, etc. If you have any connections, please let us know by joining our discord or sending an email to hello@phillymesh.net. We'd love to help get better mesh coverage in wider areas in Philadelphia.

## Local Bots/Automated Announcements

### heltec.sdr.lol (SDRH)

SDRH sends out an automated multi-part message over the mesh every morning with the day's weather forecast and any weather alerts. Other Meshtastic users often reply stating where in the city they received the messages and which messages they received. This is a fun way to make sure we have Meshtastic traffic every day.

### Phillymesh.net-08 (PM08)

PM08 records information about the mesh and posts about it in the PRM Discord. The bot sends out a daily summary of how many new nodes were seen on the mesh in the #philly-node-bot channel on the PRM Discord, and once a week it sends out a summary of how many devices were seen on the mesh that week. It also sends out a graph of what types of devices were seen.

## Footnotes

An \* indicates that this statistics is based on nodes seen by PM08 during one week in June 2025. The reference chart is here:

![Chart showing what hardware is popular in Philly](/images/uploads/2025-06-16-getting-started/hardware_chart_edited.png)
