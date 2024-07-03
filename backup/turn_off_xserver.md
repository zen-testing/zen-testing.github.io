---
title: 'linux关闭xServer'
date: 2022-09-26 19:20:43
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
如果想切换至纯粹一点的命令字符console下,一般人会认为切换Ctrl+Alt+F1(或者F2-F6都可以).

默认下,Ctrl+Alt+F7是图形界面(当然,各个Linux发行版本会有所差异).

这种情况依然没有退出X Server,只是多了一种命令的tty而已.

如果真正进入不加载X window的方式:

1. 一般选择编辑`/etc/inittab`

修改`id:5:initdefault:`为`id:3:initdefault`

(5为GUI,3为命令行)

2. 另外一种方式更为妥当,直接在运行的GUI下,切换命令

```shell
/etc/init.d/gdm stop
#或者
/etc/init.d/kdm stop
#或者
systemctl stop gdm
#或者
systemctl stop kdm
```

关闭相应的GUI服务即可


3. 第三种方式更为简单,直接在X Window下的模拟shell下输入`init 3`(前提有root权限),即可关闭XServer

此种情况多用于安装如Nvidia显卡驱动,必须退出X Server,也是一种便利.