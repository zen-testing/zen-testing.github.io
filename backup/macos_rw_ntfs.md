---
title: 'Mojave原生读写NTFS(有风险)'
date: 2022-09-26 17:49:02
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
+ 插上磁盘
  
![wNKJVe.png](https://s1.ax1x.com/2020/09/11/wNKJVe.png "桌面上会出现盘符,但这样打开只能读不能写")

+ 打开终端
![wNM1Wn.png](https://s1.ax1x.com/2020/09/11/wNM1Wn.png "查看磁盘的 Name")
<center>如图Elements就是我磁盘的Name</center>

+ 然后打开vim
![wNQ2j0.png](https://s1.ax1x.com/2020/09/11/wNQ2j0.png "sudo vim /etc/fstab")

+ 写入指令
![wNleUg.png](https://s1.ax1x.com/2020/09/11/wNleUg.png "LABEL=Elements	none	ntfs	rw,auto,nobrowse")

+ 保存文本后重启电脑
这时候会发现桌面和finder里面都没有磁盘
![wN8QxA.png](https://s1.ax1x.com/2020/09/11/wN8QxA.png "磁盘是挂在/Volumes下")

+ 为了方便使用在桌面创建快捷方式
![wNGpeP.png](https://s1.ax1x.com/2020/09/11/wNGpeP.png "在桌面创建快捷方式")

+ 卸载磁盘
![wNG8SJ.png](https://s1.ax1x.com/2020/09/11/wNG8SJ.png "或者直接用命令卸载")

+ 缺点
磁盘的省电功能不可用,通电过程中不会休眠,即使长时间未读写

+ 后果
如果你在macOS/Windows共用一块硬盘,那么你就会发现macOS读取/写入后的文件夹在Windows下是被改写的,只能通过管理员重新授权,很麻烦