---
title: 'ffmpeg 内嵌双语字幕'
date: 2024-03-01 22:23:33
tags: [ffmpeg]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
ffmpeg -i "Jimmy Fallon and Meghan Trainor - Wrap Me Up.mp4" -vf "subtitles=chi.srt,subtitles=eng.srt:force_style='MarginV=30'" once.mp4
# -vf: 嵌入第二个字母的时候设置偏移量(距离底部)
```