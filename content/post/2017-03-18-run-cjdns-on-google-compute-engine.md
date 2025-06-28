---
title: Run cjdns on Google Compute Engine
author: Mike Dank (Famicoman)
type: post
date: 2017-03-19T00:34:02+00:00
url: /2017/03/18/run-cjdns-on-google-compute-engine/
draft: true
categories:
  - Tutorial
tags:
  - cjdns
  - cloud
  - debian
  - f1-micro
  - google compute engine

---
Google recently announced the [Google Cloud Platform Free Tier][1], which includes an [f1-micro instance][2] on the Google Compute Engine. Compute Engine instances are essentially virtual private servers, with full customization available for disk size, number of processors and amount of memory. The f1-micro instance supplied free to each user boasts modest specifications: 1x shared virtual CPU (quantified as 0.2 of a CPU before bursting as available), 600MB of RAM, 5GB of snapshot storage, and 30GB of HDD persistent disk. As with all cloud providers, Compute Engine offers beefier machines priced accordingly. Luckily, Google is currently offering a (US only for the time being) free trial of the Google Cloud Platform for 12 months /$300. At around $4-$5 per f1-instance, a user could run several of these lower-tier machines for a year under their trial period.

Getting started with Google Compute Engine is relatively simple. This guide assumes you have a web browser, and a machine to make SSH connections from to access your Compute Engine instance. Commands for a Linux-based workstation will be shown, but should translate easily to a workstation running OSX or BSD.

## Compute Engine Instance Setup

Start by signing up for the free trial [here][1] (If you have already completed a trial, the same link should log you in to your account). This will ask for some personal information (if it is not already in your Google account) and credit card information to validate the account. Afterwards, we will be automatically logged into the Google Cloud Platform console. From here, we can create a new project by clicking the _Create project_ link in the console's banner near the top left of the screen.

{{< figure src="/images/uploads/2017/03/gcp-1.png" caption="Create a new project." link="/images/uploads/2017/03/gcp-1.png">}}

Give the project a name and click on the _Create_ button. Now we will be in the project's dashboard. Back in the console&#8217;s banner, press the _Products & services_ menu button on the left and select _Compute Engine_ from the menu.

{{< figure src="/images/uploads/2017/03/gcp-2.png" caption="Select Compute Engine from the menu." link="/images/uploads/2017/03/gcp-2.png">}}

A pop-up will now appear regarding VM instances. We will want to press the blue _Create_ button when prompted, this will launch the instance creation wizard. Give the instance a _Name_ (if desired) and pick a _Zone_ from the drop-down menu. There are many zones available, and their features are listed [here][3]. It is important to note that the free f1-micro instances are limited to US regions, so select one of those if interested in completing the always-free offer. If using  free trial credit or otherwise paying for an instance, feel free to select any zone desired. Under _Machine Type_, click the _Customize_ link to show our specification options.

{{< figure src="/images/uploads/2017/03/gcp-3.png" caption="Moving the slider for Cores all the way to the left will adjust the specs to an f1-micro instance." link="/images/uploads/2017/03/gcp-3.png">}}

Select the number of cores for the target virtual machine we are creating. Moving the slider all the way to the left will give us 1 shared vCPU and 600MB of RAM. Note of the monthly rate on the right side of the screen changes based on the modifications. As shown under Machine type, _Compute Engine_ offers a wide array of options for your instance, including GPU selection and even the option to run with 64 cores. We could pick a better instance for now and scale it down before the 12-month period is over to retain under the free tier, but for the sake of testing the f1-micro instance, the rest of this tutorial will proceed with settings as shown.

Lower in the page, we will leave the _Boot Disk_ selection alone as Debian Jessie on 10GB is more than enough for cjdns. Click the link for _Management, disk, networking, SSH keys_ to expand a few more options, and click on the _Networking_ tab.

{{< figure src="/images/uploads/2017/03/gcp-4.png" caption="The Networking tab for our instance." link="/images/uploads/2017/03/gcp-4.png">}}

Click on the drop-down menu under _External IP_ and select _New static IP address_. When prompted, give this IP address a name (anything will do) and press the _Reserve_ button to complete the action. This will make sure our external IP address does not change unexpectedly.

Now, we want to add an SSH key for remote access to our instance. On our Linux workstation, bring up a new console. To create the new SSH key-pair we will run `ssh-keygen`, specifying a file and our username. Make sure to create a passphrase when prompted!

```
$ ssh-keygen -t rsa -f ~/.ssh/google-compute-ssh -C famicoman
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/famicoman/.ssh/google-compute-ssh.
Your public key has been saved in /home/famicoman/.ssh/google-compute-ssh.pub.
The key fingerprint is:
d3:f1:63:ab:5a:f9:e8:54:87:92:e1:95:de:3c:58:27 famicoman
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|             .   |
|          o o E .|
|         o B * o |
|        S = O =  |
|         . = + . |
|          + .    |
|         o +     |
|        .o+ .    |
+-----------------+
```

