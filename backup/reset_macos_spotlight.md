---
title: 'MacOS重置聚焦搜索'
date: 2023-09-29 19:20:49
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
Macintosh系统大版本更新的时候经常会发生聚焦搜索找不到任何文件,需要重置

<!-- more -->
```bash
sudo mdutil -i off /
sudo mdutil -E /
sudo mdutil -i on /
```