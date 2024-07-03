---
title: 'ffmpeg仅测试输入文件,丢弃输出'
date: 2023-11-07 10:12:06
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
[原文地址](https://trac.ffmpeg.org/wiki/Null)

<!-- more -->

```bash
ffmpeg -i input -f null -
```