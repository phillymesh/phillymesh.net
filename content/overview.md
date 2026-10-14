---
title: Mesh Networking in Philadelphia
author: Emily Boda
type: post
date: 2026-10-13
url: /overview
categories:
  - Philly Mesh
tags:
  - meshtastic
#cspell:ignore meshtastic meshcore PhillyWisper MeshMapper
---

# Recent History

Since the Meshtastic project started in 2019, sending off-the-grid text messages with LoRa wireless technology has become an increasingly popular hobby all over the world. In the greater Philadelphia area alone, we have seen almost 500 independent nodes active on our networks in a single week. 

In recent years, the number of mesh networking projects has increased as MeshCore and several other variants of the same basic idea have emerged and seen wide adoption. This, as well as mesh networking hobbyists becoming more organized in the PhillyMesh group, has resulted in our networks becoming more efficient and farther-reaching than ever before.

PhillyMesh aims to support all free and open-source mesh networking projects by administering core "backbone" communication nodes in locations that increase individuals' abilities to communicate with each other. We currently focus specifically on the MeshCore and Meshtastic projects.

# What are Meshtastic and MeshCore?

The Meshtastic and MeshCore projects use LoRa (long range) wireless networking to send text messages through the air to other mesh nodes. These messages are sent without using the internet or cell towers and the network is operated almost entirely on cheap ~$30 LoRa boards, many of them solar powered. Unlike amateur radio, these mesh networking projects operate on unlicensed bands, so users do not need a ham radio license to get started.

Because of the low cost, Meshtastic and MeshCore are great projects to learn:

* radio fundamentals, such as frequency and wavelength concepts and basic signal propagation
* electronics basics, like building circuits and soldering
* antenna and signal attenuation fundamentals 

# How does mesh networking work?

The core concepts for Meshtastic and MeshCore are the same. 

A user sends a text message from their handheld radio, called a "node". This node can be a stand-alone device with a screen and a keyboard, or it could be a low-powered, pocketable device with just an antenna that the user connects to over Bluetooth from their phone. Any nodes that are nearby and can hear that initial message repeat the message to any other devices that can hear them. Nodes that heard that repeated message in turn repeat the message to those that are within their range, and so on. 

This results in a "mesh" network. Each individual device doesn't need to be powerful enough to reach every other device in Philadelphia, it only needs to reach one other device, which then in turn can reach one other device, and so on.

To expand this network further, in Philadelphia we have a number of dedicated "repeater" nodes that are installed on rooftops. While messages between small ground-level nodes might only travel 5-10 blocks on their own, messages sent from or repeated by these rooftop repeaters can travel many miles, depending on how much clear line-of-sight they have around them. 

Most of these repeater nodes are installed and maintained independently by hobbyists who happen to have access to a high roof. PhillyMesh also maintains some official nodes in partnership with local organizations such as Philly Community Wireless and PhillyWisper. We are always open to new partnerships! While we cannot pay you to host a node, we provide all parts, materials, and installation and can also provide educational talks and future support to interested parties.

# Why do people use mesh networking to communicate?

Communicating over the internet or cell networks usually works reliably, but those networks often have a point of failure that is out of the users' control.

When the cell network is overloaded, at an event like a festival or convention, text messaging and internet-reliant messaging no longer work. Mesh networking has the opposite effect in crowded environments: its reliability improves as you add more nodes.

If you're going camping in the woods where there aren't existing cell towers, you can't exactly bring your own cell tower with you. For about $100 you can build a handful of solar powered mesh networking devices that allow you to communicate with those around you.

Mesh networking hobbyists also enjoy the challenges that come along with new technology, especially the fact that we get to build it ourselves. We have folks in our community that get really into the radio frequency science side of things, running tests to figure out the optimal settings to improve signal across the region. We have other folks who enjoy designing and building the cheapest and most effective solar powered mesh nodes to make hosting a mesh node more accessible to more people.

# Comparing Meshtastic and MeshCore

Meshtastic and MeshCore, while they are built on the same fundamental concepts, are different enough that they cannot interoperate. A MeshCore text message cannot be received and decrypted by a Meshtastic node and vice versa.

From 2021-2026 Meshtastic was overwhelmingly the most popular mesh networking project in Philadelphia. However, in the summer of 2026, Meshtastic introduced some config changes that, when tested by PhillyMesh users, proved to not perform very well in Philadelphia. As a result, many users decided to try out the MeshCore project.

As much as possible, our PhillyMesh nodes support both projects. That being said, as of fall 2026, if you're a beginner who wants to try out the project with which you'll be able to communicate with the most people in Philadelphia, we recommend starting with MeshCore.

# Learn more

We have a getting started guide for both MeshCore and Meshtastic:

- [Intro to MeshCore](/2026/09/02/meshcore-intro/)
- [Intro to Meshtastic](/getting-started)

The currently recommended local settings for both Meshtastic and MeshCore can be found on the [PhillyMesh.net homepage](https://phillymesh.net).

## Live Maps

### MeshMapper (MeshCore)

Below is a user-generated map of where MeshCore coverage currently exists and where it doesn't, on PhillyMesh's recommended settings. For more information, check out the [MeshMapper website](https://midatl.meshmapper.net/?preset=919.5%2C500%2C10&m=std&l=rep.rcov.nz.rb&cm=eff&lat=39.89583&lon=-75.15655&zoom=10.67).

<iframe src="https://midatl.meshmapper.net/embed.php?preset=919.5%2C500%2C10&m=std&cm=eff&lat=39.92766&lon=-75.16334&zoom=11&geofence=0&l=rcov.nz" width="100%" height="500" title="MeshMapper MeshCore coverage map"></iframe>

### CoreScope (MeshCore)

Below is a live map of many MeshCore repeaters in the Philadelphia area. This shows repeaters that are connected to a node that reports data to [CoreScope](https://corescope500.phlm.sh/#/map), so there may be many repeaters that don't show up on this map.

<iframe src="https://corescope500.phlm.sh/#/live" width="100%" height="500" title="View of PhillyMesh CoreScope Instance"></iframe>

### Malla (Meshtastic)

Below is a live map of many of the Meshtastic nodes in the Philadelphia area. This only shows nodes that 1) report location (many choose to not report location) and 2) are connected to a node that reports data to [Malla](https://api.phillymesh.net/map).

<iframe src="https://api.phillymesh.net/map?sidebar-collapsed=true" width="100%" height="500" title="View of PhillyMesh Malla Instance"></iframe>

*With both MeshCore and Meshtastic, the only way to know for certain if there are other nodes in your area is to set up a node, install it in the highest window you have access to, and leave it running for a day or two.*

## Discord

The [PhillyMesh Discord](https://discord.gg/MWWbAkRR9v) is a great resource for getting started. Any and all questions about mesh networking and amateur radio are welcome in our #no-dumb-questions channel and you can use your local neighborhood's channel to connect and coordinate with others in your local area.
