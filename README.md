# Aria2-Build

记录在 Ubuntu 上编译安装 Aria2 的方法


### 背景

Ubuntu 这些 Linux 系统，直接使用 `apt install` 安装，版本都不是最新的

因此手动编译安装最新版本


### 依赖

`apt install` 安装一些开发工具包 

pkg-config  
libcppunit-dev  
autoconf  
automake  
autotools-dev  
autopoint  
libtool


### 编译安装一些依赖

1. OpenSSL

从 [OpenSSL](https://www.openssl.org/source/) 下载最新版本的源码

执行命令 `./Configure linux-x86_64 no-asm shared`

然后 `make && make install`

一般每个包安装完成，最好都执行一下 `ldconfig` 或者重启

2. Zlib

Zlib 从2017年到现在一直没有更新，所以直接安装就行

```bash
apt install zlib1g-dev
```

3. c-ares

从 [官网](https://c-ares.haxx.se/) 下载最新版本

```bash
./configure
make && make install
```

4. libxml2

从 [Gitlab](https://gitlab.gnome.org/GNOME/libxml2)下载最新版

```bash
./configure
make && make install
```

如果是新版的 ubuntu ，可以直接 `apt install libxml2-dev` 与git上的版本一致


5. sqlite

从[官网](https://www.sqlite.org/download.html) 下载时，需要注意，是下载带有 autoconf 的源码

```bash
./configure
make && make install
```

6. libssh2

同样从 [官网](https://www.libssh2.org/)下载最新版

```bash
./configure
make && make install
```

如果不需要 SFTP 功能，可以不装


7. libuv

[官网](https://dist.libuv.org/dist/)下载最新版

```bash
./autogen.sh
./configure
make && make install
```


### 编译 Aria2

首先还是从 GitHub 上 clone 代码

```bash
autoreconf -i
./configure --enable-static=yes --with-libuv --with-libexpat ARIA2_STATIC=yes --with-libexpat
make && make install
```
