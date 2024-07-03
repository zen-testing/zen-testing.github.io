---
title: '修复homebrew安装软件404问题'
date: 2022-11-02 23:13:33
tags: [HomeBrew]
published: true
hideInList: false
feature: 
isTop: false
---
# 问题现象

```shell
curl: (22) The requested URL returned error: 404
Warning: Bottle missing, falling back to the default domain...
```

# 产生原因

**bintray关闭了**
应该是截止到某个时间点
之后的包就没再往bintray传了
也就是404了
其实Homebrew社区对这个问题早就做了准备的
新版的homebrew程序已经去除了bintray相关
使用ghcr.io服务了
所以只要正常使用
正常先update
再upgrade
是可以完美过渡
用户是无感的

至于我遇到了问题
是因为我用了清华大学的镜像
目前清华大学的镜像中依然是指向到bintray的
所以也跟着404了

# 解决问题

那就是去掉清华大学的镜像设置就好了
具体的环境变量是
`$HOMEBREW_BOTTLE_DOMAIN`
使用
```shell
export HOMEBREW_BOTTLE_DOMAIN=''
```
命令就可以去除
可以使用`brew config`命令验证


修改完后，再进行安装，就一切正常了。

我后来又去清华大学的GitHub上看了
已经有人反馈这个问题了
同时发现`https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles/` 目录下并没有直接列出各种包
反而多了一个bottles目录
想必清华大学已经是在处理这个问题
开始同步了吧
只是这个镜像有2.5T大
要完全同步完
真不知道猴年马月了