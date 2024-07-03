---
title: '单用户模式下终端乱码解决'
date: 2022-09-26 19:19:36
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

# 终端显示英文提示,桌面环境显示中文

```shell
$ sudo vim /etc/profile

if [ "$TERM"="linux" ] ;then
  export LANG="en_US.UTF-8"
  export LC_ALL="en_US.UTF-8"
  export LANGUAGE="en_US.UTF-8"
  export LANG="en_US.UTF-8"
fi
```

或者

```shell

sudo vim .bashrc
#
if [ -z "$DISPLAY" ]; then
        export LANG="en_US.UTF-8"
        export LC_ALL="en_US.UTF-8"
        export LANGUAGE="en_US.UTF-8"
        export LANG="en_US.UTF-8"
fi
#
```