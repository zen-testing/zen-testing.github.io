---
title: 'Git clone 一个巨大的代码库'
date: 2022-09-26 16:39:32
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
git config --global core.compression 0 //关闭压缩
git clone --depth 1 <repo_URI> //只克隆第一层代码
git fetch --unshallow //克隆其他部分 或者
git fetch --depth=2147483647 //二选一的命令
git pull --all //拉取代吗
```