---
title: 'MagicbookPro安装Linux系统的8822C驱动'
date: 2022-09-26 17:38:37
tags: [Linux,华为]
published: true
hideInList: false
feature: 
isTop: false
---

# 下载驱动包备用
```
git clone https://github.com/zhangyiming748/rtl88x2Driver.git $HOME/workplace
cd $HOME/workplace
```

![图片后补]()

# 解压安装包

```
tar -zxvf rtl8822.tar.gz
```

![图片后补]()

# 进入解压后的目录

```
cd rtl88x2CE_WiFi_linux_v5.7.3_34277.20190709_COEX20190531-0e0e/
```

![图片后补]()

# 修改makefile文件

```
vi Makefile
```

其中

```
export TopDIR ?= $(shell pwd)
```

改为

```
export TopDIR ?= 你的当前目录
```

比如

```
export TopDIR ?= /home/deepin/rtl88x2CE_WiFi_linux_v5.7.3_34277.20190709_COEX20190531-0e0e
```

wq保存修改退出

# 进行编译安装载入

```
make
sudo make install
sudo modprobe -a 8822ce
```

# 重启电脑

```
reboot
```