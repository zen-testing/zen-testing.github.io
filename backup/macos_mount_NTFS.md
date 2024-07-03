---
title: 'macos原生挂载NTFS功能'
date: 2022-10-10 15:52:21
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
假设硬盘名称为`exchange`

```shell
$ sudo diskutil list 
$ sudo distutil info exchange
$ echo "UUID=<THE UUID YOU COPIED> none ntfs rw,auto,nobrowse" >> /etc/fstab
```

重新插入硬盘

然后在/Volume中可以找到

为了方便使用

也可以

```shell
$ sudo ln -s /Volumes/exchange ~/Desktop/exchange && open ~/Desktop/exchange
```