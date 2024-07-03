---
title: 'UWP设置代理'
date: 2022-09-26 18:57:12
tags: [Proxy]
published: true
hideInList: false
feature: https://s1.ax1x.com/2022/09/04/vofoRO.jpg
isTop: false
---

Win 10 的 UWP应用(应用商店下载的APP,如OneDrive和我的世界基岩版等),默认是不走代理的(沙盒的网络隔离特性:禁止APP访问localhost ),即使使用了「小飞机」软件,UWP软件仍然无法得到加速.
网上有很多解决此类问题的方法,要不就是使用 Fiddler 软件进行设置,要不就是使用`CheckNetIsolation`命令来解除限制,但是需要通过注册表来获取应用的SID,都比较麻烦.
其实有一个办法,不需要下载软件,也不需要打开注册表.
# 解除限制的方法
先获取需要走代理的APP的「程序包名称」.然后使用`CheckNetIsolation`命令解除该APP的 网络隔离.
第一步:获取名称
按Win+R,在打开(O)后面输入:
`C:\Users\%username%\AppData\Local\Packages`
打开后能看到的每一个文件夹就代表一个UWP程序包,文件夹的名称就是程序包的名称.
例如:`Microsoft.Office.OneNote_8wekyb3d8bbwe`

### 解除限制
解除限制使用的是CheckNetIsolation命令.该命令的语法是:
```
CheckNetIsolation LoopbackExempt [operation] [-n=] [-p=]
      操作列表:
          -a  -  向环回免除列表中添加 AppContainer 或程序包系列.
          -d  -  从环回免除列表中删除 AppContainer 或程序包系列.
          -c  -  清除环回免除的 AppContainer 和程序包系列的列表.
          -s  -  显示环回免除的 AppContainer 和程序包系列的列表.

      参数列表:
          -n= - AppContainer 名称或程序包系列名称.
          -p= - AppContainer 或程序包系列安全标识符(SID).
          -?  - 显示 LoopbackExempt 模块的此帮助消息.
```
以OneNote为例,在命令行里输入:
`CheckNetIsolation.exe LoopbackExempt -a -n="Microsoft.Office.OneNote_8wekyb3d8bbwe"``
命令执行后,系统会提示完成,该UWP软件无法访问localhost的限制已经解除
### 设置全局代理
在Proxifier软件里配置全局代理.
先在菜单栏的Profile / Proxy Servers 里设置你的代理地址.
然后在Profile / Proxification Rules 里面进行配置,把你需要代理的软件配置一个规则.
或者也可以直接把 Default 配置为走代理,然后在代理软件里通过PAC功能或者路由规则来配置走代理和直连.