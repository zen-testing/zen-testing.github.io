---
title: '以UOS家庭版为例升级最新内核'
date: 2024-03-01 21:57:27
tags: [UOS,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# 0x01 开启源码仓库
为了可以使用 `apt build-dep linux`命令 自动安装编译所需的依赖,需要先为 apt 配置源码仓库
编辑` /etc/apt/sources.list`,有些发行版(如Ubuntu)默认将 deb-src 开头的源码仓库注释掉了,只需要取消注释就可以了
而UOS没有,所以UOS要编译就得添加

```bash
echo "deb-src [https://home-packages.chinauos.com/home](https://home-packages.chinauos.com/home) plum main contrib non-free" >> /etc/apt/sources.list
```
# 0x02 安装需要的依赖
编辑` /etc/apt/sources.list `后执行`apt build-dep linux git zstd`

# 0x03 下载内核源码

```bash
wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.7.6.tar.xz
```

# 0x04 解压文件
```bash
tar -xf linux-6.3.1.tar.xz
```
# 0x05 进入解压目录
```bash
cd linux-6.7.6/
```
# 0x06 复制内核配置文件
```bash
cp /boot/config-"$(uname -r)" .config
```
# 0x07 编译deb
```bash
make menuconfig
make deb-pkg -j4(根据自己CPU线程数修改)
```
如果提示缺少git仓库,在编译内核目录输入以下命令
```bash
git init
git add .
git commit -m "1"
```
# 0x08 删除无关文件
我们只需要 linux-headers 和 linux-image 开头的两个 deb 文件h名字中带有 dbg,是调试内核用的

# 0x09 安装
```bash
mv *.deb /tmp
sudo apt install -f /tmp/*.deb
```
0x0A 完结