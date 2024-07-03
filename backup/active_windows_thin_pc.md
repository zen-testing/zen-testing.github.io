---
title: '证书方式激活 Windows Thin PC'
date: 2022-09-26 15:06:27
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
1. 确保三个文件放在`c:\`
![文件图](https://s1.ax1x.com/2022/09/05/vTcza6.png)
2. 使用管理员身份运行cmd
3. 输入命令`slmgr.vbs /ilc c:\pkeyconfig-embedded.xrm-ms`出现对话框后点`OK`
4. 输入命令`slmgr.vbs /ilc c:\Security-SPP-Component-SKU-Embedded-VLBA-ul.xrm-ms`出现对话框后点`OK`
5. 输入命令`slmgr.vbs /ilc c:\Security-SPP-Component-SKU-Embedded-VLBA-ul-oob.xrm-ms`出现对话框后点`OK`
6. 输入命令`slmgr.vbs /ipk XGY72-BRBBT-FF8MH-2GG8H-W7KCW`出现对话框后点`OK`
7. 输入命令`slmgr.vbs /xpr`出现对话框后点`OK`激活成功

----
打完收工