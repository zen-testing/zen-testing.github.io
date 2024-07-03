---
title: 'Windows Update 暂停更新'
date: 2023-07-08 21:46:29
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
# 视频效果

<iframe width="672" height="378" src="https://www.youtube.com/embed/i9CpmGxTHXg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

如果视频无法观看,点击[这里](https://www.bilibili.com/video/BV1Bz4y1E7g3/?share_source=copy_web&vd_source=1401ae656a2e38ecf1a20f98d4249473)
# 注册表文件
```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings]
"FlightSettingsMaxPauseDays"=dword:00001388
```
暂停更新不会影响紧急安全更新
虽然这个方法Windows 10也可以用,但是已经不建议了,因为Windows 10已经不会再有功能更新了,停止支持后普通级别的安全更新也没有了,唯一能收到的也只有可能是紧急安全更新了,用不用这个方法区别不大