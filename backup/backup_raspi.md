---
title: '树莓派系统整体备份'
date: 2022-09-26 18:19:10
tags: [Raspberry]
published: true
hideInList: false
feature: 
isTop: false
---

看到的一个youtuber的视频介绍的工具挺不错,正好手头手头一个树莓派设备身兼数职:作为Linux平台廉价的硬件跑高负载任务不心疼,作为网络机顶盒刷kodi看电视直播,作为openwrt科学上网,作为打印机服务器等等,每次转变一个角色就要重刷系统重新安装软件确实很麻烦,做好几个备份每次只要恢复就直接处于就绪状态是个省时间的好主意

----

<iframe width="560" height="315" src="https://www.youtube.com/embed/k61s3_7nyS0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# 以下是我的操作

我的磁盘状态,需要把sda备份到sdb
```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       117G  8.5G  103G   8% /
devtmpfs        1.7G     0  1.7G   0% /dev
tmpfs           1.8G     0  1.8G   0% /dev/shm
tmpfs           1.8G   10M  1.8G   1% /run
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           1.8G     0  1.8G   0% /sys/fs/cgroup
/dev/sda1       253M   49M  204M  20% /boot
tmpfs           361M  8.0K  361M   1% /run/user/1000
/dev/sdb1       670G  435G  235G  65% /media/pi/Gloway720
```

执行备份命令

`$ sudo dc3dd if=/dev/sda of=/media/pi/Gloway720/backup.img`

从固态硬盘(NVME)复制到固态硬盘(SATA)

均插在USB3.0Port上,鼠标键盘均已拔出,使用网线连接,操作使用远程ssh连接

备份过程中任何操作都会有几率让硬盘断电报错

报错信息

```
writing to `/media/pi/Gloway720/backup.img': Input/output error
```
使用带辅助供电的USB线缆重新接驳状况改善,但依然不能在备份过程中对目标磁盘进行IO操作,否则依然报错

备份会生成与硬盘相同大小的IMG文件,我一开始还天真的

`$ sudo dc3dd if=/dev/sda of=/home/pi/backup.img`

用时1h51m25s02mm生成的img文件大小为
```
$ du -h backup.img
120G	backup.img
```

压缩命令
`# ./pishrink.sh ../backup.img`
```
$ du -h backup.img
11G	backup.img
```
继续压缩

`$ XZ_OPT='-9ek --threads=0' tar -Jcvf backup.img.tar.xz`

得到最终的档案大小
```
$ du -h backup.img.tar.xz
5.8G	backup.img.tar.xz
```
# 测试其他系统
无法在open Euler系统上通过包管理器安装dc3dd
无法在open Euler系统上通过编译安装dc3dd
TF卡插入另一台deb系linux下安装dc3dd打包
无法通过PiShrink压缩 应该是因为不支持rpm系发行版
32G卡系统完成手动扩容后使用
通过tarxz压缩后文件大小5.78G
