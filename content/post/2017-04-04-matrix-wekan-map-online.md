---
title: 'Matrix, Wekan, & Map Online!'
author: Mike Dank (Famicoman)
type: post
date: 2017-04-04T23:51:39+00:00
url: /2017/04/04/matrix-wekan-map-online/
draft: true
categories:
  - Philly Mesh
tags:
  - hyperboria
  - irc
  - kanban
  - map
  - matrix
  - nodeshot
  - nycmesh
  - riot
  - tomesh
  - vultr
  - wekan

---
For the past week I've been heavily investing time into the Philly Mesh infrastructure by setting up new resources for the group. I've spun up a new VPS through [Vultr][1], located in New Jersey, to host some of the more intensive applications. Information for peering with this box will be available shortly, as it is already [up and running on the Hyperboria network][2]!

The new VPS hosts three main services for the time being:

First is a [Matrix server (matrix.phillymesh.net)][3] for group communication. All existing addresses and bridges (like IRC) will continue to work and this new server just supplies another federated endpoint to get on the network. Please don&#8217;t hesitate to say hi (we also host [our own webchat for Matrix (chat.phillymesh.net)][4] though [Riot][5] is available for many platforms)!

Second, we are hosting [a Wekan installation (wekan.phillymesh.net)][6]. This kanban-style application will help organize and keep track of current projects and map out needs for future ones. The Wekan has open registrations at this time, though it may be a bit empty at first!

Third, in collaboration with [Toronto Mesh][7] I am working on [a new node map (map.phillymesh.net)][8] based off of [NYC Mesh's map][9] source. This is a work in progress and will ultimately have a GitHub repository available for anyone to use for node submission. I am also looking at other meshnet mapping solutions such as [NodeShot][10], but they are proving to be unusable for the time being.

Rough notes for the installations are currently available through [our documentation repo on GitHub][11] and will be cleaned up and expanded upon in the future!

 [1]: https://www.vultr.com/
 [2]: https://www.fc00.org/#fc05:3ab5:1182:ae26:c81c:0a85:b6a4:b241
 [3]: https://matrix.phillymesh.net
 [4]: https://chat.phillymesh.net/#/room/#phillymesh:phillymesh.net
 [5]: https://riot.im/
 [6]: https://wekan.phillymesh.net/sign-in
 [7]: https://tomesh.net/
 [8]: http://map.phillymesh.net/
 [9]: https://nycmesh.net/map/
 [10]: https://github.com/ninuxorg/nodeshot
 [11]: https://github.com/phillymesh/documents