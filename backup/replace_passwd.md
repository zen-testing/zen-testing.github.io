---
title: 'Linux系统使用LiveCD覆盖密码'
date: 2022-10-07 16:48:14
tags: [Linux,UOS]
published: true
hideInList: false
feature: 
isTop: false
---
这里使用统信uos进行演示,因为其他没有锁单用户模式的Linux发行版,可以直接通过进入单用户模式修改普通用户的密码

然而,在大家的不懈努力下,uos终于决定把单用户模式这个方法封死了

所以只能用liveCD的方式进行覆盖密码

<!-- more -->

<iframe width="100%" height="550" src="https://www.youtube.com/embed/yqldDNl0qHw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

如果视频无法显示,点击[这里](http://player.bilibili.com/player.html?aid=561328010&bvid=BV1Fe4y1q75H&cid=854912656&page=1)查看

# 正常流程安装系统

uefi方式安装系统,密码设置为"Qwert1234%"

# 进入live环境

进入并使用liveCD模式的方法在[另一篇教程](https://zhangyiming748.github.io/post/uos_recovery/#:~:text=%E5%8D%95%E7%94%A8%E6%88%B7%E6%A8%A1%E5%BC%8F-,LiveCD%E6%A8%A1%E5%BC%8F,-%E5%AF%B9%E4%BA%8E%E7%B3%BB%E7%BB%9F%E5%B7%B2%E7%BB%8F),直接看视频也行

进入之后,首先看一下本地硬盘上的系统所在的分区对应的设备名

比如我这里就是`sda2`

然后打开终端挂载这个设备

```shell
$ sudo mount /dev/sda2 /mnt
```

**选择挂载目录的时候,千万不要刻意去选择一些特殊的文件名**

~~在UOS家庭版体验群里,就有一个奇怪的人,偏偏去找一些特殊的目录挂载他的硬盘,出现问题之后,他会暗示自己不是目录的问题,坚信自己没有错,莫名其妙的自信,然后一直在群里询问,寻找所谓的"根源"问题~~

挂载成功之后cd到这个文件夹的上一层

假设你的挂载点是`/mnt`

那么就输入这样的命令

```shell
$ cd /
$ sudo chroot /mnt
```

切换到本地的系统

然后输入命令重设密码
假设我本地的用户名是`zen`
输入的命令就应该是

```shell
passwd zen
```

然后根据提示输入密码

回车之后再输入一遍相同的密码

提示密码修改成功之后,就可以输入exit退出了

然后正常关机

拔下U盘

再进入本地的系统之后,密码就是新更改之后的密码了

开机进入桌面后有可能会警告你密钥环改变

这时候通常有两种解决方法

1. 修改密码之前的密钥环文件
2. 努力回忆之前的密码

如果你选择删除,文件的位置在
```shell
/home/zen/.local/keyrings
```
