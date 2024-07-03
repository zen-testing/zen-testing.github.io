---
title: 'macOS取消开盖自动开机和音效'
date: 2022-09-26 17:27:10
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---

取消自动开机:

`sudo nvram AutoBoot=%00`

重新启用自动开机:

`sudo nvram AutoBoot=%03`

开启开机音效:

`sudo nvram BootAudio=%01`

取消开机音效:

`sudo nvram BootAudio=%00`
