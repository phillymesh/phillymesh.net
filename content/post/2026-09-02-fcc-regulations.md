---
title: PhillyMesh Statement on the FCC Regulations for DTS-mode Devices using the 900 MHz ISM Band
author: Emily Boda
type: post
date: 2026-09-02T00:00:01+00:00
url: /2026/09/02/fcc-regulations/
categories:
  - Philly Mesh
tags:
  - meshtastic
  - meshcore
#cspell:ignore RemoteTerm opsdiv FHSS APRS Delco
---

*As a quick note, none of the Operations Division are lawyers, and none of us play lawyers on TV. Even though we discuss FCC regulations throughout this document, nothing in this document or FAQ is legal analysis or legal advice to anyone reading it. Please, for the love of heaven, always consult an actual lawyer when you have questions about the law, or FCC regulations.*

# Hey PhillyMesh community,

## Our mesh is about to become a lot more fragmented

We, (along with many in the Meshtastic community) recently found out that **most of Meshtastic's presets are not in compliance with the FCC** when the newest build of the Meshtastic app changed the USA default preset to LongTurbo. We don't yet have any official word from the Meshtastic developers about this, but the following is our understanding.

Meshtastic uses a 250 kHz bandwidth by default, and [FCC regulations state](https://www.ecfr.gov/current/title-47/part-15/section-15.247#p-15.247(a)(2)) that devices in the 900 MHz ISM frequency band (that's us) must use a bandwidth of 500 kHz or higher. The only Meshtastic preset that's in compliance is LongTurbo, which we have tested extensively and determined doesn't work well for long distance mesh communication in Philly. [Other metro areas](https://github.com/meshcore-dev/MeshCore/issues/945#issuecomment-3408847889) [have corroborated this](https://github.com/meshcore-dev/MeshCore/issues/945#issuecomment-3408643590); **LongTurbo doesn't work well just about anywhere**.

We have a [blog post](https://phillymesh.net/2026/08/12/freq-testing-report/) with all details of our LongTurbo test, but the summary is that there is a lot of interference within the ISM band, much of which is concentrated every 250 kHz (so, on .000, .250, .500, and .750 on each MHz frequency, with the worst of it being on .250/.750). Using only a 250 kHz slice of bandwidth (for example, from 915.000 to 915.250 MHz) allowed us to keep that interference on the edge of our communication spectrum. However, if we have to use 500 kHz bandwidth, we can't avoid that interference (we've looked all over the ISM Band) and **we confirmed (with your help in this summer's tests) that our ability to communicate with Meshtastic is severely compromised**.

## So, what are we going to do?

**We're wrapping up our LF910 test and now moving to compliant presets**. Because our Meshtastic LongTurbo testing went so poorly, the OpsDiv started scrambling to find options that might work better to achieve the goal of a Philadelphia-area-wide mesh network that allows us to communicate from the city to the burbs. **We started informally testing some custom settings for MeshCore at 500 kHz (we're calling it "MeshCore 500") and found that it worked surprisingly well**.

One of the biggest reasons we've seen better results with MeshCore is because it is more resilient due to its message-prioritized routing. The settings we've been tweaking during this summer's testing period to try to improve Meshtastic's performance (reducing position, telemetry, nodeinfo announcements, and more) are pre-baked into the MeshCore firmware. The additional hops MeshCore allows should mitigate the loss of reach/distance nodes that is caused by operating with a bandwidth that has more interference.

Based on that testing, going forward, **the handful of PhillyMesh infrastructure nodes that are currently installed will be tuned to MeshCore 500** because we believe this gives us a better chance to create a Philadelphia-area-wide network. Additionally, we have leads on installing several dual-radio nodes at high sites and **these will feature both Meshtastic LongTurbo and MeshCore 500**. We expect that given time, Meshtastic LongTurbo may become a more viable short-distance mesh network, especially as Meshtastic firmware matures and resolves some of the issues with overly-frequent position/telemetry/nodeinfo reports. However, MeshCore 500 is currently performing much better and will likely always be better for long-distance mesh communication. As has always been the case, **you're welcome to install whatever preset and mesh technology you're comfortable with running on your personal nodes**.

We considered announcing MeshCore 500 as a test, but we've been doing a lot of testing this summer and, honestly, a week-long test for something we already know initially shows promise won't get us the results we need. We decided to announce this as a transition (kind of like our indefinite LF910 test) and let the people decide if they want to participate. If things go poorly with MeshCore 500 or the technology changes in six months or a year (or the Meshtastic project sorts this whole thing out next week and makes LongFast FCC-compliant in a way that doesn't nuke its effectiveness) we might just go back to Meshtastic LongFast as our default. But we wanted to make one unified recommendation for right now, for those who want to test out something new with us, since we won't be able to use LongFast for the foreseeable future. Plus, trying new mesh networks is fun!

Unfortunately, **the days of defaulting to Meshtastic LongFast and everyone being on the same mesh network are likely behind us**. We expect some people will stay on Meshtastic LongFast, and once Meshtastic's default preset becomes LongTurbo, we expect many people new to the hobby (an estimated 20 people per week in our area) to be on LongTurbo. We also expect many of those who have been dabbling in MeshCore and seeing how well it performs to keep tinkering with MeshCore 500. There will likely not be one consensus network going forward, but we hope that you'll try out MeshCore 500 with us.

**<u>You do not have to buy new hardware to try out MeshCore 500</u>: almost all Meshtastic node hardware models are compatible with MeshCore and you can flash between the two as easily as you can flash between versions of the Meshtastic firmware**. If you try MeshCore and want to go back to Meshtastic, it's completely and easily reversible in a minute or so. After reading the guide to flashing your node below, if you have any questions about converting your node and changing settings, please reach out on the #meshcore-philly channel in the Discord. We are happy to help guide folks through this transition!

"But I thought this was a Meshtastic server?" Technically, the server name is just "Philly Radio & Mesh"... and if you take a look at the PhillyMesh website, you'll see posts as far back as 2016 (before Meshtastic was invented) exploring mesh networks in the Philadelphia area. Meshtastic has been a focus lately because it's been more popular in the Philadelphia area. We're here to have a good time with all kinds of mesh networks.

## Fractured PhillyMesh on the airwaves, unified PhillyMesh in our hearts

This is not a change we're introducing lightly. Many of us have poured time, energy, passion, tears, and money into testing Meshtastic nodes and settings. We want to ensure that you (the mesh users), the PRM Ops Division, and especially the gracious hosts of our infrastructure nodes do not run astray of FCC regulations. 

Large mesh networks like PhillyMesh rely on the power of numbers and agreement between its users to work. We each rely on each other's nodes to relay our messages. Most of us remember the days when you'd leave a node in your window and not see another node for weeks. **We knew a default preset change was coming and that it would cause our mesh to become fragmented, whether we wanted it to or not**. 

We had been preparing for that preset change, like many other metro areas have been doing, by testing to find a preset that works best for our area. Now, with the FCC regulations becoming more clear, we realize that our previous choice of the best preset is no longer an option. **We think that our best hope for FCC-compliant survival in the short term is MeshCore 500**.

Love,

The PhillyMesh Operations Division

# MeshCore and Meshtastic FCC-Compliant Settings

## MeshCore

*These are the settings we're recommending for MeshCore 500. They are FCC-compliant and avoid the heaviest ISM band interference that we found during our testing in the Philadelphia area. Please make sure your MeshCore node is updated to the latest firmware before using these settings!*

- Frequency: `902.250 MHz`
- Bandwidth: `500 kHz`
- Spreading Factor: `11`
- Coding Rate: `4/5` (some apps may just say `5`)
- Path Hash Mode: `1` (2-byte mode, some apps list this setting as `1-2 byte`)

We also wrote these pages that might be of help if you're new to MeshCore:
- [What you need to know about MeshCore coming from Meshtastic](https://phillymesh.net/2026/09/02/meshcore-intro)
- [How to flash MeshCore coming from Meshtastic](https://phillymesh.net/2026/09/02/how-to-flash-meshcore)

## Meshtastic

*These are the new default, FCC-compliant settings, that the Meshtastic project recommends for the US. Please update your firmware to the latest stable/beta version first!*

- Frequency: `908.75 MHz` (this is the default slot, which you can enter as `0` or `14`)
- Preset: `LongTurbo`

# FAQ

I'm sure you have a lot more questions! Hopefully we answer a good number of them below, otherwise please ask/vent/grieve the loss of 250 kHz bandwidth in the Discord.

**Q. What is this "PhillyMesh Operations Division"/"OpsDiv"? Just who the heck are you folks?**

A. The PhillyMesh Operations Division is some of the OGs from the Philly Radio&Mesh Discord server. The name "Operations Division" came about because the server admin is a Trekkie, and she couldn't resist the name. If you've seen anyone teach a class about Meshtastic, foot the bill for the website, table for the group at a local event, organize a PhillyMesh happy hour, or coordinate an infrastructure node install with another local org; that was one of the Ops folks. Feel free to bribe us with good node locations, bad puns, and Malort.

**Q. What are presets and what is LongFast?**

A. Meshtastic has many settings that allow you to change what slice of frequency you send messages in. You can customize these settings almost indefinitely, but most of the time people choose between a few different presets which are a standardized set of settings. Other Meshtastic users must (for the most part) have the same settings as you in order to receive your messages and be on the same mesh network.

Meshtastic's default settings are a preset called LongFast. This preset uses a bandwidth of 250 kHz, which we now know is in violation of FCC regulations.

**Q. Can you tell me more about this bandwidth thing?**

Meshtastic (and MeshCore) packets are sent across a frequency spectrum. That spectrum is determined by choosing a starting frequency (or, with Meshtastic, you often choose a "Frequency Slot" and the firmware uses that to [calculate your starting frequency](https://meshtastic.org/docs/overview/radio-settings/)) and then setting a bandwidth which determines how large the range of the spectrum wil be. For example if your frequency is 906.500 MHz and your bandwidth is 250 kHz (0.250 MHz), you will be transmitting from 906.500 MHz to 906.750 MHz.

The only preset that uses a 500 kHz or higher bandwidth is LongTurbo, the rest use 250 kHz. In our region there is a lot of interference put off by devices using RFID, among many other things. The interference exists every 250 kHz (at the .000, .250, .500, and .750 points of each frequency) and is strongest at .250 and .750. Using a smaller bandwidth like 250 kHz, Meshtastic packets are able to keep that interference at the edges and not be affected too much by it. However, because LongTurbo uses 500 kHz, no matter what starting frequency is chosen, it will always overlap with some of the interference. 

**Q. Who is the FCC and why do I care about them?**

A. The FCC makes and enforces the regulations regarding which frequency bands people and companies can use and what the rules are for the packets they send. As with all regulations in the US, it's possible to get in trouble for unknowingly violating them (regardless of motive/intent), and that's what we've all been doing while using Meshtastic on LongFast.

The FCC requires all packets sent in the ISM band (the band Meshtastic and MeshCore use) to have a bandwidth of 500 kHz or more. The only Meshtastic preset that uses a 500 kHz bandwidth is called LongTurbo, and that's now what the Meshtastic project will be suggesting as the default in the US. The default MeshCore setting uses a 62.5 kHz bandwidth and is even less compliant, hence the custom settings to use a 500 kHz bandwidth.

**Q. Is this a new FCC regulation?**

No. It seems that most people did not understand the FCC regulations. This includes Meshtastic devs, MeshCore devs, and device manufacturers selling devices where the default settings were out of compliance. 

There was a misunderstanding among users that did read the regulations about how Meshtastic was operating, FHSS mode vs DTS mode, and the regulations are different for each. Those users who didn't read the regulations figured if a project as big as this one was not in compliance with the FCC, we'd know about it. Well, now we know.

**Q. Does the FCC even care if we keep using Meshtastic LongFast? We've been violating regulations this whole time and no one got in trouble.**

A. At this point we don't know what enforcement the FCC will have for these regulations. You, as an individual, can make your own determination if you want to continue to operate on Meshtastic LongFast and be in violation of FCC regulations. It is important to note that if you are a licensed ham radio operator your license could be at risk for knowingly operating devices in violation of FCC regulations. The risk of punishment for past actions is probably low in this case, however, you are now aware and must make your own decisions going forward. 

As the group that is Philly Radio & Mesh, we feel it is important to stay in compliance for many reasons. Besides the obvious fact that violating FCC regulations is illegal, we have been partnering with non-profits such as Philly Community Wireless to host nodes, and we don't want to get them or any of the building owners in legal trouble. We've been asked by local businesses and libraries to do talks about Meshtastic; we can't in good conscience encourage new users to try something that we now know is illegal, and if people think we're doing that, we won't be asked back. Many of us are also licensed ham radio operators, and don't want that hobby to be put into jeopardy by affiliation with this group. Even for non-hams, using the ISM band irresponsibly could result in the privilege of using that spectrum being revoked for everyone, especially in today's environment of companies looking for spectrum to pivot to cellular 5G use.

**Q. What is MeshCore?**

A. Meshtastic is a project that allows you to send messages over LoRa. There are other projects that do the same thing, one of which is MeshCore. 

MeshCore and Meshtastic have recently grown side by side, learning and improving based on the other's work. In general, MeshCore has been optimized for nodes to be placed in a stationary routing and learns what the most efficient way to route messages between nodes is to get the furthest reach. Meshtastic has historically assumed that all nodes are mobile and hasn't added that routing part until recently. 

In Philadelphia, Meshtastic has historically been more popular. In other areas, such as NE PA, MeshCore is more popular. And as an individual, it's always more fun to join a mesh network that has more people on it, so the popularity is self-perpetuating.

More details about why we think MeshCore 500 is performing better than Meshtastic LongTurbo are in another FAQ below.

**Q. What is MeshCore 500?**

A. Most people on MeshCore operate at a 62.5 kHz bandwidth (these are the USA default settings), which, it turns out, is also in violation of those pesky FCC regulations, but the technology supports a 500 kHz bandwidth just like Meshtastic does. We have been calling using MeshCore at 500 kHz "MeshCore 500" to differentiate it from the usual MeshCore at 62.5 kHz settings that most people are currently using.

**Q. I don't want to try out MeshCore, but I do want to make sure I'm in compliance with the FCC. What should I do?**

You should switch your Meshtastic node's preset to LongTurbo. We recommend leaving your other frequency settings at default, so you can see as many other people on LongTurbo as possible. You will soon also see our dual-radio infrastructure nodes on Meshtastic LongTurbo as well, but the single-radio nodes will be on MeshCore 500.

**Q. Do I have to pay to use MeshCore?**

No. MeshCore, unlike Meshtastic, has many third-party apps you can use to interface with your nodes. Some are paid and some have paid features, but there are some great ones you can use that are entirely free.

Dusty, who has been using MeshCore for a while, recommends the apps [MeshCore One](https://apps.apple.com/us/app/meshcore-one/id6757419477) for iOS and [MeshCore Open](https://play.google.com/store/apps/details?id=com.meshcore.meshcore_open) for Android. Both are entirely free to use. 

If you're a power user, [RemoteTerm](https://github.com/jkingsman/Remote-Terminal-for-MeshCore) is a docker app like MeshMonitor and Kyle Yank has set up an instance of [CoreScope](https://corescope500.phlm.sh/#/packets), which is like Malla. Feel free to turn MQTT on and contribute (as long as you're on 500 kHz).

**Q. Can licensed amateur radio operators continue to use Meshtastic and MeshCore at 250 kHz?**

A. Yes. However, using Meshtastic as a licensed amateur radio operator requires you to not use encryption which means dropping packets from private channels and only using the default public channel (with the published key of AQ==). Setting your node to "ham mode" will do all of these things.

This is not compatible with the default Meshtastic network and won't allow you to chat with non-licensed users on LongFast. If you're intersted in getting your ham radio license, JawnCon, Philly's local cybersecurity conference in October, has free classes and exams most years.

Amateur radio has several alternatives to the ISM band that have similar messaging functionality, including normal VHF APRS, UHF, LoRa APRS, FT8 (and derivatives), JS8 Call, VARA modes, Winlink, etc. Ask your friendly neighborhood ham in #amateur-radio in our Discord to learn more.

**Q. What settings are being recommended for MeshCore 500?**

A. Some MeshCore apps have recommended presets and some don't, but there are generally agreed upon default settings that most people use so they can communicate with each other. Those settings use 62.5 kHz as the bandwidth, which is in violation of FCC regulations.

We have outlined our custom settings in the next section below, which use a 500 kHz bandwidth. This means that, for the time being, the only other MeshCore nodes you'll be able to communicate with are folks who heard about these settings from PhillyMesh. We do anticipate that once word gets out about the FCC regulations, we will see some current MeshCore users transition to 500 kHz bandwidth and find us. We are not making this change to be isolated or exclusionary, we are making this change for FCC compliance and sharing the settings that worked best in hopes of re-connecting with neighboring meshes again.

MeshCore's reach is much wider than Meshtastic LongFast; the current most widely used (and non-FCC-compliant) settings result in Philly being reachable from as far north as New Hampshire and as far south as Kentucky, depending on the weather (check [Kyle's instance of CoreScope that uses MeshCore's default settings](https://corescope.mesh.yankani.ch/#/home) to see all the repeaters he's seen recently and you'll get an idea of the reach). In order to keep the community we've had on Meshtastic LongFast together, we recommend everyone joins the #prm channel and uses that as the default comms channel. Once other meshes join our settings and the Public channel gets busy again, #prm can be a way to ensure our area's unique culture has a home.

**Q. Why do we expect MeshCore to perform better at 500 kHz than Meshtastic does?**

MeshCore has some key benefits compared to Meshtastic that will increase chances of success at this wider, more interference-heavy bandwidth.

- <u>Reduced Non-Message Traffic</u>. Baked into the firmware are the settings we were asking Meshtastic users to change as part of this summer's tests to reduce position reporting, telemetry, NodeInfo, etc. Without these packets clogging the mesh, there is more room for messages to reliably flow.
- <u>Higher Hop Limit</u>. Where Meshtastic had a hop limit of 7 (and realistically only 4-5ish hops were viable), MeshCore has a hop limit of 64. We won't need all 64 of those hops to talk across the Philly Mesh, but we know we will need more than the 4-5ish viable hops Meshtastic had. An increased hop limit will increase the functionality of the mesh to counter the degradation of node transmit/receive distance at 500 kHz bandwidth.
- <u>Better Routing</u>. MeshCore prioritizes static routing compared to Meshtastic's ad-hoc flood routing. There is still flood routing in MeshCore, but it uses it sparingly and instead focuses on building stable paths from router-to-router to reduce unnecessary retransmits. This means many nodes, especially in Center City who can reach a repeater, can stay in Bluetooth Companion mode (the equivalent of CLIENT_MUTE in Meshtastic). The reduction in unnecessary rebroadcasting also helps reduce packet collisions and noise floor, also mitigating the impacts of the higher interference on the 500 kHz bandwidth.
- <u>Better Battery Life</u>. Because most nodes in Center City can stay in Bluetooth Companion mode, they won't unnecessarily waste battery life rebroadcasting. This is a significant win for battery-run nodes, pocket nodes, small solar nodes, etc as they will live longer.

And we've seen this in practice. Compare our [Malla instance (Meshtastic)](https://api.phillymesh.net/map) to Kyle's [CoreScope instance (MeshCore)](https://corescope.mesh.yankani.ch/#/map). While on Meshtastic we see a couple of nodes further away, these are likely to be airplane nodes, or nodes that had their location incorrect. On MeshCore we see hundreds of repeaters further north than New York City and a handful down in North Carolina.

**Q. Could we just roll our own Meshtastic firmware to make Meshtastic on 500 kHz perform better?**

A. We actually thought about this; we've been joking about making MalortCore for a while. However, in order to make Meshtastic on 500 kHz perform better we'd be doing things like increasing the number of allowed hops and improving routing, and we'd basically just be recreating MeshCore. We'd rather spend our energy building out local infrastructure that will benefit everyone in the area, instead of developing and administrating a third competing LoRa mesh project, which would just serve to further fragment the PhillyMesh. 

**Q. I haven't seen anything about a new Meshtastic preset. What's your sourcing on this?**

A. It seems a lot of this discussion has been happening in private Discords, so sourcing this is hard. However, it became clear when we saw that starting in Meshtastic version 2.8, the Meshtastic firmware will [default to LongTurbo for users in the US](https://github.com/meshtastic/firmware/pull/11637). Mobile apps will warn users on the LongFast preset that their preset is violating FCC regulations and push them to move to LongTurbo. We believe this will cause many Meshtastic users, especially new ones, to use Meshtastic LongTurbo and effectively kill the current default Meshtastic LongFast network.

Meshtastic's leadership has discussed on other Discords that further "friction" will come in version 3.0 and later.

**Q. Did some people know about this? It's suspicious that we did LongTurbo tests a month before we found out that LongTurbo is the only legal default.**

A. Some folks who follow the Meshtastic firmware GitHub repo and are part of other Meshtastic Discords had heard rumors that the default preset might be changing. No one knew why; we're not even sure if the default preset change was because of the FCC regulations or because of [this meshtastic.org post](https://meshtastic.org/blog/why-your-mesh-should-switch-from-longfast/) about LongFast not being the best default for cities. 

We realized this default change would fracture the mesh significantly and our Discord would play a key role in informing users about the changes and helping support users change their existing nodes. We thought about it and decided to take the opportunity to not blindly trust the new recommended default, but to find a preset and custom settings that would actually improve PhillyMesh's performance.

It wasn't until we saw [version 2.8](https://github.com/meshtastic/firmware/pull/11637) and [this heated discussion in the MeshCore Github](https://github.com/meshcore-dev/MeshCore/issues/945) that the violation of FCC regulations became clear. This resulted in a few days of waiting to see if the Meshtastic project would say anything about it before we decided to stop waiting and make this post ourselves.

**Q. Shouldn't someone be fixing this?**

A. Meshtastic is a global project. Many of the developers are based in Europe, where the regulations are actually the opposite (in their 433 MHz frequency band the bandwidth must be less than 500 kHz). Only a small subset of the devices that hardware manufacturers sell are being used for Meshtastic, so they leave it up to the users to make sure their devices are in compliance. If there is a better solution to this issue, such as a different frequency band to use in North America for Meshtastic, we don't see it arriving quickly.

**Q. Could lowering the power on Meshtastic transmissions allow us to still have a bandwidth of 250 kHz and be FCC-compliant?**

A. Yes, but we're pretty sure it would have to be lowered so much that Meshtastic LongFast would be completely useless. Some math by one of our members, KT3H, says that the power would be limited to something like 0.0006 Watts, which is tiny compared to the ~1 Watt we have been using. Lowering the power on Meshtastic LongFast that much would severely compromise our ability to communicate using Meshtastic. Messages wouldn't be able to travel as far and the mesh would perform significantly worse. Using Meshtastic LongFast at a fraction of the power would be even worse than using Meshtastic LongTurbo.

**Q. That 0.0006 Watt number is very specific, how did you calculate it? Also, what are the actual regulations we're discussing here?**

A. Our understanding of the regulation is as follows (with the usual caveat that we are not lawyers and are awaiting official word on guidance): Unlicensed operation in the 902 MHz band is governed by 47 CFR Part 15 Subpart C. There are two sections that apply, and you must pick one to operate under. Under §15.247 the bandwidth must be no less than 500 kHz, but the power can be up to 1 Watt. Under §15.247 there is no bandwidth restriction, but the maximum field strength is 50 mV/m at a distance of 3 meters. This is equivalent to an output power of 0.0006 Watts.

**Q. Can we move to another frequency band that has different regulations?**

A. Potentially. But that would require, first, a research effort to find one compatible with the Meshtastic project. Second, it would almost certainly require purchasing new antennas for all our nodes. And third, it would likely require us to purchase entirely new nodes (which would first need to be designed and manufactured) that are compatible with the new frequency. Unfortunately, we don't see that happening anytime soon.

**Q. Is there a chance the FCC will change their regulations?**

The FCC is largely concerned with regulating the frequency bands that they license for commercial use. While using amateur bands brings us nerds a lot of joy, it actually results in less money in licensing for the government. Furthermore, [NextNav has been lobbying the FCC](https://meshtastic.org/blog/meshtastic-opposition-to-nextnav-proposed-changes/) to further restrict amateur usage of the 900 MHz ISM band and reserve parts of it for commercial use. We consider ourselves lucky that NextGen hasn't succeeded thus far, and unless an independently wealthy Meshtastic user wants to fund their own lobbying campaign, we see a change in FCC regulation to be unlikely.

**Q. Do we expect Meshtastic LongTurbo to perform better in the future than it did during our testing?**

A. We do expect Meshtastic LongTurbo to perform marginally better once more people switch over to it. We didn't have a large number of nodes participating in this test, and because LongTurbo messages don't go very far we needed more nodes than we had to get a proper mesh going. We expect that as Meshtastic LongTurbo adoption increases (and as we install more well-placed infrastructure dual-radio nodes that support LongTurbo) we will be able to communicate better over short distances using LongTurbo. The reason we're also focusing on building out MeshCore at 500 kHz is because those messages seem to be able to go a lot further, and that gives us the best shot to be able to communicate across our wide metro area, from Jersey to Delco and beyond.

A core goal of the group is to be accessible to those who are new to mesh networks and be in touch with whatever is most used in our area. That's why our dual-radio infrastructure nodes will have one radio tuned to whatever the current Meshtastic default preset is (as long as it's FCC-compliant) and the other will be on MeshCore at 500 kHz. We may move somewhere else in the future, but that's what we expect to be using until the next big revelation or new technology release.

**Q. I have a good place for a node, or a resource/skill I can bring to PhillyMesh!**

A. Please let the Ops Division know by tagging @PhillyMesh Operations Division on Discord! For node locations to be officially associated with PhillyMesh, you must have explicit permission from the property owner to install the node, and if you have internet and/or power at the location that's a huge plus.