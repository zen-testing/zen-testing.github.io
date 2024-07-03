---
title: 'WSL2安装中文字体'
date: 2022-09-26 21:10:11
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
wsl是没有中文字体的,所以在安装使用Firefox等软件时,无法正常显示中文字体,所以我们可以通过使用Windows自带字体的方式,来实现快速安装中文字体(以Ubuntu为例)

<!-- more -->

我们只需要将Windows下的字体目录链接到WSL目录下即可

```shell
sudo ln -s /mnt/c/Windows/Fonts /usr/share/fonts/font
```
然后
```shell
# echo "LANG=zh_CN.UTF-8" >> /etc/default/locale
# echo "LANGUAGE='zh_CN:zh'" >> /etc/default/locale
sudo gedit /etc/default/locale将如下添加进去,保存
LANG=zh_CN.UTF-8
LANGUAGE="zh_CN:zh"
# 安装中文字体(这里以 文泉驿微米黑为例):
sudo apt-get install ttf-wqy-microhei
# 重启,搞定 
```
