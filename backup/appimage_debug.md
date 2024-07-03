---
title: 'QT相关报错'
date: 2022-09-26 18:18:28
tags: [AppImage,Linux]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
Qt Warning: Ignoring XDG_SESSION_TYPE=wayland on Gnome. Use QT_QPA_PLATFORM=wayland to run on Wayland anyway.
```
解决方法
```shell
$ cd /etc/gdm3
$ sudo gedit custom.conf
定位到 WaylandEnable=false 删除前面的注释
reboot
```
