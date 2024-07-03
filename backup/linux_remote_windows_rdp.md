---
title: 'Linux连接局域网内Windows远程桌面'
date: 2022-10-23 17:28:39
tags: [Linux,Windows,RDP]
published: true
hideInList: false
feature: 
isTop: false
---
使用Windows自带的远程桌面

<!-- more -->

# Linux端安装

`rdesktop`

# Windows端允许远程桌面

取消勾选`网络级别验证 `字样

# 通过命令连接

`rdesktop -f -a 16 192.168.1.112`

# 参数说明

参数|说明
---:|:---
-u| user name
-p| password (- to prompt)
-f| full-screen mode
-V| tls version (1.0, 1.1, 1.2, defaults to negotiation)
-m| do not send motion events
-T| window title
-a| connection colour depth example 16
-z| enable rdp compression
-v| enable verbose logging
-g|desktop geometry (1920*1080)

-f 全屏模式，中途可使用Ctrl+Alt+Enter组合键退出全屏
-g workarea 可自适应铺满当前linux窗口大小
-r clipboard:PRIMARYCLIPBOARD 允许在远程主机和本机之间共享剪切板

# 效果图

![效果图](https://s1.ax1x.com/2022/10/23/xgLvaF.jpg)