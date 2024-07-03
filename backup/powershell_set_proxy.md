---
title: 'Powershell设置代理'
date: 2023-11-07 11:01:25
tags: [Proxy,Windows]
published: true
hideInList: false
feature: 
isTop: false
---
on

```powershell
adb shell settings put global http_proxy 192.168.xx.xxx:8080
```
off


```powershell
adb shell settings put global http_proxy :0
```
