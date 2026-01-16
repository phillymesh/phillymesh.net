---
title: "Real-Time Meshtastic Decoding with Scapy and Wireshark"
author: "Caleb Frey"
date: 2026-01-10T21:19:45-05:00
draft: false
tags:
  - meshtastic
  - mqtt
---
# The Goal
When I powered on my first Meshtastic node, I was blown away at the ability to exchange messages with people over multiple hops without even needing a license.
That awe lasted about a week before I noticed that sometimes the intended recipient never saw it.
Or the messages would often go unacknowledged, leaving me to wonder whether anyone saw it at all.
So I decided to do some digging to figure out why the message delivery was so inconsistent.

I dug into the Meshtastic [documentation](https://meshtastic.org/docs/introduction/) to learn about the "managed flooding" broadcase approach to understand how a packet gets transmitted.
In summary, the stronger a signal is for a given packet, the longer a node will wait before transmitting it, and it won't transmit if it already heard others rebroadcast it.
Theoretically this helps a signal travel as far as possible, with the assumption that weaker signal corresponds to a further distance.
But since we don't live in a perfect spherical vacuum, you end up with strange routes like a node in someone's basement becoming the preferred hop when it's the least useful.
It seems chaotic and strange but it makes sense when the system is designed for a group of nodes in constantly changing conditions and locations (and outdoor usage).
However, I wasn't content to just read about the broadcast approach, I wanted to see it in real time, from the perspective of my node here in Philly.

The Meshtastic client apps (at least for web and android) are designed first and foremost for usability, and as a result hide away a lot of the underlying networking.
I wanted to be able to see all the Meshtastic packets in the air, shown live in a tool like Wireshark for dissection and analysis.
It's possible to enable debugging mode in the app, but that requires a consistent connection to the phone app, where the data isn't particularly easy to parse.
There is also the option to enable serial debugging, but it wouldn't use the existing usb c link and I didn't love the idea of running flying leads to a USB serial converter.
Thankfully, since the Meshtastic protocol is open source, there wasn't any requirement that I even use a Meshtastic node.
I'll write my own receive-only client! How hard could it be?

# Hardware: Pulling LoRa from the Airwaves
All Meshtastic Devices amount to a LoRa modem and something to run the meshtastic device code, usually a microcontroller.
So if I wanted to decode Meshtastic, I needed some form of LoRa modem that could be plugged into my PC.
Thankfully, someone in the PhillyMesh Community had already purchased a [CatWaN USB Stick](https://electroniccats.com/store/catwan-usb-stick/) with similar intentions and let me borrow it.
This USB device consists of an RP2040 microcontroller, a RFM95W Modem and not much else, which is exactly what I wanted. 

To get the data from USB Stick to the computer, I wrote some simple firmware as for the CatWAN as if it were a Raspberry Pi Pico, since it's the same underlying chip.
I configured the LoRa module with the parameters to match the [LongFast Radio Preset](https://meshtastic.org/docs/overview/radio-settings/#presets), along with the default frequency (906.875MHz) and sync word (`0x2B`).
Every time a new LoRa signal with those parameters arrived, it was encapsulated with [LoRaTap](https://github.com/eriknl/LoRaTap/), which is mostly a header with some radio information, and written to USB Serial.
To distinguish the end of one transmission from the start of another (and avoid the `\n` vs `\r\n` conflict) I terminated each packet with a special byte sequence unlikely to be in the real data.

# Software
Now that I had an incoming stream of LoRa packets I had to learn how to decode them.
The wonderful folks selling the [HackerPager](https://www.hackerpager.net/) had already written a Meshtastic decoder plugin for Wireshark to be used on captured .pcap files, but I didn't have pcap files.
After reading the [specifications for a pcap file](https://ietf-opsawg-wg.github.io/draft-ietf-opsawg-pcap/draft-ietf-opsawg-pcap.html) I wrote a script that encapsulated the incoming LoRaTap stream into a valid stream of pcap data.
Each pcap data stream must begin with a pcap header that includes the correct [link type](https://datatracker.ietf.org/doc/html/draft-ietf-opsawg-pcaplinktype-16) (270 for LoRaTap),
followed by the individual packets, each of which had to be wrapped with timestamp and other capture information.

Once I was generating valid pcap files and followed the guide to install the HackerPager plugin, I was finally able to see all the Meshtastic traffic happening around me during that capture.
Wireshark supports pcap streams via stdin, so after a few tweaks (and discovering that powershell doesn't do normal byte-friendly piping) I had a live view of all the meshtastic traffic around me.
This was an amazing sight, being able to see "hello world" messages pinging back and forth between nodes, but I didn't plan to stop at Wireshark.
I wanted data collection and analytics, and I wasn't planning to do it all using Wireshark and Lua.

Enter: [Scapy](https://scapy.net/) - a packet manipulation library for Python. Think of it like Wireshark but with the ability to assemble and modify packets, not just read them.
Scapy decodes packets into individual layers, and includes many built-in layers, from HTTP and the OSI model to CAN bus protocols.
Unsurprisingly, it doesn't include anything for Meshtastic, so I had to add those layers myself.

## Dissecting a Meshtastic Packet
Using the Meshtastic documentation to understand the protocol, the HackerPager Wireshark plugin as a reference implementation,
and many many tabs of Scapy documentation, I was able to identify and decode the contents of each layer in the meshtastic packet.
I'll walk you through them.

### Layer 1: LoRaTap
- Mostly just an encapsulation format that Wireshark and other tools can decode
- Includes received radio information including LoRa config and SNR/RSSI
- Sync Word - byte that can be used to set a protocol
  - Need all your LoRa devices to have the same sync word
  - Meshtastic = 0x2B, LoRaWan uses 0x34
  - Think of this like a VLAN ID
- Message size

### Layer 2: MeshPacket
- Unencrypted protobuf that all nodes can read
- Routing information so other nodes can relay the packet
  - Source and destination radio IDs
  - Packet ID (used for deduplication and encryption)
  - Hop information
    - Hop limit is how many hops are "left"
    - Hop start is how many hops it started with
    - Last hop data to do some intelligent routing
- Channel hash to speed up decryption

### Layer 3: MeshPayload
- Encrypted protobuf containing the actual data
- Encrypted with AES256-CTR stream cipher
  - Uses the channel key and packet ID to encrypt/decrypt
- "Port Number" determines what app protocol is being used
- Additional metadata like request/reply IDs and the source/dest ID

### Layer 4: MeshApp or MeshText
- This is the end-user functionality of the device
- Remaining data in the LoRa packet is decoded as a protobuf according to the port number
- Applications include:
  - Node info
  - Position
  - Telemetry
- Text messages (port number = 1) contain the message as a binary string

For each layer I had to define all the fields to be extracted and write the dissection logic to set the values of those fields, including decryption and protobuf decoding.
After I had created each layer I had to "register" them with the scapy interpreter so it knew to associate the incoming data and subsequent payloads with the correct dissector.

Once Scapy fully dissected a packet I was able to access the individual fields in each packet as if it were a typical Python object.
Every packet that was processed (if it could be decoded) was added to an SQLite database to record network traffic and create a collection of known nodes based on their periodic NodeInfo broadcasts.
This let me take a look at stats such as airtime utilization by different nodes, protocols, and in general perform long-term trend observation.
I could even grow beyond my single data source with volunteers hosting another instance and sending the results to a central database
in an to get a holistic view of all the Meshtastic traffic in the city.

# The Results
Now that I had a process to collect and record all Meshtastic traffic happening around me, without the limits of using a proper Meshtastic node,
I could determine the cause of the inconsistent connectivity if I knew where to look.

Unfortunately, I didn't see anything obviously symptomatic of an unreliable network and adding advanced analytics, a webUI, and distributed data collection was beyond my skills and interest.
Lucky I was introduced to a tool called [Malla](https://github.com/zenitraM/malla),
which can collect data from multiple sources using MQTT and display them all in a much slicker WebUI than I would have been able to make.
So rather than reinvent the wheel I started a [PhillyMesh Malla Instance](https://api.phillymesh.net/) with a number of gateways feeding data into the platform.
The one limitation of Malla over the raw LoRa decoding is that by default, nodes don't have "Ok to MQTT" enabled so we don't have a complete picture,
but I doubt I could convince multiple people to setup a whole mini PC for raw LoRa sniffing, so I think the trade-off is worth it.

While I didn't end up using this project long-term to learn about our Mesh, I did learn plenty of new things along the way:
- I hadn't done embedded development in a very long time and learned about platform.io
- This was my first time dealing with binary data, bitmasking, and endianness
- I had never dealt with protobufs before but now understand why they're used everywhere
- I finally used a proper database, and I'm coming around to tolerating SQL after resisting for so long
- I learned that I should continue avoiding low-level cryptography
  - It's a bad sign when you start calling functions with "hazmat" in the name

I also got to show off my project at Jawncon 0x2 and it was so cool to see people interested in something I worked on,
especially those working on the [Kismet](https://www.kismetwireless.net/) RF analysis suite.
The idea that something I wrote as a side project could get integrated into a larger project is very exciting.

For now it's a mostly-stanalone set of scripts that are tedious to get working, but it's as feature-complete as I plan to make it.
All the source code for this project, including the firmware, build instructions, and sample SQL queries,
are available at https://github.com/calefrey/scapy-meshtastic.

