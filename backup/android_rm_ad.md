---
title: 'Android删除广告跟踪文件'
date: 2024-05-05 20:20:33
tags: [Termux,Android]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
rm -rf \
/sdcard/Pictures/.gs \
/sdcard/Pictures/.gs_fs0 \
/sdcard/Pictures/.gs_fs3 \
/sdcard/Pictures/.gs_fs6 

touch \
/sdcard/Pictures/.gs \
/sdcard/Pictures/.gs_fs0 \
/sdcard/Pictures/.gs_fs3 \
/sdcard/Pictures/.gs_fs6 
```