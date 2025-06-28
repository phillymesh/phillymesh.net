---
title: 'CJDNS on OpenWRT – Part 2: Configuring Extroot for More Storage'
author: Mike Dank (Famicoman)
type: post
date: 2016-04-11T21:46:56+00:00
url: /2016/04/11/cjdns-on-openwrt-part-2-configuring-extroot-for-more-storage/
categories:
  - Tutorial
tags:
  - extroot
  - firmware
  - flash
  - n600
  - openwrt
  - opkg
  - partition
  - rootfs
  - Western digital
#cspell:ignore rootfs fdisk opkg
---
If you have any low-memory OpenWRT device (4MB of flash) you will probably fill up any free space quickly after the initial OpenWRT install and need more room to grow. Luckily, you can transfer your root file system to a flash drive and boot off of it as long as your access point has a USB port.

If you are following along with our Western Digital N600, you probably don’t need to do this. The N600 comes equipped with 12MB of built-in flash, more than enough to accommodate the software packages we will install in the future. If you have less than this or want to have a nice learning exercise, read on!

You are going to need a Linux machine and a flash drive. The flash drive size shouldn’t matter too much. A lot of people run OpenWRT off of 8MB of internal flash, so any small drive should have plenty of room.

On your Linux machine, plug in the flash drive (mine is a ~10 year old 64MB), and run *dmesg* to get the kernel message buffer.

```
dmesg
```

You should get a lot of output, but importantly at the end, we should see our flash drive being recognized:

```
[26913.782811] usb 1-1.4: new high-speed USB device number 4 using dwc_otg
[26913.883754] usb 1-1.4: New USB device found, idVendor=0457, idProduct=0151[26913.883779] usb 1-1.4: New USB device strings: Mfr=0, Product=2, SerialNumber=3
[26913.883796] usb 1-1.4: Product: USB Mass Storage Device
[26913.883812] usb 1-1.4: SerialNumber: 00000000004FDE
[26913.884913] usb-storage 1-1.4:1.0: USB Mass Storage device detected
[26913.887282] usb-storage 1-1.4:1.0: Quirks match for vid 0457 pid 0151: 80
[26913.887450] scsi host0: usb-storage 1-1.4:1.0
[26914.884185] scsi 0:0:0:0: Direct-Access     Staples                   0.00 PQ: 0 ANSI: 2
[26914.886688] sd 0:0:0:0: [sda] 124000 512-byte logical blocks: (63.4 MB/60.5 MiB)
[26914.887210] sd 0:0:0:0: [sda] Write Protect is off
[26914.887235] sd 0:0:0:0: [sda] Mode Sense: 00 00 00 00
[26914.887748] sd 0:0:0:0: [sda] Asking for cache data failed
[26914.887771] sd 0:0:0:0: [sda] Assuming drive cache: write through
[26914.916959]  sda: sda1
[26914.920057] sd 0:0:0:0: [sda] Attached SCSI removable disk
[26914.922645] sd 0:0:0:0: Attached scsi generic sg0 type 0
```

We see that our physical device is *sda*, with one partition *sda1*. Your drive/partition may be labeled differently depending on how many drives you have installed or plugged into your machine, and how many partitions your flash drive has. We can verify we are looking at our flash drive by listing via *fdisk*.

```
fdisk -l /dev/sda
```

You will get a lot of informative output about the device:

```
Disk /dev/sda: 63 MB, 63488000 bytes
16 heads, 32 sectors/track, 242 cylinders, total 124000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x91f72d24

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *          32      123999       61984    b  W95 FAT32
```

Now we will go ahead and format the drive as ext4. First however, we need to create a partition by running the *fdisk* command on the drive (without the -l option).

```
fdisk /dev/sda
```

This is an interactive utility, so when prompted, enter <i>d</i> to delete the current partition on the drive. Then enter *n<* for a new partition (taking the defaults by pressing the return key). Finally, enter *w* to apply the changes to the disk and exit.

