---
title: '使用dos2unix批量转换换行文件'
date: 2023-09-29 20:10:08
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
dos2unix是Linux下的一个用户转换格式的程序，由于windows上文件的结束符和linux上的不同,那么在windows上编写的文件或者是脚本在Linux上就会遇到类似于下面的错误
```bash
sudo  find  .  -name  "*.go"  |  xargs  dos2unix 
或将当前路径下的所以的文件都变为unix格式
sudo find . -type f | xargs dos2unix
反过来
sudo  find  .  -name  "*.go"  |  xargs  unix2dos 
```
