---
title: '解决Linux+Windows双系统时间不同步的问题'
date: 2022-09-26 19:03:56
tags: [双系统]
published: true
hideInList: false
feature: 
isTop: false
---

>Ubuntu和Windows双系统,开发娱乐两不误,随用随切换,岂不美哉?
然而,在美的背后,存在一个让人抓狂的Bug:从一个系统切换到另一个系统后,时间就会出错,表现为—— 时差8小时.
>>例如
Ubuntu中时间正常,但是切换回Windows后,后者的时间慢8个小时.
Windows中时间正常,但是切换回Ubuntu后,后者的时间快8个小时.
一个系统中时间错乱,尚可通过互联网时间同步(NTP服务器)来解决.但是切换到另一个系统后,时差问题照样如故.

时间不同步的问题,已经是双系统使用上的一个经典问题了,很多前辈都给出了解决办法,例如设置开机服务主动同步ntp时间

# 方法1 在Linux中的设置

需要注意的是,Ubuntu会自动设置时区和时间,此时如果不进行后续的设置,机器时间就会被改写.本地时间(Local Time)就是我们在系统中使用的时间,它的值虽然正确,但这是以UTC为参照的,与机器时间存在8小时的时差.一旦重启进入仍然将机器时间视为RTC的Windows,则必会导致时间不统一.

自Ubuntu16.04版本起`timedatectl`成为Ubuntu的时间管理工具.不带参数运行时,它会输出当前的时间,以及系统时间的一些配置参数.

以下为设置前的timedatectl输出,本地时间为实际时间,注意观察时差

```shell
                      Local time: Fri 2018-09-07 22:32:18 CST
                  Universal time: Fri 2018-09-07 14:32:18 UTC
                        RTC time: Fri 2018-09-07 14:32:18
                       Time zone: Asia/Shanghai (CST, +0800)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: no
```

具体的操作如下

```shell
# 更改硬件时间标准,将硬件时间由UTC改为CST
$ sudo timedatectl set-local-rtc 1
$ reboot
# 找到你所使用发行版的时间和日期设置,选择自动配置时间和日期
# 同步硬件时间到机器时间
$ sudo hwclock --localtime --systohc
```

# 方法2 在Windows中设置

具体的操作如下

```shell
# 管理员权限打开powershell输入
$ reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
# 原理就是:在注册表项HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation中添加一个名为RealTimeIsUniversal的值,类型为REG_DWORD,数据为1
# 此项的作用就是让Windows将硬件时间当作UTC,与Ubuntu的默认设置一致
# 重启系统后即可生效
```