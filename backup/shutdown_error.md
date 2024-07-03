---
title: 'Linux关机服务卡死的解决办法'
date: 2022-12-05 21:23:53
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
教程适用于下列情况
- [ ]  若安装了桌面环境,关机时长时间卡在Ubuntu Logo屏,硬盘指示灯几乎没有动静
- [ ] 未安装桌面环境,关机时看见A stop job is running for...的日志输出
<!-- more -->
出现此问题是因为某些系统服务在关机时不能正常停止,导致系统无法达到关机时所需要的条件
最典型的就是Snap Daemon以及MariaDB,这两货就没好好停过.

对于桌面环境用户,当你关机时卡在Ubuntu Logo时,按下F1键,即可显示关机日志,然后同下无桌面环境的操作.

对于无桌面环境的用户,当你看见`A stop job is running for...`时,记下这个服务的名称

例如`A stop job is running for Snap Daemon`即`Snap Daemon`
然后根据你的常识与经验尝试猜测此服务的真实名称

例如Snap Daemon,可猜测真实名称为`snap-daemon` `snap` `snapd`
通过`sudo systemctl status {ServiceName}`来检测你的猜测是否准确.如果找到了此服务且显示名称相同,那就对了

例如猜测MariaDB Server为mysqld,验证时获得以下输出:
```shell
mariadb.service - MariaDB 10.1.44 database server
   Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
```
则猜测正确

如果经验不足或运气实在不好,可以尝试上网搜索有关信息

在验证猜测正确后,会获得指向该服务文件的路径.
如上面的`/lib/systemd/system/mariadb.service`使用root权限打开并编辑它
`sudo systemctl edit mariadb`

在文件末加一行`TimeoutStopSec=10`

意味着10秒后如果该服务还没有老老实实的去死,那systemd就会亲自动手强行弄死它

当然,你可以设置得更短,但是这可能会导致你手动关闭服务时也会超时然后服务被强行终止而无法保存数据

一般情况下,10秒已经够了,对于某些服务,可以根据实际情况设置超时

然后保存文件,退出

重载systemd`sudo systemctl daemon-reload`

然后重启查看情况.

可能会有多个服务阻止你关机,这时需要多查看几次日志把这些服务统统击毙

如果到最后所有阻止你关机的服务都击毙了还是没法关机,那可能就是什么其他的问题了

自己看着办吧


