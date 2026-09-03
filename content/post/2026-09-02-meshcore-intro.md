---
title: MeshCore Intro
author: Emily Boda
type: post
date: 2026-09-02T00:00:01+00:00
url: /2026/09/02/meshcore-intro/
categories:
  - Philly Mesh
tags:
  - meshtastic
#cspell:ignore Meshtastic meshcore RemoteTerm ops div opsdiv
---

# MeshCore Settings

*These are the settings we're recommending for MeshCore 500. They are FCC-compliant and avoid the heaviest ISM band interference that we found during our testing in the Philadelphia area. Please make sure your MeshCore node is updated to the latest firmware before using these settings!*

- Frequency: `902.250 MHz`
- Bandwidth: `500 kHz`
- Spreading Factor: `11`
- Coding Rate: `4/5` (some apps may just say `5`)
- Path Hash Mode: `1` (2-byte mode, some apps list this setting as `1-2 byte`)

# What you need to know about MeshCore coming from Meshtastic

## Bluetooth Companion Node or Repeater

In Meshtastic most devices are configured as “client”. The network is designed so that every node can not only send messages but also repeat messages sent to them for others to hear. In order to reduce traffic on the network, it was recommended that nodes that are carried with you, ones that you don’t expect to be bridging gaps in the mesh all by themselves, be configured as “client_mute”. These nodes don’t repeat messages, they’re only used to send messages.

In MeshCore that concept is built into the beginning. When flashing a node you have to choose whether it will be a “Bluetooth Companion” node (equivalent to client_mute) or a “Repeater” (client). Repeaters can’t be connected to with Bluetooth, so if you only have one node you’ll want it to be a Bluetooth Companion node. If you live close enough that your Bluetooth Companion can reach someone else’s Repeater node, you won’t need your own. But you may still want to invest in a Repeater node.

Since you can’t connect to a Repeater via Bluetooth, Repeaters must be administered from a Bluetooth Companion node or via USB. In the initial set-up for a Repeater you’ll be prompted to set an admin password. Leaving this field blank will result in anyone being able to change settings on your Repeater. The guest password setting is only for restricting other people from seeing read-only telemetry data about your Repeater. You can feel free to leave this blank.

## Encryption

Just as with Meshtastic, all MeshCore traffic is encrypted. Just as with Meshtastic, there’s just a default “public” channel with a known key baked in. 

## Chats and Channels

You can make a private channel in MeshCore just like you can in Meshtastic. MeshCore only requires that you know the key to join it, whereas in Meshtastic you need the correct combination of the name and private key.

MeshCore also introduces a feature called “Hashtag channels”. These are joinable by name-only (aka no key/password), for example: “#prm”. These are used much more heavily than private channels are in Meshtastic, since they’re easier to share and join. Add some common terms like “#philly”, “#bot”, “#weather”, or “#test” to see them.

## Announcements

On Meshtastic your node would announce itself periodically and your node database would fill over the course of a day. On MeshCore, only the repeaters announce themselves. You can force searching for repeaters by using a “Scan for Repeaters” tool in most MeshCore apps.

You can force your node to advertise itself across the MeshCore network by using the “Send Flood Advert” feature in most MeshCore apps.

## Reach

The maximum Hop Limit on Meshtastic is seven, and by default it’s set to three. In MeshCore, the default Hop Limit is 64, meaning your messages can travel much further than with Meshtastic. It is recommended to use the Path Hash Mode of “1”, aka a 2-byte path hash, which has the downside of limiting your hops to 32 instead of 64. The upside is that your repeater ID in flood path / loop-detects is encoded with 65,536 possible variations instead of only 256, making for a much more stable overall mesh. This setting is commonly used in MeshCore-default meshes as well.