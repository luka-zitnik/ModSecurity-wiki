
This Wiki page contains "copy & paste" recipes to compile libModSecurity (and connectors) in your favorite Linux distribution.

If your distribution is missing and you manage to compile it, don't forget to add it here in this list.


> **Attention:** Before start the compilation process make sure that the _paths are right_, and the _commands are sane_.

##### Table of Contents

1. [Centos 7 Minimal](#centos-7-minimal)


## Centos 7 Minimal

Sent by @elialum (See: #1039)

### libModSecurity

```sh
yum install gcc-c++ flex bison curl-devel curl yajl yajl-devel GeoIP-devel doxygen zlib-devel
cd /opt/
git clone https://github.com/SpiderLabs/ModSecurity
cd ModSecurity
git checkout libmodsecurity
sh build.sh
git submodule init
git submodule update
./configure
yum install ftp://195.220.108.108/linux/fedora/linux/updates/23/x86_64/b/bison-3.0.4-3.fc23.x86_64.rpm
make
make install
```

### nginx connector

```sh
cd /opt/
git clone https://github.com/SpiderLabs/ModSecurity-nginx
cd /opt/ModSecurity-nginx
git checkout experimental
cd /opt
wget http://nginx.org/download/nginx-1.9.2.tar.gz
tar -xvzf nginx-1.9.2.tar.gz
cd /opt/nginx-1.9.2
/bin/cp -f /usr/sbin/nginx /usr/sbin/nginx_original_bkp
./configure --add-module=/opt/ModSecurity-nginx 
make
make install
```