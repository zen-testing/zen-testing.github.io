---
title: '双系统固定挂载Windows分区'
date: 2022-09-26 16:19:35
tags: [Linux,双系统]
published: true
hideInList: false
feature: 
isTop: false
---

# 查看硬盘信息

`$ sudo fdisk -l`

找到自己需要挂载的硬盘如`/dev/sda2`

# 创建挂载点文件夹

`$ sudo mkdir /home/zen/Windows`

# 挂载硬盘分区

`$ sudo mount /dev/sda2 /home/zen/Windows   # sda2后边一定不要加/`

# 查看分区id

`$ sudo blkid`

# 找到需要自动挂载的分区
/dev/sda2的UUID="xxxxx" TYPE="ntfs",这里的type如果是ext4,后边文件中选择ext4,否则选择对应的文件格式
编辑/etc/fstab文件

# 编辑开机时自动挂载
`$ sudo vim /etc/fstab`

```
# 在启动或在终端中输入mount -a时自动挂载,或者为noauto
# user 允许任何用户挂载设备,可选nouser,这样仅仅允许root用户挂载
# rw 挂载为读写权限,可选ro挂载为只读权限

# 添加一行
UUID=xxx /home/zen/Windows ntfs auto,user,rw 0 0
```
