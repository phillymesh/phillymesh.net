---
title: Hosting a Node for Philly Radio & Mesh
author: Kyle Yankanich
type: post
date: 2026-08-03
url: /hosting-a-node
categories:
  - Philly Mesh
tags:
  - meshtastic
#cspell:ignore Yankanich Kyle
---

# Hosting a node

*First, please read [our quick overview of mesh networking](/overview.md).*

Are you interested in hosting a node? Reach out to us at hello@phillymesh.net. We have experienced installers who can assess your proposed location and determine what’s the best fit for you.

Below is an overview of the types of nodes we can install.

## Nebra Node

<add picture>

Our Nebra Dual-Radio nodes are the flagship mesh networking nodes. They support both MeshCore and Meshtastic and they are the highest priority for us to deploy. However, they require on-site power and preferably an internet connection.

They cost us a few hundred dollars to build, and we are an entirely volunteer organization, so we try to save these nodes for locations where they would substantially improve the surrounding mesh.

If you’re able to host one, PhillyMesh would still be the owners of the equipment and we choose what frequency settings and mesh technology it runs based on what’s best for the area. We will handle all updates and maintenance remotely over the internet connection.

We build these nodes to survive all kinds of weather, but there is always the possibility that an unforeseen storm may take the node offline. If that happens, we ask that you allow us to coordinate with you so we can come out and service the node. We anticipate service to be required less than once a year, and when it is needed it will not be urgent: we can work around your schedule.

### Requirements:

- Permission to install
- A location that is advantageous to the surrounding mesh
  - high on a roof
  - line-of-site to surrounding area
  - an area that has little-to-no existing mesh networking nodes
- Power on-site
- Coordination from you for install site-visit and subsequent visits (less than annually)

### Preferred:

- Internet connection (Wi-fi or POE)
  - If there is no internet, we can make do with a cellular internet connection, but that costs us about $100/year (or more) and is less reliable, so we prefer not to
- A pole or other solid mounting location

## Solar-Powered Node

<add picture>

If you’re an individual or organization who wants to improve the mesh, but you don’t have a location with power, you may be a better fit for a solar node. These nodes are much smaller and can be mounted in many more places than a Nebra node.

We recommend making one of these Harbor Breeze Solar Light nodes yourself for about $40. Whether we have any parts or full builds to donate, depends entirely on our volunteer’s availability and how much they are willing to donate out of their own wallets. We are an all-volunteer organization with no funding, so if your install location is extremely valuable to one of our volunteers, that will definitely sweeten the deal :)

Once installed, these solar nodes will be your responsibility. We’re always available to assist remotely, and we may even be able to send a volunteer to help out, but that’s not guaranteed. You’re under no obligation to keep them updated on any sort of schedule, but we ask that you plan to update them at least once every 3-6 months and join our Discord so, at the very least, we can reach out to you if we have question/suggestions/new information about what mesh technologies are popular in your neighborhood.

Over-the-air updates are a new and useful feature that’s recently been introduced into some mesh networking firmware, however, it is not the most reliable way of updating your node. We don’t recommend installing these solar nodes anywhere that you can’t easily access and connect to your computer for infrequent updates.

There are also more expensive pre-built solar-powered nodes that you can purchase. Options include Seeed Studio’s P1 Pro ($90) and Heltec’s MeshTower ($200). We recommend adding extra weatherproofing to any off-the-shelf node that you purchase (particularly around the antenna), and you will still have to flash the firmware yourself, but this is a better option if you don’t want to DIY.

### Requirements:

- Permission to install
- A location that you can easily return to for biannual updates

### Preferred:

- A location that is advantageous to the surrounding mesh
  - high on a roof
  - line-of-site to surrounding area
  - an area that has little-to-no existing mesh networking nodes

# FAQ

## Why should I place a node on my property?

- Boosts Public Safety: when other services go down, the mesh networking still operates to get people help they need and share information
- Builds Community: When one node pops up, others inevitably join in your area

## Am I exposing personal information about myself to the world by hosting a node?

Basically none. Mesh nodes do not make any information like your WiFi network name public or give anyone access to your internet connection. You choose the name for your node that is viewable by others on the mesh, which can be as generic as "Repeater #4". We ask that you choose a nearby location for your node to report, but it does not have to be at the exact point it is in real life. A nearby spot that is down the street or at the next intersection over is good enough for other users to be able to point their antennas in the correct direction.