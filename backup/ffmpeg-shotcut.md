---
title: 'ffmpeg 获取视频截图'
date: 2024-03-01 22:08:41
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
ffmpeg -ss 00:00:00.000 -t 100 -r -1 -i in.mp4 -f image2 -y %03d.jpg
```
-r 截取帧率,每秒多少帧 0.2表示每秒0.2帧,即5秒1帧
-t 使用多长时间内视频