
This Wiki page contains "copy & paste" recipes to compile libModSecurity (and connectors) in your favorite Linux distribution.

If your distribution is missing and you manage to compile it, don't forget to add it here in this list.


> **Attention:** Before start the compilation process make sure that the _paths are right_, and the _commands are sane_.

##### Table of Contents

1. [Centos 7 Minimal](#centos-7-minimal)
2. [Amazon Linux](#amazon-linux)


## Centos 7 Minimal

Sent by @elialum (See: #1039)

### libModSecurity

```sh
yum install gcc-c++ flex bison yajl yajl-devel curl-devel curl GeoIP-devel doxygen zlib-devel
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



## Amazon Linux

Provided by @csanders-git

### libModSecurity

```sh
yum install gcc-c++ flex bison curl-devel curl libxml2-devel doxygen zlib-devel git automake libtool pcre-devel
cd /opt/
# Steal Fedora's YAJL and YAJL-devel packages
wget ftp://195.220.108.108/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/y/yajl-2.1.0-4.fc23.x86_64.rpm
rpm -i yajl-2.1.0-4.fc23.x86_64.rpm
wget ftp://195.220.108.108/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/y/yajl-devel-2.1.0-4.fc23.x86_64.rpm
rpm -i yajl-devel-2.1.0-4.fc23.x86_64.rpm
# Install latest bison
yum install ftp://195.220.108.108/linux/fedora/linux/updates/23/x86_64/b/bison-3.0.4-3.fc23.x86_64.rpm
# Amazon's GeoIP-devel package does not come with geoip.pc (no idea why not)
wget ftp://rpmfind.net/linux/centos/5.11/extras/x86_64/RPMS/GeoIP-data-20090201-1.el5.centos.x86_64.rpm
wget ftp://rpmfind.net/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/g/GeoIP-1.6.6-1.fc23.x86_64.rpm
wget ftp://rpmfind.net/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/g/GeoIP-devel-1.6.6-1.fc23.x86_64.rpm
rpm -i GeoIP-1.6.6-1.fc23.x86_64.rpm  GeoIP-data-20090201-1.el5.centos.x86_64.rpm
rpm -i GeoIP-devel-1.6.6-1.fc23.x86_64.rpm
rm -rf *.rpm
git clone https://github.com/SpiderLabs/ModSecurity
cd ModSecurity
git checkout libmodsecurity
sh build.sh
git submodule init
git submodule update
./configure
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
./configure --add-module=/opt/ModSecurity-nginx 
make
make install
```