---
title: 'Git删除所有历史提交记录,只留下最新的干净代码'
date: 2022-09-26 16:38:29
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---

1. Checkout

```shell
$ git checkout --orphan latest_branch  // 基于当前分支创建新分支
```

2. Add all the files

```shell
$ git add -A // 追踪全部文件
```

3. Commit the changes

```shell
$ git commit -am "commit message" // 添加提交信息
```

4. Delete the branch

```shell
$ git branch -D master // 删除主分支
```

5. Rename the current branch to master

```shell
$ git branch -m master // 命名当前分支为主分支
```

6. Finally, force update your repository

```shell
$ git push -f --set-upstream origin master // 强制推送并设置与远程分支的对应关系
```
