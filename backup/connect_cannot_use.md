---
title: '已连接到网络,不可用的解决方法'
date: 2022-09-26 17:21:40
tags: [Windows]
published: true
hideInList: false
feature: 
isTop: false
---
此方法适用于Win7/8/8.1/10/11连接网络后提示`已连接,无Internet`的情况,有可能在不同的系统上提示不同,但大致都是没有网的意思

<!-- more -->

# 产生原因

微软用来验证网络连通性的方法是:连接到一个自家的网站,判断是否能返回正确信息

一旦这个特定的网络连接不上

即使你能连接到别的网络

也算是没有网

本来大家相安无事

GFW一定要搞点事

这个网站被墙了

受灾最严重的就是中国移动的用户

这里有张图

你们自己品

![世界触手可及](https://s1.ax1x.com/2022/09/04/vofoRO.jpg)

# 解决方法

+ [ ] 把这个地址替换成可以连接的另一个地址
+ [x] 关闭这个不能用的功能

### 把这个地址替换成可以连接的另一个地址

```Registry
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NlaSvc\Parameters\Internet]
"ActiveDnsProbeContent"="223.5.5.5"
"ActiveDnsProbeContentV6"="2400:3200::1"
"ActiveDnsProbeHost"="dns.alidns.com"
"ActiveDnsProbeHostV6"="dns.alidns.com"
"ActiveWebProbeContent"="Microsoft NCSI"
"ActiveWebProbeContentV6"="Microsoft NCSI"
"ActiveWebProbeHost"="www.alidns.com"
"ActiveWebProbeHostV6"="www.alidns.com"
"ActiveWebProbePath"="ncsi.txt"
"ActiveWebProbePathV6"="ncsi.txt"
"CaptivePortalTimer"=dword:00000000
"CaptivePortalTimerBackOffIncrementsInSeconds"=dword:00000005
"CaptivePortalTimerMaxInSeconds"=dword:0000001e
"EnableActiveProbing"=dword:00000001
"PassivePollPeriod"=dword:0000000f
"StaleThreshold"=dword:0000001e
"WebTimeout"=dword:00000023
```

### 关闭这个不能用的功能

```Registry
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NlaSvc\Parameters\Internet]
"EnableActiveProbing"=dword:00000000
```

# 尾声

当然,做这一切之前先改一下DNS