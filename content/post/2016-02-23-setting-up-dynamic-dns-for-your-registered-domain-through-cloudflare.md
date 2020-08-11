---
title: Setting Up Dynamic DNS for Your Registered Domain through CloudFlare
author: Mike Dank (Famicoman)
type: post
date: 2016-02-23T22:33:09+00:00
url: /2016/02/23/setting-up-dynamic-dns-for-your-registered-domain-through-cloudflare/
draft: true
categories:
  - Tutorial
tags:
  - cloudflare
  - cron
  - domain
  - duckdns
  - dynamic dns
  - freedns
  - linux

---
*Note: As of cjdns version 18, cjdns peering credentials will not be valid if they use domain names as opposed to IP addresses. If you are reading this in the year 2017 or later, the below guide is essentially obsolete from a peering perspective but may still be useful for automatically updating DNS records for other purposes.*  

If you host a node at a residential location, you probably do not have the comfort of a static IP address, one which does not change. Residential Internet accounts usually have the unfortunate side effect of occasional public-facing IP address changes, meaning you have a dynamic IP address. If you give out your peering information to others with your IP address and it changes, these credentials will fail until you are able to supply all of your peers with an updated IP address. Even after you discover the issue, it could take a while for all of your peers to adopt the new information, causing plenty of broken connections.  

To solve this problem, we can use dynamic DNS, and get you a domain name to use in place of your IP address by acting as a pointer to it. There are many providers that do this including [Duck DNS](https://www.duckdns.org/) and [FreeDNS](https://freedns.afraid.org/"). Almost all of them allow you to create subdomains (like *yoursupercoolsub.duckdns.org*) which behind the scenes point to your IP address. In DNS lingo, this is called an A record (or AAAA record if you have an IPv6 address). Most of these services also allow you to download a client to automatically update your IP address for the record if it changes, so you can just distribute the subdomain’s name to your peers and not worry about unexpected changes.  

This works well, but I (and possibly some of you) have a paid domain set up through CloudFlare’s DNS. Instead of *famicomans-node.duckdns.org*, I would prefer to use my own domain and configure something like *node.famicoman.com* to act as a pointer to my IP address. Now, I could make a record with a dynamic DNS provider (like *famicomans-node.duckdns.org*) and have *node.famicoman.com* point to it instead of the IP address directly (this is called a C record) but that would require me to sign up for another service and configure the two to work together.  

Instead of this, I decided to use CloudFlare directly, working with their API, some scripting, and a cron job.  

The following assumes that you have registered at CloudFlare and have already added your domain to its care. We also assume that your cjdns installation is on a Linux machine, or you have access to one on your home network.  

Before doing anything else, you need to retrieve your CloudFlare API key. Log into the CloudFlare console and navigate to *My Settings*. Scroll down until you find the API Key item and press the button labeled *View API Key*. After your API key displays, record it for use later.  

{{< figure src="/images/uploads/2017/03/image05-768x103.png"  link="/images/uploads/2017/03/image05.png">}}

Now, navigate to the *DNS* tab for your domain name. Create a new A record for your public IP by specifying a name (I chose “node”) and a dummy IP address (I used “8.8.8.8”). It doesn’t matter what IP address you supply as it will be updated later. Afterwards, press the green *Add Record* button.  

{{< figure src="/images/uploads/2017/03/image04-768x281.png"  link="/images/uploads/2017/03/image04.png">}}
   
The record should now display below with a gray cloud icon next to it. This shows that CloudFlare’s CDN services are not active for the record (which is what we want) and that this sub domain name will resolve the IP address directly.  

{{< figure src="/images/uploads/2017/03/image02-768x54.png"  link="/images/uploads/2017/03/image02.png">}}

Now on your cjdns node, we can start to configure automatic updates.  

First, we need to set up some directories. Log into a non-root account and execute the following to create and change into our new directory. I like to put each of my scripts in its own folder under a ‘scripts’ folder in my home directory, but feel free to use a different location.  

```
mkdir -p ~/scripts/cloudflare-update-record
cd ~/scripts/cloudflare-update-record
```

Now, we will download a gist with a CloudFlare update script, saving it as ‘cloudflare-update-record.sh’. As always, it is unwise to blindly execute something from a random script on the Internet, so review the code to check for any funny business. You can see updates to and comments on this script [here](https://gist.github.com/benkulbertis/fff10759c2391b6618dd/).  

```
wget https://gist.githubusercontent.com/benkulbertis/fff10759c2391b6618dd/raw/0e365a91a15e15494b312cb5492e40dec2072414/cloudflare-update-record.sh
```

Now we will edit the script to supply credentials for connecting to and updating our CloudFlare record.  

```
nano cloudflare-update-record.sh
```

Near the top of the file, there are four fields you need to set with some values. Enter your email as the *auth_email*, your API key from earlier as the *auth_key*, your root domain as the *zone_name*, and your subdomains name as the *record_name*. Below is an example of what these fields might look like filled out.  

```
auth_email="famicoman@gmail.com"
auth_key="a456a7b68cb9ac65b34c2b43b3c6bc4c2b4" # found in cloudflare account settings
zone_name="famicoman.com"
record_name="node.famicoman.com
```

Now we want to change permissions so only you can read, write, and execute the script (we wouldn’t want any other users peeking at your API key), and finally execute the script to test it out.  
  
```
chmod 700 cloudflare-update-record.sh
./cloudflare-update-record.sh
```

If all goes to plan, you should receive output similar to the following in your console:  

```
>>> IP changed to: 127.112.6.34
```

If you don’t get a message that your IP is changed, go back and check the credentials you entered into *cloudflare-update-record.sh* and make sure they are correct.  

Additionally, we can check *cloudflare.log* to see a time-stamped account of our execution.  

```
cat cloudflare.log
[Tue  9 Feb 22:32:30 UTC 2016] - Check Initiated
[Tue  9 Feb 22:32:33 UTC 2016] - IP changed to: 127.112.6.34
```

Now, we want to have this script run automatically to reduce downtime. I’ve opted to set this script up to run every 10 minutes and schedule it with cron.  

Bring up your crontab with the following command:  

```
crontab -e
```

Scroll to the bottom of the file in your editor and paste the below command on a new line. Every 10 minutes, every hour, every day of the month, every month, and every day of the week this job will run by changing to your *cloudflare-update-record* directory and then executing *cloudflare-update-record.sh*.  

```
*/10 * * * * cd ~/scripts/cloudflare-update-record && /bin/bash ~/scripts/cloudflare-update-record/cloudflare-update-record.sh
```

After saving (C-x), the new job will become active. We can watch the job go off by tailing the *cloudflare.log* file.  

```
tail -f cloudflare.log
```
   
It will take some time depending on when you first save the crontab, but you should see records written to the log in realtime, every 10 minutes starting on the hour.  
  
```
[Tue  9 Feb 22:32:30 UTC 2016] - Check Initiated
[Tue  9 Feb 22:32:33 UTC 2016] - IP changed to: 127.112.6.34
[Tue  9 Feb 22:40:02 UTC 2016] - Check Initiated
[Tue  9 Feb 22:50:02 UTC 2016] - Check Initiated
[Tue  9 Feb 23:00:02 UTC 2016] - Check Initiated
```
   
That’s all there is to it, you can now distribute your connection details using a subdomain on a registered domain name instead of your IP address. Keep in mind that this can be scaled to multiple nodes by giving them multiple subdomain names (node1, node2, etc.) for easy remember-ability.  