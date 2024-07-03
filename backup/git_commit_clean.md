---
title: 'Git只保留最后一次提交信息'
date: 2022-09-26 16:43:08
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---
应付代码洁癖领导专用

<!-- more -->

在本地github仓库中删除某一次commit 提交信息/历史/记录

>如何同步到远程github仓库(使其不显示该commit的信息)
之所以记这个,因为我在百度上没有看到合适的解决方案,所以感觉有必要在这里记录一下.

假定现在的情况是:有10个commit,然后git log查看commit信息

```shell
commit-A 10月
commit-B 9月
commit-C 8月
commit-D 7月
......
commit-n 1月

```

我现在想删除commit-C这个提交,但同时不影响commit-A,B,D等等其他commits

运行

```shell
git rebase -i HEAD~5
或者
git rebase -i <comit-D-id>
注意:这里得选择提交时间在commit-C之前的!所以我在此选择了commit-D的id
```

此时会进入到一个文件中,里面有

```
pick comit-id xxx
pick comit-id xxx
```

找到commit-C的id对应的那一行pick,pick改成f或s就行,然后保存文件,退出即可

运行`git log`,此时发现commit 历史中已经没有commit-C啦

运行`git push -f origin master`即可同步到远程github仓库

# 备份
如果怕把本地git仓库搞坏了,可以先复制一下这个仓库,作为备份,免得追悔莫及.
