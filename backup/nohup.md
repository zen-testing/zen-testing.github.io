---
title: 'nohup用法'
date: 2022-09-26 18:05:25
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
有时候需要在Linux上设置一个后台进程,但是当你关闭terminal之时,它会被系统kill掉,那该如何来实现其后台进程能一直运行下去呢?

<!-- more -->

```shell
nohup command-with-options &
# 比如
nohup ./main &
```

当在屏幕上敲击上述命令之后,屏幕上会出现如下信息
```shell
nohup: ignoring input and appending output to `nohup.out’
```
敲击回车,就退出了nohup.out当前的界面,进入正常的命令行

# nohup和&的区别

注意nohup没有后台运行功能,就是指,用nohup运行命令可以使命令永久的执行下去,和用户终端没有关系,例如我们断开SSH连接都不会影响他的运行,&才是后台运行,但当用户退出(挂起)的时候,命令自动也跟着退出

那么,我们可以巧妙的吧他们结合起来用就是
```
nohup COMMAND &
```
这样就能使命令永久的在后台执行