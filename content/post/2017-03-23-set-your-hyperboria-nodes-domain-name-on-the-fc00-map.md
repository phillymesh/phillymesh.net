---
title: Set Your Hyperboria Node’s Domain Name on the fc00 Map
author: Mike Dank (Famicoman)
type: post
date: 2017-03-23T23:17:16+00:00
url: /2017/03/23/set-your-hyperboria-nodes-domain-name-on-the-fc00-map/
draft: true
categories:
  - Tutorial
tags:
  - fc00
  - git
  - github
  - hyperboria
  - ipv6
  - pull request
  - tld

---
[fc00][1], a project aimed to make the Hyperboria network more accessible, has been hosting a network map of Hyperboria peers for a few years. The map, updated throughout the day, is available to view [here][2]. Unlike geographic maps, the fc00 map shows the network topology. While I won&#8217;t be able to see if my node in Seattle neighbors any other nodes I&#8217;m not connected to, I can see the edges between nodes and view the centrality of the network.

{{< figure src="/images/uploads/2017/03/fc00map05-768x702.png" caption="The node map at the time of writing." link="/images/uploads/2017/03/fc00map05.png">}}

The fc00 map also has a handy search feature where you are able to look up nodes based on their IP address or domain name to view cjdns version, connected peers, and centrality. However, domain names are not discovered automatically and need to be added manually via a GitHub repository.

Adding your node's domain name to the GitHub repo is a relatively simple process, and serves as a good introduction to creating pull requests for any git project. This guide assumes you have a web browser, a GitHub account, a DNS AAAA record pointed to the IPv6 address of your Hyperboria node (subdomains work too!), and a non-root, sudo user on a Linux machine. Commands for a Linux-based workstation will be shown, but should translate easily to a workstation running OSX or BSD.

## Forking the Repository

The node list lives in a GitHub repository, https://github.com/zielmicha/nodedb. Obviously, this is not our own personal repository, so we will first need to fork the repository to our own GitHub account. This will duplicate the repository&#8217;s current state so we can perform edits. Navigate to the repository's page and press the _Fork_ button on the right side of the page, near the top.

{{< figure src="/images/uploads/2017/03/fc00map01-768x163.png" caption="Press the fork button." link="/images/uploads/2017/03/fc00map01.png">}}

If prompted for a location to fork the repository to, choose your profile. You will now have a complete copy of the repo within your account. Now, on the right side of the page, press the button labeled _Clone or download_. In the small popup that appears, copy the URL from the field with `ctrl-c` to get it on our clipboard.

{{< figure src="/images/uploads/2017/03/fc00map02-768x344.png" caption=" Press the Clone or download button and copy the URL." link="/images/uploads/2017/03/fc00map02.png">}}

## Cloning the Repo

On the Linux machine, let's do a little housekeeping and install `git` so we can get to work:

```
$ sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install git
```

Now we will clone the repository to our local machine, pasting the link we copied earlier:

```
$ git clone https://github.com/Famicoman/nodedb.git
]Cloning into 'nodedb'...
remote: Counting objects: 578, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 578 (delta 4), reused 0 (delta 0), pack-reused 568
Receiving objects: 100% (578/578), 163.20 KiB | 91.00 KiB/s, done.
Resolving deltas: 100% (256/256), done.
Checking connectivity... done.
```

Next, we can change into the directory and start making updates:

```
$ cd nodedb
```

We will only be running a script in the repo to automatically add the node to the proper location in the file (sorted by address). We will be running `addnode.sh` and pass in our node&#8217;s IPv6 Hyperboria address and the domain with an AAAA record pointing to it. Note: this domain should be a fully qualified domain name (FQDN). Here is an example with domain _h.peer0.famicoman.phillymesh.net_ which points to _fc9f:990d:2b0f:75ad:8783:5d59:7c84:520b_:

```
$ ./addnode.sh fc9f:990d:2b0f:75ad:8783:5d59:7c84:520b h.peer0.famicoman.phillymesh.net
```

If we happen to have two or more domain names pointing to the node, we can add them all via one command (though currently on the first in the list is searchable on the fc00 map):

```
$ ./addnode.sh fc9f:990d:2b0f:75ad:8783:5d59:7c84:520b "h.peer0.famicoman.phillymesh.net h.peer0.famicoman.com"
```

The changes are now made, so we can commit them to our local, working copy of the repo with a message describing our changes:

```
git commit -am "Added famicoman's node0"
[master 125b493] Added famicoman's node0
 1 file changed, 1 insertion(+), 1 deletion(-)
 ```

Finally, we will push the changes back to our repo on GitHub:

```
$ git push origin master
Username for 'https://github.com': Famicoman
Password for 'https://Famicoman@github.com':
Counting objects: 3, done.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 292 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/Famicoman/nodedb.git
   3f94d16..125b493  master -&gt; master
```

## Creating the Pull Request

Back on Github, we can view the changes to our repository by clicking the link labeled _Compare_ on the right side of our fork's page.

{{< figure src="/images/uploads/2017/03/fc00map03-768x256.png" caption="Click the Compare link." link="/images/uploads/2017/03/fc00map03.png">}}

This will show the changes between our fork's repository and the official repository at **zielmicha/nodedb**. From here, all we have to do is press the button labeled _Create pull request_. This will automatically create a request for a change at the official **zielmicha/nodedb** repository which the author can then approve and merge into the main branch.

{{< figure src="/images/uploads/2017/03/fc00map04-768x395.png" caption="Press the button for Create Pull Request." link="/images/uploads/2017/03/fc00map04.png">}}

## Making Updates

Later on, we may want to go back and add more nodes to the list or otherwise edit nodes we have already added. We already know the commands to run to get our changes into our fork, but by this time it may be out of date! Luckily we can force an update to our fork from the main **zielmicha/nodedb** branch so we can perform our edits on the most up-to-date version of the repository.

Back on the Linux machine, simply run the following set of commands:

```
$ git remote add upstream https://github.com/zielmicha/nodedb
$ git fetch upstream
$ git checkout master
$ git reset --hard upstream/master
$ git push origin master --force
```

Now we are free to add nodes, commit, push changes to our fork,and create a new pull request!

## Conclusion

Creating pull requests through GitHub is a simple task, and adding a node to the fc00 map is a perfect introduction to the process. After your pull request gets successfully merged, be sure to [check out your node on the map][3]!

{{< figure src="/images/uploads/2017/03/fc00map06.png" caption="My (small) node." link="/images/uploads/2017/03/fc00map06.png">}}

 [1]: https://www.fc00.org/about
 [2]: https://www.fc00.org
 [3]: https://www.fc00.org/