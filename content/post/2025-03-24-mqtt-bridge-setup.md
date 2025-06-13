---
title: MQTT Bridge Setup
author: Mike Dank (Famicoman)
type: post
date: 2025-03-24T00:00:02+00:00
url: /2025/03/24/mqtt-bridge-setup/
categories:
  - Tutorial
tags:
  - meshtastic
  - mosquito
  - mqtt

---

In August 2024 Meshtastic made changes to their official MQTT server due to potential safety issues of third parties tracking and storing user location data. While one of the main Meshtastic node mapping websites [meshmap.net](https://meshmap.net/) continues to rely on the official MQTT server, another popular site [meshtastic.liamcottle.net](https://meshtastic.liamcottle.net/) now runs their own separate MQTT server.

While MQTT can be leveraged to connect Meshtastic nodes to one another over-the-Internet to bridge separated networks or isolated nodes, many people instead use this feature specifically for contributing to node maps so others can see what nodes may be operating in their area. As already outlined, there are now two separate MQTT servers for node maps. However, the Meshtastic application only allows one MQTT server to be configured per node, which requires the user to make a choice of which one they will use and ultimately which site they will not contribute to.

Luckily, there is another approach that can be used to reliably send data to multiple MQTT servers: creating an MQTT bridge. This bridge can act as an intermediary, allowing Meshtastic nodes to send it data which is then forwarded to other servers.

Here we can see how to set up a server that feeds to both `mqtt.meshtastic.org` and `mqtt.meshtastic.liamcottle.net`.

## Installation & Base Config

This guide assumes a Debian Linux system with a non-root, `sudo` user.

First, we will install `mosquitto` as our MQTT server of choice:

```
$ sudo apt install mosquitto
```

Now we will add the initial configuration:

```
$ sudo cat /etc/mosquitto.conf
# Place your local configuration in /etc/mosquitto/conf.d/
#
# A full description of the configuration file is at
# /usr/share/doc/mosquitto/examples/mosquitto.conf.example
allow_anonymous false

listener 1883 0.0.0.0

pid_file /run/mosquitto/mosquitto.pid

persistence true
persistence_file mosquitto.db
persistence_location /var/lib/mosquitto/

# Uncomment for logging
# log_dest file /var/log/mosquitto/mosquitto.log
# log_type all

include_dir /etc/mosquitto/conf.d

password_file /etc/mosquitto/pwfile
```

Now we will generate a password for the `phillymesh` user to authenticate with:

```
$ sudo touch /etc/mosquitto/pwfile
$ sudo mosquitto_passwd -c /etc/mosquitto/pwfile phillymesh
```

## Adding Bridges

Additional configuration can be added to `/etc/mosquitto/conf.d/`, so let's create a file for each of our bridges:

```
$ sudo cat /etc/mosquitto/conf.d/mqtt.meshtastic.org.conf
connection mqtt_meshtastic.org
address mqtt.meshtastic.org:1883

# Username and password for the upstream server
remote_username meshdev
remote_password large4cats

# MQTT version to use
bridge_protocol_version mqttv311

# Forward all traffic from msh/*/2/map/ to the remote server
topic msh/+/2/map/# out 0
topic msh/# out 0

# Enable encryption
use_identity_as_username false
bridge_insecure true

# Bridge settings to manage the connection
cleansession true
notifications false
start_type automatic
try_private true
restart_timeout 10
```

```
$ sudo cat /etc/mosquitto/conf.d/mqtt.meshtastic.liamcottle.net.conf
connection mqtt_meshtastic_liamcottle_net
address mqtt.meshtastic.liamcottle.net:1883

# Username and password for the upstream server
remote_username uplink
remote_password uplink

# MQTT version to use
bridge_protocol_version mqttv311

# Forward all traffic from msh/*/2/map/ to the remote server
topic msh/+/2/map/# out 0
topic msh/# out 0

# Enable encryption
use_identity_as_username false
bridge_insecure true

# Bridge settings to manage the connection
cleansession true
notifications false
start_type automatic
try_private true
restart_timeout 10
```

## Finishing Touches

`mosquitto` leverages `systemd` to run as a service, so let's start it up:

```
$ sudo systemctl enable --now
```

Make sure that port `1883` is open in the firewall for client connections:

```
$ sudo iptables -L | grep 1883
ACCEPT     tcp  --  anywhere             anywhere             tcp dpt:1883
```

## Client Configuration

We will assume that the Meshtastic node is connected to the Internet already via WiFi/ethernet.

Client configuration can be set as follows for **MQTT**:

* MQTT enabled: *on*
* Address: IP or FQDN of your server
* Username: Username you defined
* Password: Password you defined
* Encryption enabled: *on*
* JSON output enabled: *off*
* TLS enabled: *off*
* Root topic: *msh/country/state* (Needs to be specific for `mqtt.meshtastic.org`, for example: *msh/US/PA*)
* Proxy to client enabled: *off*
* Map Reporting: *on*
* Precise location *off* and minimum of *1194 ft* to comply with `mqtt.meshtastic.org`
* Map reporting interval (seconds): *900*

Client configuration can be set as follows for **Channels > LongFast**:

* Uplink enabled: *on*
* Downlink enabled: *off*
* Position enabled: *on*
* Precise location *off* and minimum of *1194 ft* to comply with `mqtt.meshtastic.org`

## Sources

* https://www.reddit.com/r/meshtastic/comments/1f04xdu/is_it_possible_to_connect_to_two_mqtt_servers_at/
* https://cedalo.com/blog/mosquitto-bridge-configuration/#Bridging_multiple_brokers
* https://adrelien.com/blog/how-to-host-your-own-mqtt-for-your-meshtastic-nodes/
* https://meshtastic.org/docs/configuration/module/mqtt/#connect-to-the-default-public-server
* https://www.reddit.com/r/meshtastic/comments/1cneou7/deleted_by_user/