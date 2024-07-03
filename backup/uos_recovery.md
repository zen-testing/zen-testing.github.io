---
title: 'UOS维护模式'
date: 2022-09-26 19:30:37
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---

# ~~诊断模式~~

主要进行一些系统修复\安装驱动等操作

1. 重启机器进入启动的grub菜单
2. 按E或者TAB键,进入编辑模式
3. 在linux所处那行的行尾加入`systemd.debug_shell=1`
4. `crtl X` 或者`F10` 保存进入系统
5. 进入系统后按`CRTL+ALT+F9`进入` tty9`模式,即可拥有root权限

# ~~单用户模式~~

对于一些修改密码,查看分区等操作可以通过进入单用户模式

1. 开机按e进入grub菜单编辑模式
2. 找到linux那行,把`ro splash quiet`替换成`rw single init=/bin/bash`
3. 进入系统后按`CRTL+ALT+F9`进入系统即可进入单用户模式

# LiveCD模式

对于系统已经损坏无法进入进行操作的情况下可以选择进入livecd模式进行一些备份等操作.

1. 使用启动盘引导系统进入grub菜单
2. 按E或者TAB键,进入编辑模式
3. 删除`livecd-installer`然后`ctrl+x`保存启动
4. 进入livecd进行维护