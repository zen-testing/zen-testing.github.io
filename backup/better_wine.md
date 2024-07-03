---
title: '完善WineHQ环境'
date: 2022-09-26 21:31:55
tags: [Linux,WineHq]
published: true
hideInList: false
feature: 
isTop: false
---
# 安装WineTricks(Wine安装助手)

```shell
$ winetricks
```

如果提示 `Wine cannot find the ncurses library (libncurses.so.5).` 则安装`ncurses`

```shell
$ sudo apt install libncurses5 libncurses5:i386 # 安装32位与64位curses
```

# 安装mono
```shell
$ sudo wine start  wine-mono-6.3.0-x86.msi
```
# 安装gecko
```shell
$ sudo wine start wine-gecko-2.47.2-x86.msi
$ sudo wine start wine-gecko-2.47.1-x86_64.msi
```

# 安装 必须的字体

```shell
$ winetricks corefonts
```

# 支持显示中文字体

```shell
$ winetricks richtx32
$ winetricks riched30 # 需要设置wget代理
$ winetricks riched20 # 需要设置wget代理
$ winetricks cjkfonts # 安装字体
```