---
title: 'Windows 卸载自带的UWP软件'
date: 2022-09-26 21:02:40
tags: [Windows,UWP]
published: true
hideInList: false
feature: 
isTop: false
---
Windows10自带了一些软件如`人脉` `闹钟和时钟` `获取帮助`等一些在国内网络环境下根本用不了的软件,虽然这些软件占用空间很小,但是放在那里看着也很难受,正常方法又卸不掉,只能使用powershell卸载
# step 1 打开powershell(管理员)
`win+x`后找到`Windows PowerShell(管理员)`打开
# step 2 输入你打算卸载APPX的PackageFullName
如`Remove-AppPackage Microsoft.WindowsAlarms_10.2009.5.0_x64__8wekyb3d8bbwe`
如果没有出现红字错误,就表示卸载成功
# step 3 如果出现了红字报错
比如我在卸载人脉的时候就遇到了报错`此应用是 Windows 的
一部分,无法针对每个用户卸载该应用.管理员可以尝试使用"启用或关闭 Windows 功能"从计算机中删除该应用.不过,该应用可能
无法被卸载.`
这时候就需要使用另一个命令` Get-AppxPackage *Microsoft.People* | Remove-AppPackage`来卸载了,注意`*Microsoft.People*`是你要卸载appx的`PackageName`而不是`PackageFullName`
# 已知的部分APPX信息

|DispalyName|Description|PackageName|PackageFullName
|:---:|:---:|:---:|:---:|
|Groove 音乐	|Groove 音乐	|Microsoft.ZuneMusic_10.20122.11121.0_x64__8wekyb3d8bbwe|	Microsoft.ZuneMusic_8wekyb3d8bbwe|
|Microsoft 人脉|Microsoft 人脉|	Microsoft.People_10.1909.12456.0_x64__8wekyb3d8bbwe|	Microsoft.People_8wekyb3d8bbwe|
|Microsoft 照片|Microsoft 照片|	Microsoft.Windows.Photos_2020.20110.11001.0_x64__8wekyb3d8bbwe|	Microsoft.Windows.Photos_8wekyb3d8bbwe|
|Windows 录音机|Windows 录音机|	Microsoft.WindowsSoundRecorder_10.2012.41.0_x64__8wekyb3d8bbwe|	Microsoft.WindowsSoundRecorder_8wekyb3d8bbwe|
|Windows 相机|Windows 相机|	Microsoft.WindowsCamera_2020.902.20.0_x64__8wekyb3d8bbwe|	Microsoft.WindowsCamera_8wekyb3d8bbwe|
|Windows 闹钟和时钟|Windows 闹钟和时钟|	Microsoft.WindowsAlarms_10.2009.5.0_x64__8wekyb3d8bbwe|	microsoft.windowsalarms_8wekyb3d8bbwe|
|Widget|win11的小工具| microsoftwindows.client.webexperience_421.20031.315.0_neutral_~_cw5n1h2txyewy<br> microsoftwindows.client.webexperience_421.20031.315.0_x64__cw5n1h2txyewy||


就不一一列举了,想查的人自然会查到