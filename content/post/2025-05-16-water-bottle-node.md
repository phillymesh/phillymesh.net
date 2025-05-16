---
title: Stealthy Water Bottle Node
author: Emily Boda
type: post
date: 2025-05-16T00:00:01+00:00
url: /2025/05/16/water-bottle-node/
categories:
  - Philly Mesh
tags:
  - meshtastic
  - wisblock

---

# Stealthy Water Bottle Node

For most of the day, I can be found carrying a T-1000e in my pocket. My home has (or will have ) a node on the roof with a longer range antenna, and my T-1000e works perfectly to keep myself connected to the mesh, even if my phone can't connect all the way to my roof node via bluetooth. However, when I travel outside of the house the tiny antenna in the T-1000e leaves something to be desired.

To fill this gap, I came up with a plan for a portable node with a longer range antenna that I could easily stick in a backpack or leave on my bike that wouldn't raise any alarms. While I'm not averse to carrying around large antennas, I like to save this activity for radio meetups or cons, and be a little less obvious in my day to day life. I realized this bike waterbottle I had was exactly the right length for the whip antenna I had laying around.

Since I built and started using this water bottle node, I don't know how more people don't do something like this! You can stick it in a water bottle pocket of a backpack and it stays vertically polarized. The antenna doesn't get bent or unscrewed in your bag. It's entirely waterproof so you don't have to worry about getting caught in the rain. And it doesn't get any curious looks from cursory bag checks at hospitals or museums. As a general disclaimer, I would NOT recommend bringing this to any high security location like an airport. TSA is generally fine with radio and Meshtastic equipment, but something like this might get you pulled into a room and interrogated about why you're hiding wires, batteries, and antennas in a normal looking object.

## Parts list

| Parts | Price | Description |
| ----- | ----- | ----------- |
| [WisBlock Starter Kit](https://store.rakwireless.com/products/wisblock-starter-kit?srsltid=AfmBOoqGNa6h2MSgg5oLSWXtv6xPEiVNtHl4h6oP_BMcHh4kBFPVji3x&variant=41786685063366) | $24.99 | This is the Meshtastic node. You want the RAK19007+RAK4631 version (I don't know what -R means). Pick the frequency for your region, USA is 915. |
| [Water Bottle](https://www.specialized.com/us/en/purist-moflo-22oz/p/157653) | $11.99 | I had a Specialized MoFlo 22oz bike water bottle lying around. It barely fits this 17cm Gizont whip antenna (that's actually slightly less than 17cm) that I had, but may not fit other 17cm whip antennas. I'd recommend grabbing whatever antenna you have available and finding a water bottle that fits that. |
| [Antenna](https://ovvys.com/products/gizont-long-range-whip-antenna?srsltid=AfmBOorSCCA6EwAnSAkfMoFwI7ncjHl4AFluoO8OGU7GVjI1yp73MW33) | $13.00 | I can't vouch for this particular distributer, but I've used Gizont whip antennas for many projects and always had good results. I think I bought this one on eBay, so just search the name of the antenna and find it wherever is most convenient. |
| [Right angle SMA to IPEX cable](https://www.amazon.com/Female-Right-Angle-Coaxial-12inch/dp/B098QFZ2DB?th=1) | $10.99 | If you have tight clearances you'll need one of these right angle cables rather than the usual straight ones. |
| [MuziWorks H1 Battery (1200 mAh)](https://muzi.works/products/h1-battery?srsltid=AfmBOorybyZ_2L17M_H8qQfEdhiu6lNvZm79b52aTs1dyez0qWbZaAZX)
