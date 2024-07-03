---
title: '用Golang安装新版本Golang'
date: 2022-09-26 19:40:47
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---
```shell
$ go install golang.org/dl/go1.19@latest
$ $GOPATH/bin/go1.19 download
$ echo "PATH=/Users/zen/sdk/go1.19/bin:$PATH" >> ~/.bash_profile
```