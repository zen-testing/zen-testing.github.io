---
title: 'Linux中监控(cp\mv\dd\tar等)命令进度的小工具'
date: 2022-09-26 17:25:16
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# Progress 命令参数

|参数|英文解释|中文翻译|
|:---:|:---:|:---:|
|-q<br>--quiet|hides all messages|隐藏所有信息|
|-d<br>--debug|shows all warning/error messages|显示所有信息|
|-w<br>--wait|estimate I/O throughput and ETA (slower display)|估计完成时间|
|-W<br>--wait-delay secs|wait 'secs' seconds for I/O estimation (implies -w, default=1.0)|等待x秒后估计时间|
|-m<br>--monitor|loop while monitored processes are still running|在受监视的进程仍在运行时循环|
|-M<br>--monitor-continuously|like monitor but never stop (similar to watch progress)|像监视器但从不停止(类似于监视进度)|
|-a<br>--additional-command cmd|add additional command to default command list|将附加命令添加到默认命令列表|
|-c<br>--command cmd|monitor only this command name (ex: firefox)|仅监视此命令名称(例如:firefox)|
|-p<br>--pid id|monitor only this process ID (ex: `pidof firefox`)|仅监视此进程 ID(例如:`pidof firefox`)|
|-i<br>--ignore-file file|do not report process if using file|使用文件时不报告进程|
|-o<br>--open-mode {r\|w}|report only files opened for read or write|仅报告为读取或写入而打开的文件|
|-v<br>--version|show program version and exit|显示程序版本并退出|
|-h<br>--help|display this help and exit|显示程序帮助并退出|
