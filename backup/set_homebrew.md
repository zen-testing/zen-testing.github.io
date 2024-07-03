---
title: '重装系统后需要通过homebrew安装的软件'
date: 2022-10-19 15:59:44
tags: [macOS,HomeBrew]
published: true
hideInList: false
feature: 
isTop: false
---
# 安装

```shell
$ xcode-select --install

$ git clone --depth=1 https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/install.git brew-install
$ /bin/bash brew-install/install.sh
rm -rf brew-install

$ test -r ~/.bash_profile && echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.bash_profile
$ test -r ~/.zprofile && echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```
# .bash_profile

```shell
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"
```

# 软件

```shell
brew install shadowsocksx
brew install shadowsocksx-ng
brew install shadowsocksx-ng-r
brew install android-platform-tools
brew install qlvideo
brew install vlc
brew install aria2
brew install bash
brew install scrcpy
brew install shfmt
brew install sl
brew install cweb
brew install ffmpeg
brew install media-info
brew install tree
brew install neofetch
brew install unzip
brew install nushell
brew install webp
brew install wget
brew install p7zip
brew install xz
brew install progress
```