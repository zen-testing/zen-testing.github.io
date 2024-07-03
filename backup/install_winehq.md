---
title: '安装最新版WineHQ'
date: 2022-09-26 17:17:35
tags: [Linux,WineHq]
published: true
hideInList: false
feature: 
isTop: false
---

>网上能找到的教程都太过时了或者根本就不正确,剩下的就是像抄作业一样错误答案原封不动抄上去,没办法只能自己记录一下安装过程

>直接使用Debian或Ubuntu安装没有任何技术含量可言,都是编译好的二进制文件,apt直接安装

>这里使用UOS家庭版纯手工安装WineHQ x64

# 需要提前安装的依赖
```shell
$ sudo apt-get install bison flex gcc-mingw-w64 libasound2-dev libpulse-dev libdbus-1-dev libfontconfig-dev libgnutls28-dev libjpeg62-turbo-dev libpng-dev libtiff-dev libgl-dev libunwind-dev libxml2-dev libxslt1-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libmpg123-dev libosmesa6-dev libsdl2-dev libudev-dev libvkd3d-dev libvulkan-dev libcapi20-dev liblcms2-dev libcups2-dev libgphoto2-dev libsane-dev libgsm1-dev libkrb5-dev libldap2-dev samba-dev ocl-icd-opencl-dev libpcap-dev libusb-1.0-0-dev libv4l-dev
$ aptitude install libfreetype6-dev:i386 libfreetype6-dev
#给出的方案中选择一个最优解,安装软件并不会卸载其它软件的方案
```
# 下载源码包

```shell
$ wget https://dl.winehq.org/wine/source/7.x/wine-7.10.tar.xz
```

# 编译安装

```shell
# 由于UOS中sudo有时间限制,但是编译又需要很长时间,所以还是尽量直接使用root用户
$ ./configure --enable-win64
$ sudo make
$ sudo make install
```
# 完成

![编译完成](https://github.com/zhangyiming748/zhangyiming748.github.io/raw/master/img/Wine/aftermake.webp)

![安装完成](https://github.com/zhangyiming748/zhangyiming748.github.io/raw/master/img/Wine/afterinstall.webp)
