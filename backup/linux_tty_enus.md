---
title: 'Linux系统设置tty为英文,图形界面不变'
date: 2022-09-26 17:25:59
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
tty中默认只能显示一个字节

<!-- more -->

添加以下内容到用户变量`~/bashrc`或`~/bash_profile`中,如果你希望对所有用户都生效,也可以添加到`/etc/profile`中

通常情况下,linux系统前六个tty是纯命令行界面

```shell
if [ "$(tty)" = "/dev/tty1" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
# 当然也可以把六个都变成英文输出
if [ "$(tty)" = "/dev/tty2" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
if [ "$(tty)" = "/dev/tty3" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
if [ "$(tty)" = "/dev/tty4" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
if [ "$(tty)" = "/dev/tty5" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
if [ "$(tty)" = "/dev/tty6" ]; then
	export LC_ALL="en_US.UTF-8"
	export LANGUAGE="en_US.UTF-8"
	export LANG="en_US.UTF-8"
fi
```
# 扩展阅读

如果需要让ssh连接显示中文,可以作如下设置
```shell
if [ -z "$SSH_TTY" ]; then
	export LC_PAPER=en_US.UTF-8
	export LC_ADDRESS=en_US.UTF-8
	export LC_MONETARY=en_US.UTF-8
	export LC_NUMERIC=en_US.UTF-8
	export LC_TELEPHONE=en_US.UTF-8
	export LC_IDENTIFICATION=en_US.UTF-8
	export LANG=en_US.UTF-8
	export LC_MEASUREMENT=en_US.UTF-8
	export LANGUAGE=en_US:en
	export LC_TIME=en_US.UTF-8
	export LC_NAME=en_US.UTF-8
else
	export LC_PAPER=zh_CN.UTF-8
	export LC_ADDRESS=zh_CN.UTF-8
	export LC_MONETARY=zh_CN.UTF-8
	export LC_NUMERIC=zh_CN.UTF-8
	export LC_TELEPHONE=zh_CN.UTF-8
	export LC_IDENTIFICATION=zh_CN.UTF-8
	export LANG=zh_CN.UTF-8
	export LC_MEASUREMENT=zh_CN.UTF-8
	export LANGUAGE=zh_CN:zh
	export LC_TIME=zh_CN.UTF-8
	export LC_NAME=zh_CN.UTF-8
fi
```