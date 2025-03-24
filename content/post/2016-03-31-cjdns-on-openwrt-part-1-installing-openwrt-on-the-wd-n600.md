---
title: 'CJDNS on OpenWRT – Part 1: Installing OpenWRT on the WD N600'
author: Mike Dank (Famicoman)
type: post
date: 2016-03-31T21:42:38+00:00
url: /2016/03/31/cjdns-on-openwrt-part-1-installing-openwrt-on-the-wd-n600/
categories:
  - Tutorial
tags:
  - firmware
  - n600
  - openwrt
  - Western digital

---
I was lucky enough to snag a <a href="http://www.amazon.com/N600-Dual-Router-Wireless-Accelerate/dp/B007KZQM9G">Western Digital N600</a> router recently for $10 via Woot and have been working through the process of getting it configured with <a href="http://openwrt.org/">OpenWRT</a> and cjdns.

For $10, I didn’t think I was getting a whole lot, but these devices sport a popular Atheros chipset and are perfectly compatible with OpenWRT’s latest version (Chaos Calmer 15.05 at the time of writing). For the uninitiated, OpenWRT is an alternative firmware for routers that allows for an advanced set of features and more customization.

{{< figure src="/images/uploads/2017/03/20160331_214547.jpg" caption="My N600, happily chugging away." link="/images/uploads/2017/03/20160331_214547.jpg">}}

The first (and sometimes daunting) task in this process is to flash the firmware on to the device, but this is easy to accomplish with the help of the <a href="https://wiki.openwrt.org/toh/wd/n600">OpenWRT Wiki page for the N600</a>.

One issue I’ve found is that the page states that the web updater doesn’t work on most N600 devices and that it is preferable to use telnet. Being the console junkie I am, I tried the telnet method first but had no way to configure or enable it! I found I couldn’t use telnet but ultimately was able to flash via the web interface.

Adapted from the wiki, here are the steps I took to flash my device. Any additions/modifications by me are in **bold**:

> **0) Turn on and configure the device. I couldnt do anything until i completed the initial setup.**  
> 1) Download the file openwrt-ar71xx-generic-mynet-n600-squashfs-factory.bin. **I pulled it down from https://downloads.openwrt.org/chaos_calmer/15.05/ar71xx/generic/openwrt-15.05-ar71xx-generic-mynet-n600-squashfs-factory.bin**  
> 2) Configure your computers IP address to 192.168.1.10 and connect to a LAN port in the router.  
> 3) Turn the router off.  
> 4) Using a paperclip, press and hold the reset button on the bottom of the router and turn it on. Hold the reset button for at least 15 seconds. Wait until the power light on the front is slowly flashing on and off.  
> 5) On your computer, visit http://192.168.1.1 NOTE: You will not be able to ping this address.  
> 6) Upload the file openwrt-ar71xx-generic-mynet-n600-squashfs-factory.bin as downloaded earlier.  
> 7) The router will now flash OpenWRT. This will take a couple of minutes to achieve. You can ping 192.168.1.1 and watch for ping replies to see when your router has rebooted into OpenWRT.  

That’s all there is to it. After OpenWRT boots for the first time, you'll be able to configure it to work on your local network. At most,I suggest setting a root password!

This process is pretty adaptable to other hardware, and the OpenWRT wiki is invaluable when it comes to specific steps to flash OpenWRT on any device you may have around. Dont feel like you have to get an N600 because I did, a lot of hardware is supported (I would recommend something with two radios and 8MB of flash for maximum hackery)!

This tutorial is just the first in a series where we will get cjdns configured on your OpenWRT router. The more meshing, the merrier!