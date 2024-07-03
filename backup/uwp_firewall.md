---
title: '流氓软件关闭防火墙导致win10uwp无法使用的临时解决办法'
date: 2022-09-26 18:34:21
tags: [Windows,knowledge]
published: true
hideInList: false
feature: 
isTop: false
---

>The MPSSVC service host much more functionality than just windows firewall. For instance, Windows Service hardening which is a windows protection of system services. It also host network isolation which is a crucial part of the confidence model for Windows Store based applications. 3 party firewalls know this fact and instead of disabling the firewall service they coordinate through public APIs with Windows Firewall so that they can have ownership of the firewall policies of the computer.  Hence you do not have to do anything special once you install a 3 party security product

这里面讲到MPSSVC的作用不仅仅是一个防火墙,而且微软应用商店的应用安装依赖也得靠他,第三方安全软件一般都不会对这个服务动手,而是选择应用与其相关的API来执行安全服务

----

简单来说,Windows10之后的防火墙不再是字面意义上的防火墙了.而是和Windows defender紧密团结在一起协同作战的整体安全解决方案.

Windows10之前(version 1803前)以360为首的流氓软件安装在电脑上的第一件事就是彻底关闭Windows defender的自我保护功能,但是在uac开启的情况下这一操作必须要询问用户是否同意,为了防止一小部分用户直接选择否,他们禁止了更为底层的防火墙服务,在1083前这么做不会被轻易察觉到,因为以来防火墙的只有少数几个功能性应用并且大部分人本身就用不到,这样一来,直接绕过用户控制禁用了底层防火墙,在用户毫无察觉的情况下替换了全部Windows的安全工具

形象比喻就是`为了防止你跑步摔倒摔坏腿,直接把你截肢了`

----

而1803这个节点之后,Windows defender 功能变得更强大 不再是单纯的杀毒+防火墙.然而uwp应用是依赖于防火墙的部分功能的.

360为了抢占用户电脑的杀毒软件头把交椅禁用底层服务

可感知的问题就是UWP再也打不开了

不知算不算作茧自缚

----
解决方法分为两种

1. 电脑上避免安装360或类似的流氓软件,他们能给你的问题永远比他们能解决的问题多.有人会问`那我卸载不就好了吗?`不,你不能,能卸载的叫恶意软件
2. 在安全卫士里的优化加速里的启动项里,把`windows firewall`和`defender`等相关服务打开,亦即恢复启动,重启之后,思考一下你是否真的需要这些给你帮倒忙的软件