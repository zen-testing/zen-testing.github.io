---
title: '解决Linux下挂载的NTFS分区(Windows分区)只读问题'
date: 2022-09-26 19:05:13
tags: [双系统,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

>众所周知,在liunx系统中访问不了Windows系统所在磁盘或者文件管理器中Windows所在磁盘出现❌或🔒是Windows快速启动的休眠文件导致的,只要在Windows下完整重启或者关闭快速启动功能或休眠文件即可,但是有一种特殊(扛精)情况:我已经在linux下删掉了Windows的关键文件,Windows系统已经无法启动,手头暂时也没有可用的PE,我现在只想在我的UOS系统下修复这个问题,下面就是这种极端情况的处理方法,方法同样适用于Debian系的其他发行版

<!-- more -->

```cmd
remove_hiberfile
              When  the  NTFS  volume is hibernated, a read-write mount is denied
              and a read-only mount is forced. One needs either to resume Windows
              and  shutdown it properly, or use this option which will remove the
              Windows hibernation file. Please note, this means  that  the  saved
              Windows session will be completely lost. Use this option under your
              own responsibility.
```

这个参数用来在linux下挂载处于休眠模式(睡眠\混合睡眠\快速启动待命状态)的硬盘(分区),这后面的提示大致就是说,你清楚你在干什么,休眠文件保存了什么,你知道你在删除什么

```shell
$ sudo umount /mnt/win10 #这里假设自动挂载点为/mnt/win10
$ sudo ntfs-3g -o remove_hiberfile /dev/sda1 /mnt/win10 # 取消休眠状态并重新挂载/dev/sda1到/mnt/win10
```