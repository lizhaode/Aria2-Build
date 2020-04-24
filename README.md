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

2. Zlib

[Zlib](https://www.zlib.net/zlib-1.2.11.tar.gz) 从2017年到现在一直没有更新，所以直接下载编译就行

```bash
./configure
make
make install
```

3. c-ares

从 [官网](https://c-ares.haxx.se/) 下载最新版本

```bash
./configure
make && make install
```

4. libexpat

同样从 [官网](https://github.com/libexpat/libexpat/releases)下载最新版

```bash
./buildconf.sh
./configure
make && make install
```

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

有可能因为 zlib 编译不过，可以选择添加参数 `--without-libz-prefix` 不适用 zlib 来编译


### 编译 Aria2

首先还是从 GitHub 上 clone 代码

```bash
autoreconf -i
./configure --enable-static=yes --with-libuv --with-libexpat ARIA2_STATIC=yes --with-libexpat
make && make install
```
