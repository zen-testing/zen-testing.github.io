---
title: '解决windows预览体验计划页面空白问题'
date: 2022-09-26 19:08:21
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
右键以管理员身份运行powershell

在powershell中分别执行如下四个命令

```
$path = "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection"
# Telemetry level: 1 - basic, 3 - full
$value = "3"
New-ItemProperty -Path $path -Name AllowTelemetry -Value $value -Type Dword -Force
New-ItemProperty -Path $path -Name MaxTelemetryAllowed -Value $value -Type Dword -Force
```

执行完重启电脑,重新查看windows预览体验计划