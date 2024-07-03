---
title: 'Windows Thin PC安装功能包'
date: 2022-09-26 20:48:41
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
Windows Thin PC 是一个官方精简版的Windows7系统,只安装了最必要的功能,并且没有给用户提供GUI的选择功能界面,所以需要自己手动用dism命令添加功能
1. 下载Windows thin pc的.net framework文件
2. 在系统盘(一般为C盘)创建文件夹,命名为FeaturePack
3. 复制所需的功能扩展包文件到文件夹 C:\FeaturePack
4. 以管理员权限打开命令提示符窗口并运行以下命令:

```
Dism.exe /Online /Add-Package /PackagePath:C:\FeaturePack /NoRestart
```
个人经验:在安装 .net 3.0 和 3.5 时,要与 2.0 一起安装..net 2.0 文件 为 winemb-netfx20.cab 和 winemb-netfx20client.cab

安装其他功能也是把功能包放在C:\FeaturePack下,同样执行
```
Dism.exe /Online /Add-Package /PackagePath:C:\FeaturePack /NoRestart
```
以下是一些常用WINDOWS功能相关组件的具体信息:
1. Windows Media Player 高级解码
winemb-premiumcodecs-dolby-ac3-audioencoder.cab
WinEmb-PremiumCodecs-MPEG2andDolbyDecoder.cab
WinEmb-PremiumCodecs-MPEG2-Decoder.cab
winemb-premiumcodecs-mpeg2-encoder.cab
WinEmb-PremiumCodecs-MPEG3.cab
WinEmb-PremiumCodecs-MPEG4.cab
winemb-premiumcodecs-wmv.cab
2. Windows搜索
winemb-natural-language.cab
winemb-search.cab
3. .NET Framework 3.5
winemb-iis-was.cab
winemb-netfx30.cab
winemb-netfx30client.cab
winemb-netfx35 .cab
winemb-netfx35client.cab
4. Windows DVD Maker :
winemb-dvdburning.cab
winemb-imapiv2.cab
5. Windows ISO Burner
winemb-imapiv2.cab
6. Windows 媒体中心:
winemb-mediacenter.cab
7. Windows 照片查看器:
winemb-photos-viewer.cab
8. Windows Defender:
winemb-antimalware.cab