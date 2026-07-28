---
title: Frequency Testing Explanation
author: Emily Boda (BODA)
type: page
#cspell:ignore PMXX
---

This is a primer on why we will be testing different Meshtastic frequencies and what that means. The instructions for the new settings and full details about the test can be [found here.](/freq-test-instructions/)

## What's going on?

On Saturday, August 1st at 10pm a group of organized Philadelphia Mesh users will be switching from the default frequency preset to a custom one to test if custom presets are more reliable than the default. We welcome you to join in on our test and help us improve the Philly Mesh!

Test 1: Aug 1st at 10pm to Aug 8th at 10pm we will be testing MediumSlow 22

Test 2: Aug 8th at 10pm to Aug 14th at 10pm we will be testing LongTurbo 12

In addition to the different preset and non-default frequency slot, there are some other settings you're required to change if you want to participate in this test. [Please view the full instructions with screenshots here](/freq-test-instructions/) to participate.

Not sure what all this means? Read on as we attempt to explain what this all means for you, if you're new to Meshtastic and frequencies.

## First, here's some background on how Meshtastic works…

In the United States, Meshtastic uses the 915MHz frequency band. This is a range of frequencies from 902-928 MHz that is set forth by the FCC (the governing body for the airwaves) as a band in which unlicensed people and devices can communicate with their radios.

In order for your Meshtastic radio to communicate with another Meshtastic radio, those two radios must be communicating on the same frequency and some other Meshtastic settings (such as bandwidth) must also be the same. 

Since there's a wide range of possible frequencies and settings, the Meshtastic project has created "presets". These presets are combinations of a chosen bandwidth and several other settings that allow users to have a shorthand for which settings they're going to use. These settings are used by the Meshtastic firmware to calculate which frequency you will be on.

These presets are optimized for two things: the distance your messages will travel (either Long, Medium, or Short) and how fast they will be sent (Fast, Moderate, Slow, and Turbo).

There are also some physical (over the air) benefits to using different settings combinations. 

