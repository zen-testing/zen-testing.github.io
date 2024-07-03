---
title: '设置windows时间开机同步方法'
date: 2022-09-26 17:43:15
tags: [Windows,NTP]
published: true
hideInList: false
feature: 
isTop: false
---

最近在花粉俱乐部看见几个宣称自己电脑时间总是不准的人,虽然是初始号,无等级,无发帖历史,隐藏手机型号很可疑,但还是说一下遇到这种问题的普适解决方法吧

<!-- more -->

windows的时间同步windows默认是7天,同步默认是通过微软的授时服务器,但是移动宽带用户和狗连不上这个网站,所以第一步的解决方法就是换一个时间同步服务器(NTP)或者换成其他的ISP

NTP可以选择
[阿里云](ntp.aliyun.com)
[Apple](http://time1.apple.com)
[Google](http://time1.google.com)
[中科院授时中心](ntp.ntsc.ac.cn)
[中国授时](cn.ntp.org.cn)
七天同步一次还是太慢,通过修改注册表实现调整:

1. 定位到`[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient]`
2. 双击`SpecialPollInterval`键值,值改为你想要的同步频率
3. 定位到`[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters]`
4. 双击`NtpServer`键值,值改为你想要的NTP服务器


或者直接导入这个注册表文件

```regedit
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient]
"SpecialPollInterval"=dword:00000060

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Parameters]
"NtpServer"="ntp.aliyun.com"
```