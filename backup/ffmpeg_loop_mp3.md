---
title: 'ffmpeg将一段音频循环播放20遍'
date: 2024-06-12 08:42:32
tags: [ffmpeg,AI]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
ffmpeg -stream_loop 20 -i input.mp3 -c copy output.mp3
```
将"input.mp3"替换为您的输入音频文件名，"output.mp3"替换为您想要输出的文件名。