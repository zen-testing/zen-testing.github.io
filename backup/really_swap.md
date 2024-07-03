---
title: '交换分区是否有必要，应该给多大空间'
date: 2023-05-24 20:48:50
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
经常有小白在网上找了一些关于swap分区"应该"多大的教程,其实对于写这些教程的人来说,这可能是人家当时确实根据机器的状态和业务需求得出的结论,而看这些教程的人却经常因为自己坚信的那一份教程在各大社区争论得面红耳赤甚至恶语相向
对此,最好的方法还是根据自己的实际情况来决定交换空间应该多大,是否需要这个东西;先建立一个交换文件,用几天之后看看,是否真正用到了这个功能

监控Linux交换文件主要有以下几种方式:
1. 使用free\vmstat等命令监视Swap字段
2. 使用swapon或cat /proc/swaps命令查看交换文件详细使用量 
3. 监控/var/log/messages日志,了解系统交换事件

----

1. `free`命令

`free`命令可以显示内存和交换文件使用情况.

```bash
free -h
              total        used        free      shared  buff/cache   available
Mem:            29G        2.1G         22G         32M         4.7G         27G
Swap:          8.0G          0B         8.0G
# Swap行显示交换文件总量与使用量,我们可以监视Swap: used的值.
```

2. `vmstat`命令

`vmstat`命令的`swpd`列显示交换文件中使用的内存页面数量.

```bash 
vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 22156860 860268 758744    0    0     8    60   12   19  3  1 96  0  0 
 0  0      0 22157060 860300 758624    0    0     0   496 2382 6673  5  1 94  0  0
# 可以每隔几秒运行vmstat 1查到交换文件的使用量.
```

3. `swapon`命令 

`swapon`命令列出当前激活的交换文件与使用量.

```bash
swapon 
NAME            TYPE        SIZE USED PRIO
/dev/sda5                               partition    8388608   0   -2
我们可以看到/dev/sda5交换分区的使用量(USED列).
```

4. `cat /proc/swaps`

`/proc/swaps`文件包含系统中所有的交换文件信息.

```bash
cat /proc/swaps
Filename                Type        Size    Used    Priority
/dev/sda5                               partition    8388608    0    -2
# 同样可以查看各交换文件的使用量.
```

5. 监控`/var/log/messages`

`/var/log/messages`日志文件中记录了系统的交换事件.我们可以通过监控这个日志来了解系统的交换频度和使用量.
例如:
```bash
Jan 10 12:34:56 localhost kernel: [103371.173586] swapper/2: page allocation failure: order:0, mode:0x20
Jan 10 12:34:56 localhost kernel: [103371.173603] swapper/2: warning: swap rather than OOM kill
这表示由于内存不足,进行了交换操作.
```

所以,通过上述几种方式,我们可以清楚地掌握系统的交换文件使用情况和交换频度,你应该根据自己的需求决定,而不是看一个看起来正确的教程,可能对于现在的年轻人来说32G硬盘空间不算什么,但是对于我这个老人来说,当年我电脑硬盘一共才40G啊