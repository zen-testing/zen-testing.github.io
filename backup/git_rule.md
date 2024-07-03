---
title: '代码提交管理流程'
date: 2022-09-26 16:00:04
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---

# 代码分支

**master(长期分支)** :主分支,仅包含最终的产品代码,禁止直接提交改动到 `master` 分支上.

**dev(长期分支)**:开发分支,基于`master`分支,用于汇总已完成新功能的基础分支.

**feature(短期分支)**:功能分支,基于`dev`分支,开发新功能的主要分支,主要合并到`dev`分支(合并之前先解决可能的冲突).

**release(短期分支)**:测试分支,基于合并完功能分支后的`dev`分支,用于测试,最终需要合到 `master` 分支和 `dev`分支.

**hotfix(短期分支)**:补丁分支,基于主分支,需要合到`master` 分支和`dev`分支.

# 命名规范

|分支|命名|说明|
|:---:|:---:|:---:|
|主分支|master|主分支,所有提供给用户使用的正式版本,都在这个主分支上发布|
|开发主分支|dev|开发分支,永远是功能最新最全的分支|
|功能分支|feature-*| 新功能分支,某个功能点正在开发阶段|
|发布版本|release-*| 发布定期要上线的功能|
|修复发布版本分支|hotfix-release-*|修复测试 bug|
|紧急修复分支|hotfix-master-*|紧急修复线上代码的 bug|


# git 常用命令(参考)

* 拉取远程分支并切换到该分支

```
git checkout -b 本地分支名 origin/远程分支名
git checkout --track origin/远程分支名 (这种写法是上面的简化版,效果完全一样)
git checkout -t origin/远程分支名(这种写法是上面两种的简化版)
```

* 修正提交
```
git commit --amend // 将暂存区中的文件提交(先可以将需要提交的文件进行add)
```
* 关联远程分支并推送
```
git push --set-upstream origin feature/xxx
```
* 将指定的提交(commit)应用于其他分支
```
git cherry-pick commit-id
```
* 删除分支
```
git branch -D 本地分支名 // 删除本地分支
git push origin --delete 远程分支名 // (慎用)删除远程分支
```
* 暂存和恢复
```
git stash list // 列出暂存的列表
git stash save "备注信息" // 执行暂存并添加备注
git stash pop // 恢复暂存的工作目录,并将缓存堆栈中的对应stash删除,将对应修改应用到当前的工作目录下,默认为第一个stash,即stash@{0},如果要应用并删除其他stash,命令:git stash pop stash@{$num} ,比如应用并删除第二个:git stash pop stash@{1}
git stash show // 显示做了哪些改动,默认show第一个存储,如果要显示其他存贮,后面加stash@{$num},比如第二个 git stash show stash@{1}
git stash show -p // 显示第一个存储的改动,如果想显示其他存存储,命令:git stash show stash@{$num} -p ,比如第二个:git stash show stash@{1} -p
git stash apply // 应用某个存储,但不会把存储从存储列表中删除,默认使用第一个存储,即stash@{0},如果要使用其他个,git stash apply stash@{$num} , 比如第二个:git stash apply stash@{1}
git stash drop stash@{$num} // 丢弃stash@{$num}存储,并从列表中删除这个存储
git stash clear // 删除所有缓存的stash
```
