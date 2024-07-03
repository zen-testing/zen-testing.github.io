---
title: '自动挂载硬盘实现所有用户可读写'
date: 2022-09-26 15:30:45
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 查看硬盘信息
`sudo fdisk -l`
# 找到自己需要挂载的硬盘
如`/dev/sda2`
# 创建挂载点文件夹
`sudo mkdir /mnt/disk1`
# 挂载硬盘分区
`sudo mount /dev/sda2 /mnt/disk1 `
# 查看分区id
`sudo blkid`
# 编辑/etc/fstab文件
`sudo vim /etc/fstab`
```shell
# 在启动或在终端中输入mount -a时自动挂载,或者为noauto
# user 允许任何用户挂载设备,可选nouser,这样仅仅允许root用户挂载
# rw 挂载为读写权限,可选ro挂载为只读权限
UUID=xxx /mnt/disk1 ext4 auto,user,rw,uid=1000,gid=1000 0 0
```
# 验证
输入`sudo mount -a`
如果有报错重新修改
如果不验证的话下次开机直接进入紧急模式,重新编辑这个文件也能解决