Now, we can make a file system on the partition we just created, formatting it as ext4:

```
mkfs.ext4 /dev/sda1
```

Afterwards we can list with *fdisk* again to see our changes:

```
fdisk -l /dev/sda

Disk /dev/sda: 63 MB, 63488000 bytes
3 heads, 32 sectors/track, 1291 cylinders, total 124000 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x91f72d24

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1            2048      123999       60976   83  Linux
```

You can now remove your USB drive from your Linux machine and plug it into your OpenWRT device.

Next, we ssh into our OpenWRT device and login as root. We need to install a few utilities with *opkg* before we can switch over the root filesystem.

```
opkg update && opkg install block-mount kmod-fs-ext4 kmod-usb-storage fdisk nano
```

Now we will run *fdisk* to see that our drive is recognized:

```
root@OpenWrt:~# fdisk -l

Disk /dev/mtdblock0: 256 KiB, 262144 bytes, 512 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock1: 64 KiB, 65536 bytes, 128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock2: 64 KiB, 65536 bytes, 128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock3: 64 KiB, 65536 bytes, 128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock4: 15.5 MiB, 16252928 bytes, 31744 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock5: 1.3 MiB, 1310720 bytes, 2560 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock6: 14.3 MiB, 14942208 bytes, 29184 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock7: 12.1 MiB, 12648448 bytes, 24704 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/mtdblock8: 64 KiB, 65536 bytes, 128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk /dev/sda: 60.6 MiB, 63488000 bytes, 124000 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x91f72d24

Device     Boot Start    End Sectors  Size Id Type
/dev/sda1        2048 123999  121952 59.6M 83 Linux
```

My drive registers as /dev/sda1, and this is used through the commands below. Make sure you take note of yours and make the necessary changes when running additional commands.

Next, we will copy our filesystem over and set the device to boot from the flash drive. If you are squeamish about making this change via a terminal, scroll down and view the sources referenced at the end of this tutorial. There is a way to perform this configuration using OpenWRT’s default graphical interface: LuCI. If you prefer to issue commands over ssh, read on.

Now, we will actually mount the drive, and copy the root filesystem to it:

```
mkdir /mnt/sda1
mount /dev/sda1 /mnt/sda1
mkdir -p /tmp/cproot
mount --bind / /tmp/cproot
tar -C /tmp/cproot -cvf - . | tar -C /mnt/sda1 -xf -
umount /tmp/cproot
```

After we have moved the filesystem over, we can modify the *fstab* with our editor of choice.

```
nano /etc/config/fstab
```

Paste the following at the top the file and save it. This will use the flash drive as the primary filesystem and preserve this configuration even after reboot.

```
config mount
	option device '/dev/sda1'
	option target '/'
	option fstype 'ext4'
	option enabled '1'
```

Finally, we reboot the device by issuing the *reboot* command:

```
reboot
```

After the system comes back up, ssh into it once more and run the *df* command.

```
df -h
```

In the output, pay attention to the *Size* column to make sure it matches up closely to your flash drive’s capacity to verify that you are actually running off of the flash drive.

```
Filesystem                Size      Used Available Use% Mounted on
rootfs                   53.7M      9.7M     39.8M  20% /
/dev/root                 2.3M      2.3M         0 100% /rom
tmpfs                    61.6M    628.0K     61.0M   1% /tmp
/dev/sda1                53.7M      9.7M     39.8M  20% /
tmpfs                   512.0K         0    512.0K   0% /dev
```

That's all there is to it! Now, you are booting directly off of the flash drive and have more room to install packages. Additionally, you may want to save an image of your drive for future use. You never know when you will be trying something out and need to restore from a backup!

**Sources**
* https://samhobbs.co.uk/2013/11/more-space-for-packages-with-extroot-on-your-openwrt-router
* http://blog.lincomatic.com/?p=1287