Now we will modify the permissions of our private key to ensure only our user can access it:

```
$ chmod 400 ~/.ssh/google-compute-ssh
```

Finally, read the contents of our public key file, which we will be using to complete the Compute instance setup.

```
$ cat ~/.ssh/google-compute-ssh.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDbEKVCbgDus+hno+GKtsuYgrWSgarOH3/2R1q5IA1SWZXn9OJZQ1LAWn7QsM01tg7TTrrAo57wAlemC+eJgLLVsAnayvA/WZjlvjEdcX3TvQqzNnWGNf4VK7g/PvIOvyX4gj8uaHc/zWdz28KIgz2cUP/2bNWJox/p9M3vssxttpuTIL2knFIOKYphxaBWvfXu92a5kB60gso/0pcyZ7O+Kt2evfjtyByJRvypeM0YyMHM+xZ7b0gooWk9rSkpkGRJMBtHQOVVWqIQ2rjnEMPWNpEyqqC3KZmgolRP4a8TpXEDyP6N/2pc53zuVqCrgL7M8jYcIEmcLYASvTqWJlh5 famicoman
```

Back in our Compute instance setup, click on the _SSH Key_s tab, directly to the right of the _Networking_ tab we are currently on. In the _Enter entire key data_ textbox, paste the contents of the `google-compute-ssh.pub` file we just printed with `cat` and press the _Add item_ button.

{{< figure src="/images/uploads/2017/03/gcp-5.png" caption="Instance configuration after adding the SSH key." link="/images/uploads/2017/03/gcp-5.png">}}

Finally, press the _Create_ button to make our instance and boot it up for the first time.

After a few seconds, the virtual machine will appear on our screen and be ready to access.

{{< figure src="/images/uploads/2017/03/gcp-6.png" caption="Instance configuration after adding the SSH key." link="/images/uploads/2017/03/gcp-6.png">}}

## Cjdns Installation

Now back on our Linux workstation, we will SSH to the instance using the _External IP_ displayed for our instance:

```
$ ssh -i .ssh/google-compute-ssh famicoman@146.148.43.98
```

When prompted, accept the key for the host and enter the passphrase for the SSH key.

Now on our instance, let's change over to root, run an update and then upgrade all of the packages:

```
famicoman@instance-1:~$ sudo -i
root@instance-1:~$ apt-get update && apt-get upgrade -y
```

Now, we will install the packages we need to retrieve and install cjdns:

```
root@instance-1:~# apt-get install -y git build-essential
```

IPv6 is disabled on all Compute Engine instances by default, so we will want to override this by adding a few lines the `sysctl.conf` file to enable IPv6 and then reboot the instance:

```
root@instance-1:~$ { echo "net.ipv6.conf.all.disable_ipv6 = 0"; echo "net.ipv6.conf.default.disable_ipv6 = 0"; echo "net.ipv6.conf.tun0.disable_ipv6 = 0 = 0";} >> /etc/sysctl.conf && reboot
```

After a few moments, the machine should become unresponsive and the SSH session should terminate. Afterwards, SSH back into the machine from the workstation and change over to root again:

```
$ ssh -i .ssh/google-compute-ssh famicoman@146.148.43.98

famicoman@instance-1:~$ sudo -i
root@instance-1:~$ apt-get update && apt-get upgrade -y
```

Now we will change over to the `/opt` directory and clone the cjdns repo, checking out the latest version:

```
root@instance-1:~$ cd /opt
root@instance-1:/opt$ git clone https://github.com/cjdelisle/cjdns.git
root@instance-1:/opt$ cd cjdns && git checkout cjdns-v19.1
```

Now that the latest version is checked out, we can perform an optimized build:

```
root@instance-1:/opt/cjdns$ CFLAGS="-O2 -s -static -Wall -march=native" ./do
```

After a few minutes the build will be done. Next, we will link `cjdroute` into `/usr/local/bin` and generate a configuration file.

```
root@instance-1:/opt/cjdns$ cd /usr/local/bin/ && ln -s /opt/cjdns/cjdroute cjdroute
root@instance-1:/usr/local/bin$ cjdroute --genconf &gt; /usr/local/etc/cjdroute.conf
```

Finally, we can start cjdns:

