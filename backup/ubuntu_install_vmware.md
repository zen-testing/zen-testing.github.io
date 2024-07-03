---
title: 'Ubuntu22.04安装VMware16[解决各种安装问题]'
date: 2022-09-26 19:24:54
tags: [Linux,Ubuntu]
published: true
hideInList: false
feature: 
isTop: false
---
# 0x01 下载[安装包](https://www.vmware.com/cn/products/workstation-pro/workstation-pro-evaluation.html )

# 0x02 安装gcc

```shell
$ sudo apt-get install gcc
```

# 0x03 安装make

```shell
$ sudo apt-get install make
```

# 0x04 安装lib

```shell
$ sudo apt-get install libaio1 libglib2.0-dev
```

# 0x05 安装git

```shell
$ sudo apt-get install git
```

# 0x06 安装kernel modules

```shell
$ git clone https://github.com/mkubecek/vmware-host-modules.git
```

# 0x07 切换分支

首先确定你下载的VM的版本,因为不同的版本安装的内容不同,确定版本之后,切换到自己版本的分支中进行编译!

我的版本是16.2.3,所以我先切换到我自己版本对应的分支中

```shell
$ git checkout workstation-16.2.3
```

# 0x08 编译vmware-host-modules

```shell
$ make
```

# 0x09 安装vmware-host-modules

```shell
$ sudo make install
```

# 0x0A 配置所有模块

```shell
$ sudo su -
vmware-modconfig --console --install-all
```

# 0x0B 安装VMware

```shell
$ sudo ./VMware-Workstation-你下载的安装包名称
```

# 0x0C 运行VM
