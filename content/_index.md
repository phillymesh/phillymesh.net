---
title: Home
author: Mike Dank
type: homepage
#cspell:ignore Rokland Yggdrasil
---
<div class="pm-hero">
<p>PhillyMesh is a group for people who enjoy experimenting with mesh networking and related decentralized technologies. We run several <a href="https://meshcore.io/">MeshCore</a> and <a href="https://meshtastic.org/">Meshtastic</a> nodes across the Greater Philadelphia area.</p>
{{<discord-badge href="https://discord.gg/MWWbAkRR9v">}}Join us on Discord{{</discord-badge>}}
</div>

## Start Here

Brand new? Read our [overview of mesh networking in Philly](/overview/).

As much as possible, PhillyMesh supports all free, open-source mesh networking projects.

Take a look at the maps to see what project the nodes near you are using. They are not interoperable, but you can always change your mind and flash the other project later!

<div class="pm-switch">
<input type="radio" name="pm-project" id="pm-pick-mc" checked>
<input type="radio" name="pm-project" id="pm-pick-mt">
<div class="pm-tabs">
<label for="pm-pick-mc">MeshCore<small>919.5 MHz/500 kHz/10 SF</small></label>
<label for="pm-pick-mt">Meshtastic<small>LongTurbo</small></label>
</div>
<div class="pm-panel pm-mc">

### Recommended MeshCore settings

| Setting | Value |
|---|---|
| Frequency | `919.500 MHz` |
| Bandwidth | `500 kHz` |
| Spreading Factor | `10` |
| Coding Rate | `4/5` (some apps just say `5`) |
| Path Hash Mode | `1` (2-byte mode, sometimes listed as `1-2 byte`) |

*These settings are FCC-compliant and avoid the heavier ISM band interference we found during our [summer 2026 testing](/2026/08/12/freq-testing-report/). Update your node to the latest firmware first.*

### Guides

- [What you need to know about MeshCore coming from Meshtastic](/2026/09/02/meshcore-intro/)
- [How to flash MeshCore coming from Meshtastic](/2026/09/02/how-to-flash-meshcore/)

<details class="pm-map">
<summary>Live map</summary>

Some of the MeshCore nodes on our 919.5/500/10 settings in the Philadelphia area, and live traffic on the network, from our [CoreScope](https://corescope500.phlm.sh/#/map) instance.

<iframe src="https://corescope500.phlm.sh/#/live" width="100%" height="600" loading="lazy" title="View of PhillyMesh CoreScope Instance"></iframe>

</details>

<details class="pm-map">
<summary>Coverage map</summary>

This is a map generated from wardriving data. Check out [MeshMapper](https://midatl.meshmapper.net/?preset=919.5%2C500%2C10&m=std&l=rep.rcov.nz.rb&cm=eff&lat=39.89583&lon=-75.15655&zoom=10.67) for a more complete view.

<iframe src="https://midatl.meshmapper.net/embed.php?preset=919.5%2C500%2C10&m=std&cm=eff&lat=39.92766&lon=-75.16334&zoom=11&geofence=0&l=rcov.nz" width="100%" height="500" loading="lazy" title="MeshMapper MeshCore coverage map"></iframe>

</details>

*These maps do not show all nodes. The only way to know for sure if there are any nodes near you is to flash your node and send a few test messages.*

</div>
<div class="pm-panel pm-mt">

### Recommended Meshtastic settings

| Setting | Value |
|---|---|
| Frequency | `908.75 MHz` (the default slot, enter as `0` or `14`) |
| Preset | `LongTurbo` |

*These are the new default, FCC-compliant settings the Meshtastic project recommends for the US. Update your firmware to the latest stable or beta version first. We no longer use LongFast because [it is not FCC-compliant](/2026/09/02/fcc-regulations/).*

### Guides

- [Getting Started with Meshtastic in Philly](/getting-started/) (This guide is slightly out of date, because it focuses on LongFast)

<details class="pm-map">
<summary>Live map</summary>

Some of the Meshtastic nodes in the Philadelphia area. This map shows all nodes, including ones that are on presets other than LongTurbo. Check out the full [Malla](https://api.phillymesh.net/map) and filter by PrimaryChannel = LongTurbo to see if there are nodes on LongTurbo near you.

<iframe src="https://api.phillymesh.net/map?sidebar-collapsed=true" width="100%" height="500" loading="lazy" title="View of PhillyMesh Malla Instance"></iframe>

</details>

*This map only shows nodes that are opted into MQTT and connected to a reporting node. The only way to know for sure if there are any nodes near you is to flash your node and send a few test messages.*

</div>
</div>

## Support PhillyMesh

If you'd like to help support PhillyMesh and Philly Radio & Mesh, please consider using our affiliate links:

- [Rokland](https://store.rokland.com/?ref=phillymesh) for Meshtastic and MeshCore hardware
- [Battery Hookup](https://batteryhookup.com/discount/PhillyMesh) for genuine batteries (please don't buy 18650s from Amazon)

## History

Not limited to LoRa-based networks, PhillyMesh has been open for experimentation with all meshing projects since 2013. Other areas of interest include 802.11-based networks (Wi-Fi), meshing via amateur radio projects such as AREDN, routing protocols and practices (such as BGP), overlay networks (such as Tor and Yggdrasil), and other networking projects and technologies (such as DNS, or just networking fundamentals). Check out our [post history](/post/) to learn more.
