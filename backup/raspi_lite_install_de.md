---
title: '树莓派4B lite 系统安装桌面环境'
date: 2022-10-12 23:21:27
tags: [Raspberry]
published: true
hideInList: false
feature: 
isTop: false
---
经过长时间的测试发现

ssh终端卡顿 回显不及时 甚至连本地连接终端都会卡一下

就是配置低带不动的原因

安装其他系统没有树莓派自家软件工具支持

所以只能尝试使用32位版本的lite系统

安装一个可用的轻量级桌面

最终选择了`LXQT`桌面

不是因为它最好

只是没有其他可选了

```shell
$ sudo apt install lxqt
```

登录管理器使用`slim`

```shell
$ sudo apt install slim
```