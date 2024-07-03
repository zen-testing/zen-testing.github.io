---
title: 'macOS升级新版本Bash'
date: 2022-09-26 17:35:43
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
许多macOS用户不知道的一件事是,他们正在使用完全过时的 Bash shell 版本.所以,强烈建议在macOS上使用较新版本的 Bash,因为它有很多可用的新功能

<!-- more -->

macOS上的默认Bash版本
要查看 macOS 中包含的 Bash 版本的是否已经过时,请执行以下命令:

```shell
$ bash --version
//返回值类似如下
GNU bash,版本 3.2.57(1)-release (x86_64-apple-darwin19.0.0)
Copyright (C) 2007 Free Software Foundation, Inc.
许可证 GPLv3+: GNU GPL 许可证第三版或者更新版本
<http://gnu.org/licenses/gpl.html>
本软件是自由软件,你可以自由地更改和重新发布.
在法律许可的情况下特此明示,本软件不提供任何担保.
```

如你所见,这是`GNU Bash 3.2`版,其日期为2007年,此版本的Bash包括在所有macOS版本中,甚至是最新版.
苹果在其操作系统中包含如此旧版本的Bash的原因与许可有关

从4.0版本(3.2的后继版本)开始,Bash使用GNU通用公共许可证v3(GPLv3),Apple不(想)支持.
GNU Bash 的 3.2 版是 Apple 接受的带有`GPLv2`的最新版本,因此坚持使用这个版本.
这意味着整个世界(例如Linux)都将使用 Bash 的新版本,而macOS用户则只能使用十年前的旧版本.

# 如何升级

要将macOS系统的默认Shell升级到最新版本的Bash,你必须做三件事:

	1. 安装最新版本的Bash
	2. 将新的`Bash Whitelist`作为`login shell`
	3. 将新的Bash设置为`default shell`

每个步骤都非常容易,如下所述.

**注意:**以下说明不会更改Bash的旧版本,而是安装新版本并将其设置为默认版本.这两个版本将在你的系统上并存,但是你可以从此处忽略旧版本.

# 安装

我建议使用Homebrew安装最新版本的Bash:

brew安装bash

```shell
brew install bash
```
要验证安装,你可以检查系统上现在有两个版本的Bash

```shell
$ which -a bash
/opt/homebrew/bin/bash
/bin/bash
```

# 添加到 "受信任" Shell 程序列表中

`sudo vim /etc/shells`

并将 /usr/local/bin/bash Shell 添加到其内容中,以便文件看起来像这样:

```shell
/opt/homebrew/bin/bash
/bin/bash
/bin/csh
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```

# 设置默认 Shell

`chsh -s /opt/homebrew/bin/bash`

该 chsh 命令仅为执行命令的用户(当前用户)更改默认 Shell 程序.如果你也想更改其他用户的默认 Shell ,则可以通过登录其他用户的身份来重复此命令
也许你可能想要更改 root 用户的默认 Shell 程序,你可以执行以下操作
```shell
$ sudo chsh -s /opt/homebrew/bin/bash
```