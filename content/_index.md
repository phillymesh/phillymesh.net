---
title: Home
author: Mike Dank
type: homepage
#cspell:ignore Rokland Yggdrasil
---

<style>
.pm-hero { margin: 1.5em 0 2em; }
.pm-hero p { font-size: 1.15em; margin: 0 0 1.2em; }
.pm-discord {
  display: inline-flex;
  align-items: center;
  gap: 0.6em;
  padding: 0.9em 2em;
  border-radius: 10px;
  background: #5865F2;
  color: #fff !important;
  font-size: 1.25em;
  font-weight: bold;
  text-decoration: none !important;
  border: none !important;
}
.pm-discord:hover, .pm-discord:focus-visible { background: #4752C4; }
.pm-discord svg { width: 1.4em; height: 1.4em; fill: currentColor; flex-shrink: 0; }
.pm-discord-note { display: block; margin-top: 0.6em; font-size: 0.9em; color: var(--post-info-color); }

.pm-switch > input { position: absolute; opacity: 0; pointer-events: none; }
.pm-tabs { display: flex; gap: 0.5em; margin: 0.5em 0 0; }
.pm-tabs label {
  flex: 1;
  text-align: center;
  padding: 0.8em 0.5em;
  border: 2px solid var(--hr-color);
  border-bottom: none;
  border-radius: 10px 10px 0 0;
  cursor: pointer;
  font-weight: bold;
  font-size: 1.1em;
  color: var(--nav-link-color);
}
.pm-tabs label small { display: block; font-weight: normal; font-size: 0.75em; }
#pm-pick-mc:checked ~ .pm-tabs label[for="pm-pick-mc"],
#pm-pick-mt:checked ~ .pm-tabs label[for="pm-pick-mt"] {
  border-color: var(--link-color);
  color: var(--font-color);
  background: var(--nav-bg-color);
}
#pm-pick-mc:focus-visible ~ .pm-tabs label[for="pm-pick-mc"],
#pm-pick-mt:focus-visible ~ .pm-tabs label[for="pm-pick-mt"] { outline: 2px solid var(--link-color); }
.pm-panel {
  display: none;
  border: 2px solid var(--link-color);
  border-radius: 0 0 10px 10px;
  padding: 0.5em 1.2em 1.2em;
}
#pm-pick-mc:checked ~ .pm-mc, #pm-pick-mt:checked ~ .pm-mt { display: block; }
.pm-panel iframe { border: 0; border-radius: 6px; }
.pm-map { margin: 1em 0; border: 1px solid var(--hr-color); border-radius: 8px; padding: 0 1em; }
.pm-map summary { cursor: pointer; font-weight: bold; font-size: 1.15em; padding: 0.7em 0; }
.pm-map summary::after { content: " (click to show)"; font-weight: normal; font-size: 0.8em; color: var(--post-info-color); }
.pm-map[open] summary::after { content: " (click to hide)"; }
.pm-map[open] { padding-bottom: 1em; }
</style>

<div class="pm-hero">
<p>PhillyMesh is a group for people who enjoy experimenting with mesh networking and related decentralized technologies. We run several <a href="https://meshcore.io/">MeshCore</a> and <a href="https://meshtastic.org/">Meshtastic</a> nodes across the Greater Philadelphia area.</p>
<a class="pm-discord" href="https://discord.gg/MWWbAkRR9v"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3332-.946 2.4189-2.1568 2.4189Z"/></svg>Join us on Discord</a>

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
