---
title: Home
author: Mike Dank (Famicoman)
type: homepage
---

PhillyMesh is a group for people who enjoy experimenting with mesh networking and related decentralized/distributed technologies.

**We run several [Meshtastic](https://meshtastic.org/) and [MeshCore](https://meshcore.io/) nodes in the Greater Philadelphia area.**

# Discord

Join the [**Philly Radio & Mesh Discord**](https://discord.gg/MWWbAkRR9v) to chat with others in the area.

# Getting started with Meshtastic

*These are the new default, FCC-compliant settings, that the Meshtastic project recommends for the US. Please update your firmware to the latest stable/beta version first!*

- Frequency: `908.75 MHz` (this is the default slot, which you can enter as `0` or `14`)
- Preset: `LongTurbo`

We also wrote a [Getting Started guide](/getting-started) which details local groups, Discords, and meetups for Meshtastic, as well as best practices and lessons learned for using Meshtastic in our local area. It is slightly out of date, as it focuses on LongFast which [we no longer use because it is not FCC-compliant](https://phillymesh.net/2026/09/02/fcc-regulations/).

# Getting started with MeshCore

*These are the settings we recommend for using MeshCore with 500 kHz bandwidth. They are FCC-compliant and avoid the heaviest ISM band interference that we found during our summer 2026 testing in the Philadelphia area. Please make sure your MeshCore node is updated to the latest firmware before using these settings!*

- Frequency: `902.250 MHz`
- Bandwidth: `500 kHz`
- Spreading Factor: `11`
- Coding Rate: `4/5` (some apps may just say `5`)
- Path Hash Mode: `1` (2-byte mode, some apps list this setting as `1-2 byte`)

We also wrote these pages that might be of help if you're new to MeshCore:
- [What you need to know about MeshCore coming from Meshtastic](https://phillymesh.net/2026/09/02/meshcore-intro)
- [How to flash MeshCore coming from Meshtastic](https://phillymesh.net/2026/09/02/how-to-flash-meshcore)

# Supporting PhillyMesh

If you are interested in helping support PhillyMesh and Philly Radio & Mesh, please consider using one of our affiliate links from these awesome vendors:

- [Rokland affiliate link for Meshtastic and MeshCore hardware](https://store.rokland.com/?ref=phillymesh)
- [Battery Hookup affiliate link for genuine batteries (please don't buy 18650s from Amazon)](https://batteryhookup.com/discount/PhillyMesh)

# PhillyMesh Malla Instance

This shows some of the Meshtastic nodes on LongFast in the Philadelphia area. It does not show all of them because nodes must opt-in to participate in MQTT.

<iframe src="https://api.phillymesh.net/map?sidebar-collapsed=true" width="100%" height="500" title="View of PhillyMesh Malla Instance"></iframe>

# History

Not limited to Lora-based networks, PhillyMesh has been open for experimentation with all meshing projects since 2013. Other areas of interest include 802.11-based networks (Wi-Fi), meshing via amateur radio projects such as AREDN, and routing protocols and practices (such as BGP), overlay networks (such as Tor and Yggdrasil), and other networking-based projects/technologies (such as DNS, or even just networking fundamentals). Check out our post history to learn more.
