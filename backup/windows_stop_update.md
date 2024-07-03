---
title: 'Windows暂停自动更新14年'
date: 2023-08-18 13:58:45
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
注册表文件如下
```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings]
"FlightSettingsMaxPauseDays"=dword:00001388
```
暂停更新不会影响紧急安全更新
虽然这个方法Windows 10也可以用,但是已经不建议了,因为Windows 10已经不会再有功能更新了,停止支持后普通级别的安全更新也没有了,唯一能收到的也只有可能是紧急安全更新了,用不用这个方法区别不大