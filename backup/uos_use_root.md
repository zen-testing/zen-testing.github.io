---
title: '不提交个人信息不让用root?naive'
date: 2022-09-26 16:33:52
tags: [UOS]
published: true
hideInList: false
feature: 
isTop: false
---

可能是我用过的linux发行版太少了,同为Debian衍生的翘楚Ubuntu,稳坐公司服务器系统第一把交椅的Redhat都不敢禁root用户,锁sudo,没见过这种操作,用开源系统还强制登录账号,微信一注册一半个人敏感信息就上交了,再打开开发者选项需要注册个人开发者,另一半个人敏感信息又上交了,没有红帽的命得了红帽的病,谁给你们的勇气

<iframe width="560" height="315" src="https://www.youtube.com/embed/vUPH_5qyBwQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# 为暴躁老哥准备的文字版
1. ~~开机按e进入任意一个启动项的grub编辑界面~~
2. ~~如果有类似`ro`字样改成`rw single`~~
3. ~~如果有类似`xx=xx`字样改成`init=/bin/bash`,如果没有就自己添加~~
4. ~~`Ctrl+x`保存退出自动重启进入单用户模式~~
>使用liveCD挂载本地系统分区

5. 启用root用户并设置密码
6. 分别编辑`/etc/pam.d/sudo`和`/etc/pam.d/su`
7. 注释掉第一行 `auth		requisite	deepin_security_verify.so`
8. 输入`visudo`编辑允许sudo列表
9. 按照格式添加自己

```
# User privilege specification
root	ALL=(ALL:ALL) ALL
${USER}	ALL=(ALL:ALL) ALL
```
----
可以断电重启了

重启后删除`/usr/bin/uos-activator`和`/usr/bin/uos-activator-cmd`
