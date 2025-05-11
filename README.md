# phillymesh.net
This is the repository for the `phillymesh.net` website! Anyone is welcome to submit updates to this site via [pull request]((https://github.com/phillymesh/phillymesh.net/pulls). Merged updates will go live automatically.

## Local Development

This site is built with the open-source [Hugo](https://gohugo.io/) static site generator, which converts Mardown posts and pages into HTML. 

If you want to run the site locally to test changes, you can do the following on a Debian Linux host. Hugo maintains a [gettiny started guide](https://gohugo.io/getting-started/quick-start/) if uou use a different operating system.

First, install `git` and grab Hugo extended:

```
sudo apt install git
wget https://github.com/gohugoio/hugo/releases/download/v0.113.0/hugo_extended_0.113.0_Linux-64bit.tar.gz
tar -xzf hugo_*.tar.gz && rm hugo_*.tar.gz
chmod +x hugo
```

Now, clone the `phillymesh.net` repo and pull down the theme via submodules:

```
git clone https://github.com/phillymesh/phillymesh.net.git
cd phillymesh.net
git submodule update --init --recursive
```

Finally, run `hugo` and build the site, hosting it on a live webserver:

```
hugo server
```

You know have a live server of the site running at <http://127.0.0.1:1313>

## Deploying on a Server

You likely don't need to know the following, but this was how the site was previously self-hosted.

```
cd /usr/local/bin/
wget https://github.com/gohugoio/hugo/releases/download/v0.113.0/hugo_extended_0.113.0_Linux-64bit.tar.gz
tar -xzf hugo_extended_0.113.0_Linux-64bit.tar.gz
rm hugo_*.tar.gz

cd /var/www
mkdir phillymesh.net
cd phillymesh.net
git clone https://github.com/phillymesh/phillymesh.net.git private
cd private
git submodule update --init --recursive
hugo
mv public ../
```
