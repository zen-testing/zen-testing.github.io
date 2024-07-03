---
title: 'ls只显示文件名/文件夹名的方法'
date: 2022-12-05 21:33:14
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# 只显示文件名
```shell
ls -l | grep ^[^d] | awk '{print $9}'
```
# 只显示文件夹名
```shell
ls -l |grep ^d | awk '{print $9}' 
```