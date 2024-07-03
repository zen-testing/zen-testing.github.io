---
title: '开放麒麟安装过程中报错解决'
date: 2022-09-26 18:17:28
tags: [openKylin]
published: true
hideInList: false
feature: 
isTop: false
---

# 关键字:
`没有Releases文件` `没有数字签名` `no pubkey`
![安装日志](https://s1.ax1x.com/2022/09/07/vH0Wtg.png)
### 原因
无法连接服务器导致无法验证公钥
### 解决办法 
1. 断网安装
2. 安装后更换apt源之后系统才能正常下载软件
```shell
deb http://mirror.lzu.edu.cn/openkylin/ yangtze main cross pty
deb http://mirror.lzu.edu.cn/openkylin/ yangtze-security main cross pty
deb http://mirror.lzu.edu.cn/openkylin/ yangtze-updates main cross pty
deb http://mirror.lzu.edu.cn/openkylin/ yangtze-proposed main cross pty
```