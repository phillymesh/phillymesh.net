---
title: Torrent Tracker Now Online
author: Mike Dank (Famicoman)
type: post
date: 2018-01-08T20:25:46+00:00
url: /2018/01/08/torrent-tracker-now-online/
draft: true
categories:
  - Philly Mesh
tags:
  - bittorrent
  - cjdns
  - hyperboria
  - opentracker
  - tcp
  - torrent
  - tracker
  - udp

---
I've gone ahead and set up a BitTorrent tracker that only faces the Hyperboria network. This tracker runs the opensource [OpenTracker][1] software written by Dirk Engling, compiled with IPv6 support. It is available via either udp or tcp (udp preferred, as it is less resource intensive):

```
udp://h.tracker.phillymesh.net:6969 
http://h.tracker.phillymesh.net:6969
```

You can add this tracker to any torrent you create to distribute over the Hyperboria network. No peers outside of Hyperboria will be able to contact this tracker or send/receive any torrent data.

 [1]: http://erdgeist.org/arts/software/opentracker/