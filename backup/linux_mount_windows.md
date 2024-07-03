---
title: 'Linux下正确挂载Windows分区'
date: 2022-10-10 11:37:50
tags: [双系统]
published: true
hideInList: false
feature: 
isTop: false
---
在某个系统的微信群中,一个自信到自负的人,纠结了好几天关于挂载Windows分区的问题,群里很多人帮他,包括我,但是他从写错格式到占用系统目录,所有能犯的错犯了一遍,包括但不限于挂载到`/home`、`/mnt`、`/tmp`、`media`等位置,然而他总是很自信,坚信不是位置选错了,一直在坚持找到"问题的根源"

<!-- more -->

<iframe width="100%" height="550" src="https://www.youtube.com/embed/rCpAz0Dwevc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

如果视频无法显示,点击[这里](http://player.bilibili.com/player.html?aid=431389295&bvid=BV1tG411E7Ys&cid=857531615&page=1)查看

# 0x01
找到需要挂载分区的名称

```shell
$ lsblk
```
找到分区对应的名称

我这里是`nvme0n1p3`

# 0x02

进入`/dev/disk/by-uuid`

输入`ls -al`就能看见设备对应的uuid

记住这个uuid

# 0x03

新建一个挂载点,在你的家目录下

```shell
$ mkdir ~/windows
```

# 0x04

编辑fstab

用vim或者nano文本编辑器打开`/etc/fstab`

添加一行

```shell
UUID=xxxxx  <你的挂载点绝对路径,如/home/zen/windows>    ntfs    auto,rw,user,uid=1000,gid=1000  0   0
```

**中间分隔用tab不是空格**

#0x05

验证是否正常挂载**非常重要**

正常Linux系统如果fstab错误,重启后会进入紧急模式

如果你没给自己挖坑让终端也显示中文的话,改回来就好

如果你碰巧选择了UOS这种锁死紧急模式的系统,那么你只能学着用livecd改回去了

所以如果你不想给自己找麻烦

**一定要验证**

**一定要验证**

**一定要验证**

如我视频里演示

`fstab`写完之后

`mount -a`会报错找不到UUID(我少写了一位)

修改正确后再次执行`mount -a`

如果没有报错并能正常在挂载点看到文件

就说明设置正确

可以放心重启了

# tips

如果你在Windows下选择了 睡眠、休眠、混合睡眠或者在快速启动的就绪状态下切换到Linux系统，这个挂载点的文件会不可读写,虽然可以用sudo霸王硬上,但是不建议这么做

如果你不想每次都被这些问题困扰

在Windows下关闭休眠文件

用管理员权限打开powershell

输入

```powershell
powercfg -h off
```