- A lower coding rate allows messages to be sent with a smaller amount of data, whereas a higher coding rate adds redundancy to error-correct for noise (at the cost of more data needing to be sent). 
- A higher bandwidth gives more allocated airspace for the messages to be sent, meaning they can be sent faster at the expense of shorter distance (kind of like going from a narrow 20 MHz channel in 5 GHz Wi-Fi to a wider 80 MHz channel).
- A higher spreading factor (SF) allows messages to be picked up a further distances because it uses more airtime, similar to speaking slower lets others hear you more clearly than speaking very quickly.
- You can take a look at [the preset table in the Meshtastic Docs](https://meshtastic.org/docs/overview/radio-settings/#presets) to see how these settings affect the Long-Short and Turbo-Slow scales.

While most users choose to use one of the default presets and their accompanying default frequency slots, some users may wish to have their own "private mesh". This means they set all their Meshtastic devices to the same random frequency slot and preset combination, in hopes that no other nearby users have picked the same combo so that they only communicate with their own devices.

## What preset am I using now?

The default preset for the Meshtastic project is called Long Range/Fast, also known as Long/Fast, LF, or LF20. This is accepted to be the best "all around" default. The default frequency slot for Long/Fast is 20 (hence the "LF20" moniker) which, if you're curious, results in your frequency being centered at 906.875 MHz.

Check out [this calculator](https://meshtastic.org/docs/overview/radio-settings/#frequency-slot-calculator) if you want to see what the frequency is for other preset/slot combinations.

## Why are we considering changing this?

Long/Fast works great for a sparse mesh, but at some point when there are enough Meshtastic devices trying to communicate with each other, we start running out of bandwidth to reliably send and receive messages. 

In Philadelphia, as of July 2026, we have about 400-500 nodes on the mesh any given week, and that number is increasing every month. Even if the users of these nodes aren't sending messages to each other all at once, these nodes are sending periodic pings in the background about who they are and asking for information from all the other nodes. This results in a congested mesh that doesn't perform as well as it could, impacting message reliability and reach.

This means you're more likely to attempt to send a message and see "Max retries attempted". This usually indicates that your message wasn't received by another radios, but in a congested mesh it can also indicate that your radio never received an acknowledgement that your message was seen by another radio, even if it was. On the receiving end, you may miss a significant percentage of messages and there is no way to know that you haven't received a message that others have seen.

This makes Meshtastic a less reliable communication method, and it also makes it pretty frustrating to use, defeating the goals of the technology and this community we've developed to support and advance its use.

## Success stories

At Defcon each year, there are so many radios in the span of only a few blocks, that the default Long/Fast preset doesn't work at all. Messages are often sent and not acknowledged or even received by other nodes that are right next to them. As a result, the Meshtastic developers create a custom firmware each year that includes custom settings that are optimized for this environment. 

It is usually a super-charged version of the Short/Turbo preset. The move from Long to Short is because, on average, the next Meshtastic device is about five feet away from you, so the messages don't have to be sent very far. And the move from Fast to Turbo reduces the amount of airtime used by each message, freeing up the airwaves faster for the next message. While cities don't usually have nearly that many radios in one location, dense urban areas with a lot of nodes do see similar problems.

Other metro areas have shown that using a preset other than Long/Fast can improve Meshtastic's reliability. The Bay Area switched to Medium/Slow a few years back and saw a big improvement in their mesh performance. New York City has also been experimenting with Medium/Slow and seen good results. Some of these successes were outlined on the Meshtastic Blog in this article from 2025, [Is LongFast Holding Your Mesh Back? Better LoRa Presets for Bigger Meshtastic Networks](https://meshtastic.org/blog/why-your-mesh-should-switch-from-longfast/).

There is also some talk that the Meshtastic project as a whole will move from Long/Fast to Long/Turbo as the default for all new nodes. This would be a big change, and nothing concrete has been announced at this time, but it does seem to be the way the project is moving. 

## Ok, so back to this test. What's going on?

Our ultimate goal is to switch to settings that increase the reliability of the mesh. The first week we are testing Medium/Slow and the second week we're testing Long/Turbo. For both tests we're also choosing a non-default frequency slot in hopes that we won't encounter any existing nodes using those frequencies and that future new nodes will make deliberate changes recommended here to ensure continued reliability of the Philly Mesh.

We're also requiring users to change other settings that aren't related to the actual frequency, but will also free up airtime for more messages to get through. These include reducing or eliminating telemetry and position messages that your radio sends behind the scenes, depending on the node's role or setup.

If you'd like to participate in this test or find out more about the settings, please check out the full instructions with screenshots [here](link to full instructional article).

After the test is over, there will be a period of transition where either the participating nodes change back to Long/Fast 20 aka LF20 (if the test was unsuccessful) or switch to one of the new presets.

## What if I don't want to or can't change my settings?

You're not required to! There are many reasons you may not want to participate in the test. You may not want to abide by the requested settings for telemetry and position. You may have nodes that you've placed in locations for which it is difficult to change the settings. You may enjoy the wild-west nature of the default mesh and want to stick around to see where it goes. You may live on the border between Philadelphia and another mesh that uses Long/Fast or some other preset.

You can always try out both the custom and default meshes during the weeklong tests. If you have more than one node, feel free to set one to the test preset and keep one on default.  

Whether you stay with the default Long/Fast or move to the custom presets, you will likely experience a better performing, less congested mesh because we are splitting the mesh up and your instance of it will now have less nodes using it. However, there could be an unintended disadvantage to you personally, depending on which nodes you interface with regularly. 

Nodes that are labelled PMXX will be participating in the test, so if you are counting on those nodes to relay your messages to the rest of the network, and you are now on a different preset as them, you may be cut off from the rest of the mesh during the test and in the future. Remember that nodes on different presets cannot communicate with each other.

Conversely, you may have the opposite problem if you'd like to participate in the test, but count on a node that isn't participating to connect you to the rest of the mesh. Before the tests start, we won't have a list of nodes that will be participating and ones that will not. You'll have to find out along with us when the tests start! 

## What happens when the test is finished?

Depending on the outcome of the tests, a large group of nodes may be moving to a new frequency. This will be discussed at length in the [PhillyMesh Discord](https://discord.phlm.sh) and your participation in the discussion is welcomed and encouraged.

If a majority of PhillyMesh members decide to make a new frequency our home, we will publicize this and make it as easy as possible for users new to our area and/or Meshtastic to follow us there if they so please. There will likely always still be a large number of nodes on Long/Fast as long as that is the default setting in the Meshtastic firmware.

We wish to welcome as many PhillyMesh users to participate with us, but we also encourage you to use the mesh how you want to use it! A happy byproduct of moving a large number of nodes to a new preset is opening up more airspace for experimentation and learning to those left on the default Long/Fast preset.

We (the PhillyMesh website and Discord admins) intend to use this platform for good and make sure no one feels left out. We will continue to make sure that new Meshtastic users understand all their options and feel as welcomed as possible to the radio waves. 

[Full test settings and instructions are here.](/freq-test-instructions/)
