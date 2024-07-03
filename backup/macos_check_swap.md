---
title: 'macOS查看硬盘信息'
date: 2022-09-26 17:28:19
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---

>2020 年 11 月份,苹果发布了几款搭载自研 M1 芯片的新 Mac 产品,引燃了整个硬件圈.随后的各方评测也显示,这款芯片的性能确实令人惊艳,CPU 单线程\多线程性能都很优秀,GPU 足以称霸集显,甚至可以媲美独显
>但令人没想到的是,让全网高呼真香的 M1 最近也暴露出了自己的缺陷:对固态硬盘寿命非常不友好.
从上周开始,社交网络中就有一些苹果用户在使用工具查看 SSD 硬盘状态的时候发现了SSD写入总量异常
一些高级用户表示,他们发现 M1 在读写数据时会过度使用 Mac 电脑的 SSD,这一问题可能会影响到 M1 版 Mac 中搭载的 SSD 的寿命,进而影响整个机器的寿命.
一些推特用户发帖说,macOS 的健康报告显示,M1 Mac 的 SSD「在非常短的时间内经历了极高的硬盘写操作」.甚至有用户指出,他刚用了 60 天的 M1 Mac 已经消耗了 SSD 10% 的最大可保证 TBW 可写入字节(数据写入总量寿命).
>由于 SSD 是基于芯片而不是机械部件,因此有预定的寿命,寿命长短取决于他们读写了多少数据.你往 SSD 中写入的数据越多,它就会越早暴露出问题,如速度变慢或数据损坏.由于 M1 版 Mac 的内部存储器是焊接在逻辑板上的,因此一旦 SSD 寿终正寝,用户可能就要更换整台电脑.
如果只是常规使用,SSD 的寿命可以达到十年,但最近的这些报告显示,由于 macOS 的异常行为,M1 版 Mac 的内部 SSD 寿命可能会缩短到 2 年.一位 M1 MacBook Pro(2TB+16GB)的用户表示,ta 刚用了两个月的 MacBook Pro 也已经消耗了 3% 的 SSD 寿命.在低端 Mac 产品中,这一问题将更加突出.

----

**那么问题来了**

<b>如何查看自己的 SSD 使用情况?</b>

首先,我们要安装一个叫做`smartmontools`的工具.它并不是一个独立的 App,我们需要打开苹果的`Terminal`,输入 `/usr/local/sbin/smartctl -a /dev/disk0` (如果你不接外部硬盘的话,磁盘号一定是`disk0`)

如果觉得这个命令太长,可以软连接到`/usr/local/bin`

按下回车后,我们就可以看到如下资料

```
smartctl 7.2 2020-12-30 r5155 [Darwin 19.6.0 x86_64] (sf-7.2-1)
Copyright (C) 2002-20, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Model Number:                       APPLE SSD AP0256M //型号
Serial Number:                      C02920505FKM3DW1H 序列号
Firmware Version:                   1161.80. //固件版本
PCI Vendor/Subsystem ID:            0x106b  //PCI厂商ID/子(次要)系統(裝置)識別碼
IEEE OUI Identifier:                0x000000
Controller ID:                      0
NVMe Version:                       <1.2
Number of Namespaces:               1
Local Time is:                      Mon Mar  8 20:44:36 2021 CST
Firmware Updates (0x02):            1 Slot
Optional Admin Commands (0x0004):   Frmw_DL
Optional NVM Commands (0x0004):     DS_Mngmt
Maximum Data Transfer Size:         256 Pages

Supported Power States
St Op     Max   Active     Idle   RL RT WL WT  Ent_Lat  Ex_Lat
 0 +     0.00W       -        -    0  0  0  0        0       0

=== START OF SMART DATA SECTION ===
SMART overall-health self-assessment test result: PASSED

SMART/Health Information (NVMe Log 0x02)
Critical Warning:                   0x00 //严重警告,该字段表示控制器状态的严重警告,Raw值是0的话就没事
Temperature:                        28 Celsius //温度
Available Spare:                    100% //可用备用空间,是可用剩余容量的百分比
Available Spare Threshold:          99% //可用备用空间,是可用剩余容量的百分比
Percentage Used:                    2% //使用百分比,设备使用寿命百分比的估算,具体取决于实际设备使用情况和厂商对设备寿命的预测
Data Units Read:                    39,117,943 [20.0 TB] //数据单位读取,该项记录的是主机从SSD里读取512字节数据单元的数量,每1000个单元记录一次,即这项Raw数据1的值等于500KB
Data Units Written:                 31,211,154 [15.9 TB] //数据单位写入,同上,把上面那段的读取换成写入即可
Host Read Commands:                 713,244,048 //主机读取命令,主控收到的读取命令数量.
Host Write Commands:                584,466,686 //主机写入命令,主控收到的写入命令数量
Controller Busy Time:               0 //控制器繁忙时间,主控忙于I/O命令的时间
Power Cycles:                       181 //电源循环,SSD的通电次数
Power On Hours:                     548 //开机时间,记录开机的小时数
Unsafe Shutdowns:                   69 //不安全关机,非正常断电次数记录
Media and Data Integrity Errors:    0 //媒体和资料完整性错误,主控检测得到的未恢复的数据完整性错误次数
Error Information Log Entries:      0 //错误资料记录项目数,主控总共收到的错误信息日志数量.

Read 1 entries from Error Information Log failed: GetLogPage failed: system=0x38, sub=0x0, code=745
```
