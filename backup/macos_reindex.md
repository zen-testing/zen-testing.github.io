---
title: 'macOS重置聚焦搜索'
date: 2022-09-26 17:29:20
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
Mac电脑的Spotlight(聚焦搜索)可以用来全系统的搜索文件及应用程序,但偶尔用户会遇到不显示文件和应用程序的情况,其实重置一下Spotlight就能解决这个问题

<!-- more -->

1. 关闭spotlight
```shell
$ sudo mdutil -a -i off
```
2. 不加载控制聚焦参数的文件
```shell
$ sudo launchctl unload -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
```
3. 重新加载控制聚焦参数的文件
```shell
$ sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.metadata.mds.plist
```
4. 打开聚焦
```shell
$ sudo mdutil -a -i on
```
----
以上操作需要关闭系统完整性