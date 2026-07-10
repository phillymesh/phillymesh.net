---
title: "Cat Solar Node"
date: 2026-05-24T22:00:12-04:00
author: Joe Mac
draft: false
---
## Introduction
The solar light used for this build has distinctive 'cat ears', giving this build its strange name.
You will need to purchase [this solar light from Amazon](https://www.amazon.com/dp/B0FKGR8YS1), approximately $7 per light.

Case dimensions: 5"(h) (not counting antenna height) x 4"(w) x 4"(d) (to rear of the mounting post).

Solar panel dimensions: 4 3/8" x 2 1/4"

![Solar light being measured from different angles](images/uploads/2026-05-24-cat-solar-node/Intro.png)

This is a simple build and the case pairs perfectly with the RAK 4631 Mini board. Do not get the larger 4631 on the 19007 base because it's too large and will not fit.

The case includes an 18650 1200 mAh battery which works great with the RAK 4631. The lowest the battery level I've seen on 2 cloudy days is 85%.

Note: the pictures here show an upgrade battery because this node is going to be remotely deployed and I wanted a little extra fuel but I currently have 3 of these nodes running the stock battery and they work great.

Note: for this build you will need to do some soldering for the solar and battery connectors.  You will need to supply the following parts: RAK 4631 Mini, antenna port and your antenna of choice, silicone caulk, hot glue gun, drill and small drill bit, and a small desiccant (optional).


## Instructions

### Step 1: Remove Front Panel
Remove the 4 screws holding the clear front panel.
![Annotated photo of the front panel, with red "Remove" arrows pointing to the 4 screw holes](images/uploads/2026-05-24-cat-solar-node/Step-1.png)

### Step 2: Disassemble LED Board
Remove the 2 screws to free the LED light board (retain the screws; you will need 1 to mount the RAK 4631).
![Annotated photo of the disassembled front panel, with the focus lens crossed out as "discard"](images/uploads/2026-05-24-cat-solar-node/Step-2(1).png)

Cut the 4 wires attached to the board (2 for battery and 2 for solar).
![LED board with 4 cut wires attached. Black wires are connected to "S-" and "B-", a white wire is connected to "S+", and a red wire is connected to "B+"](images/uploads/2026-05-24-cat-solar-node/Step-2(2).jpg)
![Before and after cutting the 4 wires on the LED panel](images/uploads/2026-05-24-cat-solar-node/Step-2(3).png)

Note the polarity from the board - the solar white wire is positive and the battery uses standard red/black for +/-.
Check the battery and make sure it is secure with glue (most of mine were but a few were not so I used a hot glue gun to secure the battery).

### Step 3: Seal Weep Holes
There are 9 small weep holes that need to be filled with silicone:
- 4 on the back
- 2 on the top of the solar panel
 - not sure these are actual holes but I sealed them and recommend you do too
- 2 on the clear front lens on the bottom, opposite of each Cat ear
- 1 in the handle mount which requires removing the handle to get to the hole (see pic below).

![Remove rear handle mount and fill in hole](images/uploads/2026-05-24-cat-solar-node/Step-3(1).png)
!["Caulk Here" arrows pointing to the 4 holes on the back and 2 on the top](images/uploads/2026-05-24-cat-solar-node/Step-3(2).jpg)
![Arrow pointing to small hole on front lens](images/uploads/2026-05-24-cat-solar-node/Step-3(3).png)

### Step 4: Remove the Rubber Switch Grommet
Take advantage of the existing hole for the pusbutton switch by removing the rubber grommet.
This is where the antenna will be mounted.
![Tweezers grabbing rubber switch grommet and "Antenna port" pointing to the now exposed hole](images/uploads/2026-05-24-cat-solar-node/Step-4.png)

### Step 5: Solder Solar and Battery Connections Leads
Shrink wrap the connections and install the antenna connector in the existing hole.
![JST connectors installed for the solar panel and battery leads](images/uploads/2026-05-24-cat-solar-node/Step-5.jpg)

### Step 6: Update the RAK Firmware
After installing the included bluetooth and LoRa antennas, plug the RAK into a PC.
Flash the board with the latest build from the [Meshtastic Web Flasher](https://flasher.meshtastic.org/).
After updating disconnect the small LoRa antenna, but leave the bluetooth antenna connected.

### Step 7: Trim the Case
You will need to trim off a small tab next one of the mounting holes (see pics).
I used a pair of wire cutters to remove it.
Trimming this piece will allow the board to fit evenly.
Use one of the small screws that held the LED light to secure the RAK 4631 board in place.
The board will align with a screw mount inside of the case.
![Annotations indicating to cut the tab in the middle of the enclosure](images/uploads/2026-05-24-cat-solar-node/Step-7.png)

### Step 8: Connections
Connect the external antenna to the RAK, then connect the solar and the battery connectors to their appropriate ports on the RAK. Make sure the antenna is connected before the power!
Use the small screw that held the LED light in place to secure the RAK in place.

IMPORTANT: The RAK 4631 positive(+) is marked in red and goes on the inside (toward the center).  I had to repin the power connector for the correct orientation. Incorrect polarity will kill the board.
![Arrows pointing to the screw securing the board to the case, and highlighting the polarity of the power leads](images/uploads/2026-05-24-cat-solar-node/Step-8.png)

### Step 9: Add a Dessicant (Optional)
This step is optional but recommended.
Adding a small dessicant packet will help mitigate any condensation inside the case from temperature changes
![Dessicant packet on top of the RAK inside the case](images/uploads/2026-05-24-cat-solar-node/Step-9.png)

### Step 10: Add Silicone to Seal the Case
Apply a bead of silicone caulk around the inside groove of the case where the lens seats.
This step is very important because I found that the clear lens is not water tight and even though you will most likely be mounting it with the lens upside-down water can (and will) find its way in.
![Thin bead of silicone around the case edge](images/uploads/2026-05-24-cat-solar-node/Step-10.jpg)

### Step 11: Add Drainage Holes
Before mounting clear front lens, drill 2 small holes in the "Cat" ears to allow water to drain.
!["drill holes" pointing to two spots in the cat ear portions of the front lens](images/uploads/2026-05-24-cat-solar-node/Step-11.png)

### Step 12: Reassemble the Case
Install the 4 screws on the clear lens and apply silicone caulk over them.
!["caulk screw holes" pointing to the 4 holes in the front lens](images/uploads/2026-05-24-cat-solar-node/Step-12.jpg)

### Step 13: Caulk the Antenna
The orientation of the case will allow rain to contact the antenna port so I use a generous amount of caulk to insure the antenna port will not leak.
![External antenna with a lot of caulk around it](images/uploads/2026-05-24-cat-solar-node/Step-13.png)

### Step 14: Mounting
When installing the completed unit outdoor I use the round mount with 2 or 3 screws. I have installed these units on trees, fences, and even used rope for a high tree mount.
![final assembly mounted on a fence](images/uploads/2026-05-24-cat-solar-node/Step-14.png)

### Total Cost
- Solar light, including case, battery and solar panel - $6
- RAK 4631 Mini - $31
- Antenna - $7

Total $44 (does not include your supplied silicone caulk, shrink wrap, solder, connectors, or hot glue).