
This Wiki page contains "copy & paste" recipes to compile libModSecurity (and connectors) in your favorite Linux distribution.

If your distribution is missing and you manage to compile it, don't forget to add it here in this list.


> **Attention:** Before start the compilation process make sure that the _paths are right_, and the _commands are sane_.

##### Table of Contents

1. [CentOS 7 Minimal](#centos-7-minimal)
2. [Amazon Linux](#amazon-linux)
3. [CentOS 6.x](#centos-6x)
4. [CentOS 6.5](#centos-65-minimal)
5. [Ubuntu 15.04](#ubuntu-1504)

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

## CentOS 6.x

Provided by @moodygit

### libModSecurity

```sh
$ cd /opt/
$ git clone https://github.com/SpiderLabs/ModSecurity
$ cd ModSecurity
$ git checkout libmodsecurity
$ sh build.sh
$ git submodule init
$ git submodule update
$ ./configure
$ make
$ make install
```

### nginx-connector (openresty) 

```sh
$ cd /opt/
$ git clone https://github.com/SpiderLabs/ModSecurity-nginx
$ cd /opt/Modsecurity-nginx
$ git checkout experimental
$ cd /opt/
$ wget https://openresty.org/download/ngx_openresty-1.9.7.1.tar.gz
$ tar -xvzf ngx_openresty-1.9.7.1.tar.gz
$ ./configure --add-module=/opt/ModSecurity-nginx
```

## CentOS 6.5 Minimal

Provided by @csanders-git

### libModSecurity

```sh
yum install -y wget perl cmake
# Add a newer version of GCC that can make c++-11
wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo
yum install -y devtoolset-2-gcc-c++ devtoolset-2-binutils
PATH=/opt/rh/devtoolset-2/root/usr/bin:$PATH
cd /opt/
#Install bison
wget http://ftp.gnu.org/gnu/bison/bison-3.0.4.tar.gz
tar -xvzf bison-3.0.4.tar.gz
cd bison-3.0.4
./configure
make
make install
cd /opt/
# Install autoconf
wget http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.gz
tar -xvzf autoconf-2.69.tar.gz
cd autoconf-2.69
./configure
make
make install
cd /opt
# Install libtool
wget http://ftp.gnu.org/gnu/libtool/libtool-2.4.5.tar.gz
tar -xvzf libtool-2.4.5.tar.gz
cd libtool-2.4.5
./configure
make
make install
cd /opt
# Install automake
wget http://ftp.gnu.org/gnu/automake/automake-1.15.tar.gz
tar -xvzf automake-1.15.tar.gz
cd automake-1.15
./configure
make
make install
cd /opt	
# Insteall PCRE-devel
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.38.tar.gz
tar -xvzf pcre-8.38.tar.gz
cd pcre-8.38
./configure
make
make install
cd /opt/
# Install YAJL2
wget http://github.com/lloyd/yajl/tarball/2.1.0 -O yajl-2.1.0.tar.gz
tar -xvzf yajl-2.1.0.tar.gz
cd lloyd-yajl-66cb08c
./configure
make
make install
cd /opt
# Install Curl
wget http://curl.haxx.se/download/curl-7.46.0.tar.gz
tar -xvzf curl-7.46.0.tar.gz 
cd curl-7.46.0
./configure --prefix=/opt/curl
make
make install
# Little hack because make doesn't respect --with-curl currently
cp -R /opt/curl/include/curl/ /usr/include/
cd /opt/
# Install GeoIP
wget ftp://rpmfind.net/linux/centos/5.11/extras/x86_64/RPMS/GeoIP-data-20090201-1.el5.centos.x86_64.rpm
wget ftp://rpmfind.net/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/g/GeoIP-1.6.6-1.fc23.x86_64.rpm
wget ftp://rpmfind.net/linux/fedora/linux/releases/23/Everything/x86_64/os/Packages/g/GeoIP-devel-1.6.6-1.fc23.x86_64.rpm
rpm -i GeoIP-1.6.6-1.fc23.x86_64.rpm  GeoIP-data-20090201-1.el5.centos.x86_64.rpm
rpm -i GeoIP-devel-1.6.6-1.fc23.x86_64.rpm
yum install -y libxml2-devel doxygen zlib-devel git flex
git clone https://github.com/csanders-git/ModSecurity
cd ModSecurity
git checkout libmodsecurity
sh build.sh
git submodule init
git submodule update
./configure --with-yajl=/opt/lloyd-yajl-66cb08c/build/yajl-2.1.0/ --with-curl=/opt/curl/
make
make install
```

### nginx-connector (openresty) 

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

## Ubuntu 15.04

Provided by @m2n and @akoul

### libModSecurity

```sh
$ sudo apt-get install g++ flex bison curl doxygen libyajl-dev libgeoip-dev libtool dh-autoreconf libcurl4-gnutls-dev libxml2 libpcre++-dev libxml2-dev
$ cd /opt/
$ git clone https://github.com/SpiderLabs/ModSecurity
$ git checkout libmodsecurity
$ sh build.sh
$ git submodule init
$ git submodule update #[for bindings/python, others/libinjection, test/test-cases/secrules-language-tests]
$ ./configure
$ make
$ make install
```