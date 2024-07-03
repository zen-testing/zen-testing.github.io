---
title: '恢复Win10系统更新失败'
date: 2022-09-26 16:27:04
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
适用于安装更新后直接无法进入系统和RE环境的状况

<!-- more -->

+ 用U盘启动后,进入恢复环境后,先选择"修复计算机",之后逐级进入"疑难解答-高级选项",找到"命令提示符",OK,开始吧!
![](https://z3.ax1x.com/2021/07/20/WYNEFS.jpg)
+ 打开"命令提示符"后,会提示让大家输入密码,输入当前Windows 10登录账号的密码(不是PIN码,是账号密码).
![高级选项](https://z3.ax1x.com/2021/07/20/WYNko8.jpg)
+ 在命令提示符中输入"bcdedit"(不含引号,下同),找到名为"resumeobject"的选项,记录下后面的一长串字符(即GUID)
![bcdedit](https://z3.ax1x.com/2021/07/20/WYNVJg.jpg)
+ 接着输入"bcdedit /set {GUID} recoveryenabled No"后回车运行,目的是禁用Windows的自启修复功能,其中{GUID}就是上面resumeobjec选项显得的一长串字符,可以直接复制,每台电脑GUID都不一样
+ 最后只要再输入"sfc /scannow"开始系统文件扫描\验证并修复就行了,这个过程稍微有点长,把电脑丢在一边做点别的吧!
![scannow](https://z3.ax1x.com/2021/07/20/WYNFdf.jpg)
+ 全部完成后,重启电脑再用Windows Update打个补丁试试,肯定完美的!
![reinstall](https://z3.ax1x.com/2021/07/20/WYNZWQ.jpg)
