---
title: '使用dd命令整盘备份/还原系统盘'
date: 2022-09-26 15:32:17
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 备份
```
sudo dd bs=512 count=123729920 if=/dev/sdb | xz -9e > /windows.img.xz
//其中bs的数字为一个扇区(sector)的大小
//其中count的数字为fdisk -u -l 中最后一个end+1
```
# 恢复
```
xz -d /windows.img.xz | dd of=/dev/sda
```

# 磁盘备份

### 磁盘➡️磁盘

```shell
$ sudo dd if=/dev/sda of=/dev/sdb
```

**dd命令是按照文件块操作,如果不指明块的大小和数量,dd命令会对全部硬盘进行复制,并不会跳过磁盘未使用的空间.一定要确保目标文件比原来的磁盘文件大.**

### 磁盘➡️镜像

```shell
$ sudo dd if=/dev/sda of=~/disk1.img
```

**需要在livecd环境操作,不要把本机硬盘备份到本机,那样只会无限递归**

### 磁盘➡️压缩镜像

```shell
$ sudo dd if=/dev/sda | gzip > disk.img.gz
$ sudo dd if=/dev/sda | bzip2 > disk.img.bz2
```

# 磁盘恢复

### 磁盘➡️磁盘

```shell
$ sudo dd if=/dev/sda of=/dev/sdb
```

### 镜像➡️磁盘

```shell
$ sudo dd if=~/disk1.img of=/dev/sda
```

### 压缩镜像➡️磁盘

```shell
$ sudo gzip -dc /disk.img.gz | dd of=/dev/sda
```

**不过既然是烧写磁盘这种小事,完全可以使用现成的程序来做,比如[balenaEtcher](https://www.balena.io/etcher/),~~就像最终幻想已经安装在PC上,蒂法穿什么还不是我说了算?~~**

# 显示dd进度

使用progress命令]