```
root@instance-1:/usr/local/bin$ cjdroute &lt; /usr/local/etc/cjdroute.conf
1489881689 INFO cjdroute2.c:642 Cjdns amd64 linux +seccomp
1489881689 INFO cjdroute2.c:646 Checking for running instance...
1489881689 DEBUG UDPAddrIface.c:293 Bound to address [0.0.0.0:34199]
1489881689 DEBUG AdminClient.c:333 Connecting to [127.0.0.1:11234]
1489881690 DEBUG Pipe.c:134 Buffering a message
1489881690 DEBUG cjdroute2.c:699 Sent [144] bytes to core
1489881690 INFO RandomSeed.c:42 Attempting to seed random number generator
1489881690 INFO RandomSeed.c:50 Trying random seed [/dev/urandom] Success
1489881690 INFO RandomSeed.c:56 Trying random seed [sysctl(RANDOM_UUID) (Linux)] Failed
1489881690 INFO RandomSeed.c:50 Trying random seed [/proc/sys/kernel/random/uuid (Linux)] Success
1489881690 INFO RandomSeed.c:64 Seeding random number generator succeeded with [2] sources
1489881690 INFO LibuvEntropyProvider.c:59 Taking clock samples every [1000]ms for random generator
1489881690 DEBUG Pipe.c:231 Pipe [/tmp/cjdns_pipe_client-core-ycdqw9fs9m75mv3vqv16x7pvg0mcw5] established connection
1489881690 DEBUG Pipe.c:253 Sending buffered message
1489881690 DEBUG Core.c:354 Getting pre-configuration from client
1489881690 DEBUG Pipe.c:231 Pipe [/tmp/cjdns_pipe_client-core-ycdqw9fs9m75mv3vqv16x7pvg0mcw5] established connection
1489881690 DEBUG Core.c:357 Finished getting pre-configuration from client
1489881690 DEBUG UDPAddrIface.c:254 Binding to address [127.0.0.1:11234]
1489881690 DEBUG UDPAddrIface.c:293 Bound to address [127.0.0.1:11234]
1489881690 DEBUG UDPAddrIface.c:293 Bound to address [0.0.0.0:37092]
1489881690 DEBUG AdminClient.c:333 Connecting to [127.0.0.1:11234]
1489881690 INFO Configurator.c:135 Checking authorized password 0.
1489881690 INFO Configurator.c:159 Adding authorized password #[0] for user [default-login].
1489881690 INFO Configurator.c:411 Setting up all ETHInterfaces...
1489881690 INFO Configurator.c:427 Creating new ETHInterface [eth0]
1489881690 INFO Configurator.c:388 Setting beacon mode on ETHInterface to [2].
1489881690 DEBUG Configurator.c:531 Security_chroot(/var/run/)
1489881690 DEBUG Configurator.c:576 Security_noforks()
1489881690 DEBUG Configurator.c:581 Security_setUser(uid:65534, keepNetAdmin:1)
1489881690 DEBUG Configurator.c:596 Security_seccomp()
1489881690 DEBUG Configurator.c:601 Security_setupComplete()
1489881690 DEBUG Configurator.c:685 Cjdns started in the background
```

Now that cjdns is running, let's verify this by checking out the interface with `ifconfig`:

```
root@instance-1:/usr/local/bin# ifconfig tun0
tun0      Link encap:UNSPEC  HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00
          inet6 addr: fcab:62fc:cd8b:36f0:7837:4361:9aa3:946d/8 Scope:Global
          UP POINTOPOINT RUNNING NOARP MULTICAST  MTU:1304  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:500
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

## Conclusion

We are now free to add peers to our `cjdroute.conf` file or generate our own peering credentials for other installations! Be sure to keep in mind Google Compute Engine's rates for egress bandwidth as noted [here][4]. Nobody wants to make up with a $500 bill for bandwidth. And, as always, consider locking down your node with proper firewall rules, etc. now that it is live and Internet-facing.

Compute instances should perform relatively well, even the f1-micro instances. Below are sample cjdns bench results for the f1-micro:

```
root@instance-1:/usr/local/bin# cjdroute --bench | grep "per second"
1489881851 INFO Benchmark.c:62 Benchmark salsa20/poly1305 in 653ms. 1837672 kilobits per second
1489881851 INFO Benchmark.c:62 Benchmark Switching in 342ms. 598830 packets per second
root@instance-1:/usr/local/bin# cjdroute --bench | grep "per second"
1489881854 INFO Benchmark.c:62 Benchmark salsa20/poly1305 in 635ms. 1889763 kilobits per second
1489881854 INFO Benchmark.c:62 Benchmark Switching in 335ms. 611343 packets per second
root@instance-1:/usr/local/bin# cjdroute --bench | grep "per second"
1489881858 INFO Benchmark.c:62 Benchmark salsa20/poly1305 in 664ms. 1807228 kilobits per second
1489881858 INFO Benchmark.c:62 Benchmark Switching in 355ms. 576901 packets per second
```

 [1]: https://cloud.google.com/free/
 [2]: https://cloud.google.com/compute/docs/machine-types
 [3]: https://cloud.google.com/compute/docs/regions-zones/regions-zones
 [4]: https://cloud.google.com/compute/pricing#network