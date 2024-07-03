---
title: '编译安装curl'
date: 2023-06-06 20:20:19
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
本想测试openkylin1.0Beta能否安装homebrew,没想到当头一棒的问题居然是开放麒麟的curl默认就和系统上已经安装的软件冲突,这可真是闻所未闻的事
# 下载
```bash
wget https://curl.se/download/curl-8.1.1.tar.bz2
```
# 解压
```bash
tar xvf curl-8.1.1.tar.bz2
```
# 配置
```bash
./configure  --without-ssl --prefix=/usr/local
# 参数可以根据自己的需要选择,如果想查看都有什么参数可选,运行
./configure --help
```
# 编译
```bash
make
```
# 安装
```bash
make install
```
# 生效
```bash
sudo ldconfig
```
![2023-05-28-21.24.03.png](https://loli.tc/images/2023-05-28-21.24.03.png)
