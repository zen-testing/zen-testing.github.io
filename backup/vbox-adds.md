---
title: 'VirtualBox安装的Linux系统中安装增强功能'
date: 2022-09-26 20:34:45
tags: [VirtualBox,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

以UOS为例

<iframe width="100%" height="480" src="https://player.bilibili.com/player.html?aid=430302425&bvid=BV19G411G7fr&cid=825341118&page=1" frameborder="0" allow="accelerometer; encrypted-media; gyroscope; picture-in-picture,enablejsapi" allowfullscreen></iframe>

# 文字说明

首先在任务栏上点击`安装增强功能`

```shell
$ sudo mount /dev/cdrom /mnt # 挂载增强功能安装盘
$ cd /mnt # 进入目录
$ sudo ./VBoxLinuxAdditions.run # 运行安装程序
$ sudo systemctl reboot # 重启电脑
```