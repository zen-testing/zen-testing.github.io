---
title: 'openKylin安装homebrew从而安装更多软件'
date: 2022-11-04 17:29:52
tags: [openKylin,HomeBrew]
published: true
hideInList: false
feature: 
isTop: false
---
>由于众所周知的原因,openKylin安装了ubuntu的部分基础软件后删除了密钥环,导致无法再安装其他的基础软件,除了补全ubuntu密钥环,还可以通过brew帮助你安装软件

<!-- more -->

# 安装基础软件

```shell
$ sudo apt-get install git curl build-essential
```

# 配置git

```shell
$ git config --global http.sslverify false
$ git config --global core.compression 0
$ git config --global http.postBuffer 1048576000
```

# 设置环境变量

```shell
# 使用homebrew官方源无需做以下设置
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles" # 可以不用设置这条 历史遗留问题
```

应用`source ~/.bashrc`

# 安装主程序

```shell
$ git clone --depth=1 https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/install.git brew-install
$ /bin/bash brew-install/install.sh
$ rm -rf brew-install
# 如果你的网络条件很好 也可以使用如下命令
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

# 设置环境变量

```shell
# 使用homebrew官方源无需做以下设置
$ test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
$ test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
$ test -r ~/.bash_profile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bash_profile
$ test -r ~/.profile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.profile
$ test -r ~/.zprofile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.zprofile
```

# 按照提示执行命令

```shell
$ echo '# Set PATH, MANPATH, etc., for Homebrew.' >> /home/zen/.bashrc
$ echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/zen/.bashrc
$ eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
```

# Debug

如果使用中出现了如下错误
```shell
fatal: Could not resolve HEAD to a revision
```

执行

```shell
$ brew doctor
```

按照推荐的方法解决问题即可

# 测试

安装一个在软件仓库中不存在的软件

```shell
$ sudo apt-get install neofetch
# 会报错没有这个软件
# 正在读取软件包列表... 完成
# 正在分析软件包的依赖关系树       
# 正在读取状态信息... 完成       
# E: 无法定位软件包 neofetch
```

使用brew install命令

```shell
$ brew install neofetch
```

会自动补全依赖

```shell
Running `brew update --auto-update`...
==> Downloading https://ghcr.io/v2/homebrew/core/linux-headers/5.15/manifests/5.15.57-1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/linux-headers/5.15/blobs/sha256:8692682830cbb1fb74bb61190b644da9de0f4c3a40cf1
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:8692682830cbb1fb74bb61190b644da9de0f4c3a4
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/glibc/manifests/2.35_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/glibc/blobs/sha256:274dd06ae6ecaee3025d6bf21cf4c7641df9a1cc3973e162911a1f4a76
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:274dd06ae6ecaee3025d6bf21cf4c7641df9a1cc3
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gmp/manifests/6.2.1_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gmp/blobs/sha256:786ae29f0c0b06ea86e42bd9c6ac2c49bd5757da037dead7053e8bd612c4
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:786ae29f0c0b06ea86e42bd9c6ac2c49bd5757da0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/isl/manifests/0.25
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/isl/blobs/sha256:c0244c95ed9cc89b826868de83bec3150fcc120add126501717677015075
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:c0244c95ed9cc89b826868de83bec3150fcc120ad
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/mpfr/manifests/4.1.0-p13
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/mpfr/blobs/sha256:345a3d99db0f4149f84f0aa16c0ee9c4275f695e4fa0f6d2ae1e8054a0d
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:345a3d99db0f4149f84f0aa16c0ee9c4275f695e4
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/libmpc/manifests/1.2.1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/libmpc/blobs/sha256:d74eb5f1377d8fa72fad88baca1bd5f00c29d45ba186fbec89ad690c1
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:d74eb5f1377d8fa72fad88baca1bd5f00c29d45ba
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/lz4/manifests/1.9.4
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/lz4/blobs/sha256:1757fefc3840e11c4822e4c2a95aa62aca44a4eaccce6f5c414ea51d1e58
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:1757fefc3840e11c4822e4c2a95aa62aca44a4eac
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/xz/manifests/5.2.7
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/xz/blobs/sha256:dda25f66145c180884d0550a36d68491abd648011b9ac91566773961a1d92
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:dda25f66145c180884d0550a36d68491abd648011
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/zlib/manifests/1.2.13
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/zlib/blobs/sha256:0082aa29a61507e237389ee4e9fb6a6ed0cbd5d341e3905527c089c88e7
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:0082aa29a61507e237389ee4e9fb6a6ed0cbd5d34
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/zstd/manifests/1.5.2-3
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/zstd/blobs/sha256:006b5ab6a4616a8b6f59953cb9efb546d312e3ba231c303bb56749e7f66
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:006b5ab6a4616a8b6f59953cb9efb546d312e3ba2
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/binutils/manifests/2.39_1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/binutils/blobs/sha256:efa7497e2ea56d9b68ce41363cdc1a41cad032b3ae2fa2cbe819459
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:efa7497e2ea56d9b68ce41363cdc1a41cad032b3a
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gcc/manifests/12.2.0-1
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gcc/blobs/sha256:c7f773f9af560766b2d971d815a8d224c267088c05ed1f2b864bd1d9ebc2
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:c7f773f9af560766b2d971d815a8d224c267088c0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/neofetch/manifests/7.1.0-2
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/neofetch/blobs/sha256:78eb3e99dfde7f5fb1c3b192804a6d345f428c9effa6ea6ba54d7e5
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:78eb3e99dfde7f5fb1c3b192804a6d345f428c9ef
######################################################################## 100.0%
==> Installing dependencies for neofetch: linux-headers@5.15, glibc, gmp, isl, mpfr, libmpc, lz4, xz, zlib, zstd, binutils and gcc
==> Installing neofetch dependency: linux-headers@5.15
==> Pouring linux-headers@5.15--5.15.57.x86_64_linux.bottle.1.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/linux-headers@5.15/5.15.57: 963 files, 5.7MB
==> Installing neofetch dependency: glibc
==> Pouring glibc--2.35_1.x86_64_linux.bottle.tar.gz
==> /home/linuxbrew/.linuxbrew/Cellar/glibc/2.35_1/sbin/ldconfig
==> Installing locale data for en_US.UTF-8
==> /home/linuxbrew/.linuxbrew/Cellar/glibc/2.35_1/bin/localedef -i en_US -f UTF-8 en_US.UTF-8
🍺  /home/linuxbrew/.linuxbrew/Cellar/glibc/2.35_1: 1,404 files, 47MB
==> Installing neofetch dependency: gmp
==> Pouring gmp--6.2.1_1.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/gmp/6.2.1_1: 23 files, 3.9MB
==> Installing neofetch dependency: isl
==> Pouring isl--0.25.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/isl/0.25: 74 files, 9.2MB
==> Installing neofetch dependency: mpfr
==> Pouring mpfr--4.1.0-p13.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/mpfr/4.1.0-p13: 31 files, 6.0MB
==> Installing neofetch dependency: libmpc
==> Pouring libmpc--1.2.1.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/libmpc/1.2.1: 13 files, 550.2KB
==> Installing neofetch dependency: lz4
==> Pouring lz4--1.9.4.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/lz4/1.9.4: 22 files, 695.6KB
==> Installing neofetch dependency: xz
==> Pouring xz--5.2.7.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/xz/5.2.7: 151 files, 2.5MB
==> Installing neofetch dependency: zlib
==> Pouring zlib--1.2.13.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/zlib/1.2.13: 13 files, 471.8KB
==> Installing neofetch dependency: zstd
==> Pouring zstd--1.5.2.x86_64_linux.bottle.3.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/zstd/1.5.2: 31 files, 2.6MB
==> Installing neofetch dependency: binutils
==> Pouring binutils--2.39_1.x86_64_linux.bottle.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/binutils/2.39_1: 4,687 files, 370.5MB
==> Installing neofetch dependency: gcc
==> Pouring gcc--12.2.0.x86_64_linux.bottle.1.tar.gz
==> Creating the GCC specs file: /home/linuxbrew/.linuxbrew/Cellar/gcc/12.2.0/bin/../lib/gcc/current/gcc/x86_64-pc-linux-gnu/1
🍺  /home/linuxbrew/.linuxbrew/Cellar/gcc/12.2.0: 1,633 files, 306.4MB
==> Installing neofetch
==> Pouring neofetch--7.1.0.all.bottle.2.tar.gz
🍺  /home/linuxbrew/.linuxbrew/Cellar/neofetch/7.1.0: 6 files, 375KB
==> Running `brew cleanup neofetch`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```
软件的可执行文件通常在

```shell
/home/linuxbrew/.linuxbrew/bin/neofetch
```

# 效果图

![效果图](https://s1.ax1x.com/2022/11/04/xLWZlD.png)
