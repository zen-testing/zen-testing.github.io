---
title: 'snap store status-code=409 解决方案'
date: 2022-12-02 17:26:48
tags: [snap]
published: true
hideInList: false
feature: 
isTop: false
---
假设报错内容如下
```shell
unable to install xmind: status-code=409 kind=snap-change-conflict message=snap"xmind"has "install-snap"change in progress
```

终端输入`snap changes`检查状态
```shell
zen:~$ snap changes
ID   Status  Spawn                     Ready                     Summary
6    Done    6 days ago, at 16:03 CST  6 days ago, at 16:04 CST  自动刷新 snap "snapd"
7    Doing   today at 16:40 CST        -                         Install "xmind" snap from "latest/stable" channel
```
找到正在安装的软件，如`xmind`将其强制关闭
```shell
# 其中 7 指的是事件序号
zen:~$ snap abort 7
```