---
title: 'windows合并多个系统安装镜像'
date: 2023-08-18 13:12:00
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
```cmd
Dism.exe /Export-Image /SourceImageFile:C:\Users\zen\Documents\windows\Windows1122H2专业版.wim /SourceIndex:1 /DestinationImageFile:C:\Users\zen\Documents\multi.wim
Dism.exe /Export-Image /SourceImageFile:C:\Users\zen\Documents\windows\Windows1022H2专业版.wim /SourceIndex:1 /DestinationImageFile:C:\Users\zen\Documents\multi.wim
Dism.exe /Export-Image /SourceImageFile:C:\Users\zen\Documents\windows\Windows10LTSC.wim /SourceIndex:1 /DestinationImageFile:C:\Users\zen\Documents\multi.wim
```