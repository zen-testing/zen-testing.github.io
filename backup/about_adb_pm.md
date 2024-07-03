---
title: 'adb shell pm命令详解'
date: 2022-09-26 15:11:28
tags: [adb,Android]
published: true
hideInList: false
feature: 
isTop: false
---

```
adb shell pm list packages -[option] 命令查看已经安装的应用,列出包名,后面加不同的后缀输出不同信息.

adb shell pm list packages     // 查看当前连接设备或者虚拟机的所有包
adb shell pm list packages -d    // 只输出禁用的包.
adb shell pm list packages -e    // 只输出启用的包.
adb shell pm list packages -s    // 只输出系统的包.
adb shell pm list packages -i   // 只输出包和安装信息(安装来源).
adb shell pm list packages -u   // 只输出包和未安装包信息(安装来源).
adb shell pm list packages -i   // 只输出包和安装信息(安装来源).
adb shell pm list packages -f   // 输出包和包相关联的文件
adb shell pm list packages -3   // 输出所有第三方包.
adb shell pm list packages -[option] "sina"   // 按照要求搜索包.

```