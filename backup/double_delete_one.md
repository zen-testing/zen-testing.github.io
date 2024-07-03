---
title: '双系统在Windows下安全删除Linux的方法'
date: 2022-09-26 16:20:31
tags: [Linux,Windows,双系统]
published: true
hideInList: false
feature: 
isTop: false
---

# 以这种常见的分区方式为例
windows所在磁盘:efi(esp)分区,系统分区
Linux所在磁盘:efi分区,系统根分区,用于双系统间数据交换的exfat分区
![磁盘管理界面](https://s1.ax1x.com/2022/09/05/vT6pex.png)
# 下载diskgenius

[官网](https://www.diskgenius.cn/)下载正常64位版本即可,不要抖机灵随便找个绿色专业版

!{直接去官网}(https://s1.ax1x.com/2022/09/05/vT6FYD.png)

一定要下载[64位版本](https://download.eassos.cn/DG5451412_x64.zip)

![下载64位版本](https://s1.ax1x.com/2022/09/05/vT6iFO.png)

#  运行主程序

![运行主程序](https://s1.ax1x.com/2022/09/05/vT69w6.png)

# 找到不需要的文件并删除

### Windows的efi应该有如下文件夹

![Windows应该有的boot文件](https://s1.ax1x.com/2022/09/05/vT6kfe.png)

### Linux的efi应该有如下文件夹

![其他Linux系统应该有的boot文件](https://s1.ax1x.com/2022/09/05/vT6CTK.png)

**如果你的电脑安装的是开放麒麟这种比较奇葩的不允许存在多efi分区的Linux系统,并且一定要覆盖原文件的奇葩,一定要记得在进入系统后马上重建grub菜单(`sudo grub-update`),否则就会像某位热心网友一样,莫名其妙就被删除了Windows启动项**

# 进阶

### Linux下删除Windows

方法:
1. 挂载Windows所在硬盘的efi分区
2. 删除Windows相关内容
3. 挂载Linux所在分区
4. 删除有可能存在的Windows相关内容

### Linux下删除Linux

方法:
**必须一次成功,如果未完全清理,下次开机就会进入grub报错菜单**
1. 挂载/boot/efi分区(很可能已经挂载) **需要使用root用户,sudo不可以**
2. 删除Linux相关内容
3. 挂载Windows的efi分区
4. 删除Linux相关内容