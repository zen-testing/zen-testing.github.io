---
title: 'Android设备实现网络adb连接'
date: 2022-09-26 15:12:27
tags: [adb,Android]
published: true
hideInList: false
feature: 
isTop: false
---

本文以Mate 30 Pro为例,使用adb工具实现网络连接
----
## 明确手机此时的IP地址

![GXSKr6.png](https://s1.ax1x.com/2020/04/13/GXSKr6.png)

## 在开发者选项中启用调试

![GXS3Ie.png](https://s1.ax1x.com/2020/04/13/GXS3Ie.png)

## 打开一个terminal,输入命令

`adb connect 192.168.31.69:5555`

报错`unable to connect to 192.168.31.69:8880: Connection refused`

## 这时如果报错连接被重置,ping一下这个地址,确认连接正常

`ping 192.168.31.69`

![GXS1aD.png](https://s1.ax1x.com/2020/04/13/GXS1aD.png)

## 手机用线连接电脑后使用adb命令更改端口

![GXSlVO.png](https://s1.ax1x.com/2020/04/13/GXSlVO.png)

这时手机上会要求授权

![GXSGPH.png](https://s1.ax1x.com/2020/04/13/GXSGPH.png)

端口号理论上可以改成0-65535,选择你的幸运数字

## 使用网络调试

拔掉数据线,再试一次网络调试,有可能要求重新授权

![GXSJGd.png](https://s1.ax1x.com/2020/04/13/GXSJGd.png)

## 之后就可以为所欲为了
