---
title: '获取pip安装包的缓存 以便迁移到断网环境安装'
date: 2024-05-07 17:52:15
tags: [python]
published: true
hideInList: false
feature: 
isTop: false
---
联网电脑安装后文件保存在 `~/.cache/pip`文件夹
打包这个文件夹转移到断网电脑
断网电脑使用`RUN pip install <package name> --break-system-packages`直接安装
