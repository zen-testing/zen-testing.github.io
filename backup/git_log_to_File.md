---
title: 'Git 历史提交日志导出到文件中'
date: 2023-11-07 10:57:53
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---

在项目根目录下执行命令,导出 git 提交记录到桌面

```bash
git log --pretty=format:"%ai , %an: %s" --since="100 day ago" >> ./commit.log
```
如果想导出某些提交者的提交记录,可以用`grep`过滤,比如我想导出`zen`这个人在项目中的提交记录:
```bash
git log --pretty=format:"%ai , %an: %s" --since="126 day ago" | grep "zen" >> ./commit.log
```
当然也可以导出成 Excel 文件
```bash
git log --date=iso --pretty=format:'"%h","%an","%ad","%s"' >> ./commit.log
```