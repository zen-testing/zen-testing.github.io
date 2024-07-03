---
title: 'UOS合并自动分区产生的不合理分区'
date: 2022-09-26 19:29:30
tags: [Linux,UOS,gparted]
published: true
hideInList: false
feature: 
isTop: false
---
>无论是deepin\uos\开放麒麟...
自动安装都会分出来一些无用的分区
资本家和股东认为这样很合理,并且他们会通过各种手段让消费者潜意识里也认为这样很合理
然而稍微懂电脑的人都知道,多一个从/拆分出来的独立分区都是给自己挖坑

# 0x01 这里以UOS一键安装为例

![直接选择立即安装](https://s1.ax1x.com/2022/08/28/vWRGsf.png)

# 0x02 一锤子买卖

/boot不用单独分出来,并且想合并回去很麻烦

# 0x03 决策是否关闭swap

如果你的电脑内存大于4g,关闭swap

```
sudo swapoff -a
```

# 0x04

RootB完全是一个"小事用不上,大事用不了"的存在

# 0x05

剩下几个分区,如果有重要数据,先备份到外部硬盘,操作完有需要再挪回来(我不用备份是因为我知道如何操作,但我不保证你一遍能看懂)

# 0x06 使用[gparted](https://downloads.sourceforge.net/gparted/gparted-live-1.4.0-5-amd64.iso)的liveCD进入系统

第一项就是,默认就会进入

![第一项就是](https://s1.ax1x.com/2022/08/28/vWRteS.png)

# 0x07 快捷键默认选项就可以

![默认选项就可以](https://s1.ax1x.com/2022/08/28/vWRmZD.png)

# 0x08 语言选择简体中文(输入26)

其实选什么关系不大

![选择你要用的语言](https://s1.ax1x.com/2022/08/28/vWRZqO.png)

# 0x09 默认使用图形界面(0)

![选择桌面环境](https://s1.ax1x.com/2022/08/28/vWRnde.png)

# 0x0A 进入桌面环境

![进入桌面环境](https://s1.ax1x.com/2022/08/28/vWRMid.png)

# 0x0B 创建三个挂载点

![创建三个挂载点](https://s1.ax1x.com/2022/08/28/vWRNdg.png)

分别挂载`/dev/sda3`,`/dev/sda5`,`/dev/sda6`到`/mnt/uosroot`,`/mnt/uosdata`,`/mnt/uosrec`

```shell
sudo mount /dev/sda3 /mnt/uosroot
sudo mount /dev/sda5 /mnt/uosdata
sudo mount /dev/sda6 /mnt/uosrec
```

# 0x0C 挂载三个分区

![分别挂载三个要修改的分区](https://s1.ax1x.com/2022/08/28/vWRuIH.png)

把`/mnt/uosdata/home`恢复到`/mnt/uosroot/home`下,需要带属性复制

```shell
sudo cp -a /mnt/uosdata/home /mnt/uosroot
```

把`/mnt/uosdata/opt`恢复到`/mnt/uosroot/opt`下,需要带属性复制

```shell
sudo cp -a /mnt/uosdata/opt /mnt/uosroot
```

把`/mnt/uosdata/root`文件文件夹恢复到`/mnt/uosroot/root`下,需要带属性复制

```shell
sudo cp -a /mnt/uosdata/root /mnt/uosroot
```

把`/mnt/uosdata/var`文件夹恢复到`/mnt/uosroot/var`下,需要带属性复制

```shell
sudo cp -a /mnt/uosdata/var /mnt/uosroot
```

# 0x0D 卸载所有分区

```shell
sudo umount /dev/sda3
sudo umount /dev/sda5
sudo umount /dev/sda6
```

# 0x0E 删除不必要的分区

包括`rootb`,`_dde_data`,`Backup`如果关闭了交换分区`swap`也可以删除

![右键delete就可以](https://s1.ax1x.com/2022/08/28/vWRQJA.png)

# 0x0F 右键根目录所在分区并选择扩容(resize)

矩形条左侧拉到最左右侧拉到最右,然后确定

![矩形条左侧拉到最左右侧拉到最右](https://s1.ax1x.com/2022/08/28/vWRlRI.png)

# 0x10 修改后效果

![修改后的分区状况](https://s1.ax1x.com/2022/08/28/vWRJL8.png)

# 0x11 无视警告后点击对号应用修改

![点击对号应用修改](https://s1.ax1x.com/2022/08/28/vWR1zt.png)

# 0x12 如果之前有很多数据 这里会比较慢

![如果之前有很多数据这里会比较慢](https://s1.ax1x.com/2022/08/28/vWR8QP.png)

# 0x13 应用成功后点击关闭

![应用成功后点击关闭](https://s1.ax1x.com/2022/08/28/vWWxN4.png)

# 0x14 打开一个新的终端(terminal)

桌面有图标,鼠标移动到图标上会显示为手掌,和正常习惯不一样,双击打开

# 0x15 挂载本地系统根分区

已知现在的根目录在`sda3`分区,卷标为`Roota`

先挂载sda3到/mnt

```shell
sudo mount /dev/sda3 /mnt
````

# 0x16 cd到根目录之后进入本机系统

```shell
cd /
sudo chroot /mnt
```

# 0x17 编辑fstab

```shell
nano /etc/fstab
```

如果刚才扩容的分区是sda3,那么就保存这条,带有`/boot`,`/boot/efi`字样的那条和带有`swap`字样的那条(如果你之前在本地系统关闭了交换分区,这里也可以删除)

![只保留部分](https://s1.ax1x.com/2022/08/28/vWRUoQ.png)

其中带有/的条目,前面`UUID=XXXX`改为`LABEL=Roota`(其中Roota是在gparted中的LABEL字段)

依次按下`ctrl+x`,`y`,`回车`保存退出

# 0x18 退出

输入`exit`退出`chroot`状态

# 0x19 重启

输入`reboot`重启电脑

# 0x1A重启之后正常进入系统

![重启之后正常进入系统](https://s1.ax1x.com/2022/08/28/vWRdij.png)