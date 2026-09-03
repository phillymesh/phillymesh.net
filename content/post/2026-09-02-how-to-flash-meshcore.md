---
title: How to Flash MeshCore
author: Someone else
type: post
date: 2026-09-02T00:00:01+00:00
url: /2026/09/02/how-to-flash-meshcore/
categories:
  - Philly Mesh
tags:
  - meshtastic
#cspell:ignore Meshtastic meshcore RemoteTerm ops div opsdiv
---

# How to flash a Meshtastic node to MeshCore

1. Back up your previous Meshtastic settings
    - Before doing anything, it is recommended to backup your current Meshtastic node config. From your phone app while connected to your Meshtastic node, go to Settings > Export Configuration, select all toggles, and then save that .cfg file somewhere safe.
    - If ever you want to change your node back to Meshtastic, you can use this config file with the “Import Configuration” to more quickly return it to its current state.
2. Grab your node and a GOOD data-enabled USB cable
    - Same operating experience as firmware updates via serial, you’re going to want a good cable that enables data transmission (many cables are charge-only). If you have a cable that worked for Meshtastic flashing, it should work for MeshCore as well.
    - So many instances of “flashing failed” are cable-related. If the thing is old, wobbly, been chewed on by your cat, filled with lint, been through the washing machine, been used by Gritty, etc … get a better cable, otherwise you’re gonna have a bad time.
3. Plug your node into your computer. If it’s USB-A, it’s upside-down, flip it. Now flip it again. GUESS WHAT, IT WAS RIGHT THE FIRST TIME, flip it one more time.
4. Go to [https://flasher.meshcore.io/](https://flasher.meshcore.io/)
5. Find your exact node (exact model) and click on it. If you can't find your exact model, ask in the Discord.
6. Select device role
    - Unlike Meshtastic where you could change between CLIENT and CLIENT_MUTE in the app, MeshCore requires specific firmware for each role.
    - If you only have one single device/node, select “Companion Bluetooth”.
    - If you have a multi node setup, for the powerful/stationary node (e.g. the node on your roof, in your tree, in your attic etc) you’ll select “Repeater”. And for the pocket node, you’ll select “Companion Bluetooth”. Note that Repeater nodes cannot be connected to nor configured over Bluetooth, they must be initially setup via USB serial (during this process) and then can be remotely administered later over LoRa.
7. nRF nodes only
    - There is a warning at the top that says “We strongly recommend installing OTAFIX BOOTLOADER … for more reliable Bluetooth OTA DFU.” Click on “OTAFIX BOOTLOADER” and it will download a .uf2 file that does this. Follow the instructions here: [Installing the OTAFix Bootloader - MeshCore Blog](https://blog.meshcore.io/2026/04/06/otafix-bootloader). When it comes time to update the node, you will be happy you did this.
    - Click “Enter DFU Mode” (in theory there is no need to double click the reset button anymore). If nothing happens (no pop up), ensure you are using a Chromium based browser like Chrome or Edge.
    - When the pop-up with devices shows up, select the COM port of your device. It is typically something like “nRF Serial” but may be something different depending on your device. When it is connected, the previous “Enter DFU Mode” button will now have a check and say “DFU Mode Active”.
    - Click “Erase Flash”. When complete, a popup will show “Device erase firmware has been flashed and flash has been erased. You can flash MeshCore now.” Click OK.
    - Click the Flash button. A similar popup with COM ports will allow you to select the device. A warning that the COM port number and/or device name may have changed now that it has been erased.
    - A new page will open with a progress bar showing the flashing. DO NOT CLOSE THE WINDOW when done if setting up a Repeater. Proceed to Step 9 or 10 depending on device role.
8. ESP32 nodes only
    - Select “Erase Device” because the current firmware on your node is Meshtastic and must be erased.
    - Click “Flash”
    - In the pop-up, select your node based on the COM port. Click OK.
    - Watch the progress. Beware that erasing flash may take some time (minutes) where it appears little progress is occurring. It will then progress to flashing. DO NOT CLOSE THE WINDOW when done if setting up a Repeater. Proceed to Step 9 or 10 depending on device role.
9. Companion Bluetooth nodes only
    - After flashing in either Step 7 or 8, disconnect the node from your computer and connect to your node via bluetooth. If the device has a screen, the PIN is displayed there as a randomized six digit number. If the device has no screen, 123456 is the default PIN.
    - Setup the node per the “MeshCore and Meshtastic FCC-Compliant Settings” section below.
    - Location (lat/long) can be set in your app of choice, with the map icon being the easiest to set a static location (press and hold and then select “set as my location”). Note that the location does not get fuzzed like in Meshtastic, please do not use your exact home address if you are not comfortable doing so.
    - In your app of choice, look for a setting similar to “sync/set device clock to phone time” and click it. MeshCore can be weird with time settings, it is a good practice to occasionally do this so your node’s clock doesn’t become too out-of-sync with the mesh.
10. Repeater nodes only
    - After flashing in either Step 7 or 8, DO NOT DISCONNECT the node from your computer. Initial settings must be made over serial first!
    - Click on “Configure via USB”.
    - A new window will pop up. Click “Connect” in the top right. Yet another pop up will let you select the device via COM port, and yet again the number and/or name may have changed.
    - The repeater setup page has a few settings you MUST setup before you disconnect, we’ll start with those:
        - Under ACCESS, create a new admin password and keep it somewhere safe. This is how you will access your repeater via LoRa. If you lose this, you can’t get back into the repeater without plugging it back into your computer again.
        - Under RADIO SETTINGS, change the settings to match “MeshCore and Meshtastic FCC-Compliant Settings”. These settings (freq, bandwidth, SF, coding rate) must match your companion node for the two to see each other. It’s also where you tell the repeater to match the settings as the rest of MeshCore 500. 
        - Click SAVE SETTINGS at the bottom. A toast message with “Data successfully saved” should pop up for a second.
        - At this point you can disconnect your Repeater and configure the rest over LoRa if you wish. Or finish setting it up here (because it’s easier to type via computer).
    - The remainder of these settings are optional via USB but preferred for ease on a computer.
        - Copy the Public and Private keys and keep them somewhere safe.
        - In NAME & LOCATION, at least change the name to something unique. A warning that when you set the location (now or later on) it will truncate the name from 32 bytes to 24 bytes.
        - Location (lat/long) can be set here, with the map icon being the easiest to set a static location. Note that the location does not get fuzzed like in Meshtastic, please do not use your exact home address if you are not comfortable doing so.
        - Under ADVERTISING, change the Advert Interval to 240. Leave the Flood Advert at 47.
        - In Owner Info, feel free to put in your Discord username or Ham call sign or leave it blank, whatever you’re comfortable with!
        - Click on the SHOW ADVANCED SETTINGS checkbox and change LOOP DETECTION to Minimal. Change PATH HASH MODE from 1-byte (0) to 2-byte (1).
        - Hit SAVE SETTINGS in the bottom left.
        - Hit Reboot in the top middle (some of the settings don’t take effect until after a reboot). Rebooting also has the effect of disconnecting the device from the computer. You can now unplug and place the repeater back into its strategic location!
    - In your app of choice, look for a setting similar to “sync/set device clock to phone time” and click it. MeshCore can be weird with time settings, it is a good practice to occasionally do this so your Repeater’s clock doesn’t become too out-of-sync with the mesh. Some apps have a setting to enable this to automatically occur.
11. For any step, when in doubt, feel free to reach out! We’re happy to help on the Discord.
