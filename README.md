# phillymesh.net
The Philly Mesh Website

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
