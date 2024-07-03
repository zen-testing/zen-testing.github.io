---
title: 'Ubuntu使用Intel AX200网卡'
date: 2022-09-26 19:21:26
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
把大象装冰箱只需要三步,网卡驱动同理

----

环境:Windows10(sda)esp in sda1 Ubuntu18.04.3LTS(sdb) esp in sdb1
kernel=5.0
由于AX200的最低内核版本要求是5.1,并且本人觉得万一以后在有个AX250什么的再更新内核挺麻烦的,直接一步到位更新个目前最新版本
## 下载内核文件
在Ubuntu[官网](https://kernel.ubuntu.com/~kernel-ppa/mainline/)上下载内核文件备用,网站经常连不上,也可以直接使用`wget`命令下载

`wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.4.2/linux-headers-5.4.2-050402_5.4.2-050402.201912042231_all.deb`

`wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.4.2/linux-headers-5.4.2-050402-generic_5.4.2-050402.201912042231_amd64.deb`

`wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.4.2/linux-image-unsigned-5.4.2-050402-generic_5.4.2-050402.201912042231_amd64.deb`

`wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.4.2/linux-modules-5.4.2-050402-generic_5.4.2-050402.201912042231_amd64.deb`

## 下载网卡驱动

在Intel[官网](https://www.intel.com/content/www/us/en/support/articles/000005511/network-and-io/wireless-networking.html)下载对应网卡的驱动文件备用

同理也可使用`wget`命令下载

`wget https://wireless.wiki.kernel.org/_media/en/users/drivers/iwlwifi/iwlwifi-cc-46.3cfab8da.0.tgz`

解压出`iwlwifi-*.ucode`即为驱动程序文件

## 完善安装环境

如果之前更改过安装源,需要重新添加一个Ubuntu官方源

`sudo gedit /etc/apt/sources.list`

文件尾部追加

`deb http://security.ubuntu.com/ubuntu bionic-security main`

更新软件包

`sudo apt-get update`

`sudo apt-get upgrade`

玄学

`sudo apt-get install libssl1.1`

## 更新内核

安装四个下载好的内核包

`sudo dpkg -i *.deb`

## 重启

`sudo reboot`

## 安装驱动

移动驱动文件到系统的驱动程序目录

`sudo cp *.ucode /lib/firmware`

## 重启

`sudo reboot`

## 完成

我,秦始皇,打钱
