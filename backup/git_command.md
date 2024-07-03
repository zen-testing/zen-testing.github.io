---
title: 'Git相关知识'
date: 2022-09-26 16:40:49
tags: [Git]
published: true
hideInList: false
feature: 
isTop: false
---
## Tag
tag可以单独提交,提交后push即可被其他人看到,无需更行origin/HEAD
## 全局设置

用 Git 提交必须先声明自己的身份,可用如下指令设置:

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

# 生成公钥
`ssh-keygen -t rsa -C "zhangyiming748@gmail.com"`

# 设置默认的编辑器

`vim .gitconfig`

```
# [user]
#       email = zhangyiming748@gmail.com
#       name = zen
# [http]
#       proxy = http://172.29.128.1:8889
# [https]
#       proxy = http://172.29.128.1:8889
[core]
        editor = sublime -n -w
```

# 安装git

[OSX](http://git-scm.com/download/mac)

[Windows](http://git-for-windows.github.io/)

[Linux](http://book.git-scm.com/2_installing_git.html)

# 创建新仓库
创建新文件夹,打开,然后执行

`git init`

以创建新的 git 仓库

# 检出仓库
执行如下命令以创建一个本地仓库的克隆版本:

`git clone /path/to/repository`

如果是远端服务器上的仓库,你的命令会是这个样子:

`git clone username@host:/path/to/repository`

# 工作流

你的本地仓库由 git 维护的三棵"树"组成:

第一个是你的 工作目录,它持有实际文件;第二个是 暂存区(Index),它像个缓存区域,临时保存你的改动;最后是 HEAD,它指向你最后一次提交的结果

添加和提交
你可以提出更改(把它们添加到暂存区),使用如下命令:

`git add <filename>`
`git add *`

这是 git 基本工作流程的第一步;使用如下命令以实际提交改动:

`git commit -m "代码提交信息"`

现在,你的改动已经提交到了`HEAD`,但是还没到你的远端仓库

# 推送改动

你的改动现在已经在本地仓库的`HEAD`中了执行如下命令以将这些改动提交到远端仓库:
`git push origin master`

可以把`master`换成你想要推送的任何分支

如果你还没有克隆现有仓库,并欲将你的仓库连接到某个远程服务器,你可以使用如下命令添加:
`git remote add origin <server>`

如此你就能够将你的改动推送到所添加的服务器上去了

# 分支


# 更新与合并
要更新你的本地仓库至最新改动,执行:

`git pull`

以在你的工作目录中获取(fetch)并合并(merge)远端的改动

要合并其他分支到你的当前分支(例如 master),执行:

`git merge <branch>`
 在这两种情况下,git都会尝试去自动合并改动,遗憾的是,这可能并非每次都成功,并可能出现冲突`conflicts` 这时候就需要你修改这些文件来手动合并这些冲突`conflicts`改完之后,你需要执行如下命令以将它们标记为合并成功:

`git add <filename>`

在合并改动之前,你可以使用如下命令预览差异:

`git diff <source_branch> <target_branch> `

# 标签
为软件发布创建标签是推荐的这个概念早已存在,在 SVN 中也有你可以执行如下命令创建一个叫做 1.0.0 的标签:
`git tag 1.0.0 1b2e1d63ff`
`1b2e1d63ff`是你想要标记的提交ID的前10位字符可以使用下列命令获取提交ID:
`git log`

你也可以使用少一点的提交ID前几位,只要它的指向具有唯一性

# log

如果你想了解本地仓库的历史记录,最简单的命令就是使用:

`git log`

你可以添加一些参数来修改他的输出,从而得到自己想要的结果

只看某一个人的提交记录:

`git log --author=bob`

一个压缩后的每一条提交记录只占一行的输出:

`git log --pretty=oneline`

或者你想通过 ASCII 艺术的树形结构来展示所有的分支, 每个分支都标示了他的名字和标签:

`git log --graph --oneline --decorate --all`

看看哪些文件改变了:

`git log --name-status`

这些只是你可以使用的参数中很小的一部分

更多的信息,参考:

`git log --help`

# 替换本地改动

假如你操作失误(当然,这最好永远不要发生),你可以使用如下命令替换掉本地改动:

`git checkout -- <filename>`

此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件已添加到暂存区的改动以及新文件都不会受到影响

假如你想丢弃你在本地的所有改动与提交,可以到服务器上获取最新的版本历史,并将你本地主分支指向它:

`git fetch origin`

`git reset --hard origin/master`

#实用小贴士

内建的图形化 git:

`gitk`

彩色的 git 输出:

`git config color.ui true`

显示历史记录时,每个提交的信息只显示一行:

`git config format.pretty oneline
`
交互式添加文件到暂存区:

`git add -i`

----


# 常用命令介绍
## 命令行介绍
### Git 全局设置
```
$ git config --global user.name "Zen"
$ git config --global user.email "zhangyiming748@gmail.com"
```

### 创建一个新仓库(本地)
```
$ git clone git@github.com:zhangyiming748/zhangyiming748.github.io.git
cd git-exmple
$ touch README.md
$ git add README.md
$ git commit -m "add README"
$ git push -u origin master
```

### 在已存在的目录中创建仓库
```
cd existing_folder
$ git init
$ git remote add origin github.com:zhangyiming748/zhangyiming748.github.io.git
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```

### 将本地已存在的仓库推送到远程仓库
```
cd existing_repo
$ git remote rename origin old-origin
$ git remote add origin github.com:zhangyiming748/zhangyiming748.github.io.git
$ git push -u origin --all
$ git push -u origin --tags
```

### 查看分支相关命令
```
$ git branch -r//查看远程分支
$ git branch //查看本地分支
$ git branch -a //查看所有分支
```

### 拉取远程分支并创建本地分支
```
// dev2为远程分支,dev1为本地分支
$ git checkout -b dev1 origin/dev2;
//从远程分支dev拉取到本地并且创建本地分支dev,且俩者之间建立映射关系,同时当前分支会切换到dev1

//dev2为远程分支,dev1为本地分支
$ git fetch origin dev2:dev1;
//使用该方式会在本地新建分支dev1,但是不会自动切换到该本地分支dev1,需要手动checkout.采用此种方法建立的本地分支不会和远程分支建立映射关系.
```

### 切换当前本地分支
```
// dev为本地分支名
$ git checkout dev
```

### 拉取远程分支代码
```
$ git pull
//使用的前提是当前分支需要与远程分支之间建立映射关系
```

### 推送本地分支代码到远程分支
```
$ git push
//使用的前提是当前分支需要与远程分支之间建立映射关系
```

### 合并分支

//场景:现在有dev本地分支与远程分支,master本地分支与远程分支 现在将dev的分支代码合并到master主干上
//思路步骤:
1. 有本地修改进行commit并且push到远程dev分支上,保证没有遗漏的,确保当前本地dev与远程dev是一致的
3. 将当前本地分支切换到本地master上
4. 将本地分支dev合并到本地master上
5. 将本地已经合并了dev分支的master进行push到远程master上 大概思路就是这样.需要注意的是在进行merge(合并)的时候需要禁用fast-forward模式

`git merge --no-ff dev` (dev为本地被合并的分支名字)

# Git 版本回退

对于版本的回退,我们经常会用到两个命令:
`$ git reset`
`$ git revert`

## git reset
`$ git reset --hard a0fvf8`

如果直接使用git push命令的话,将无法将更改推到远程仓库.此时,只能使用-f 选项将提交强制推到远程仓库:
`$ git push -f`


## git revert
git revert的作用通过反做创建一个新的版本,这个版本的内容与我们要回退到的目标版本一样,但是HEAD指针是指向这个新生成的版本,而不是目标版本.

`$ git revert 5lk4er`
`$ git revert 76sdeb`


## 分支命名规范
### 主分支:
master:master 分支就叫 master 分支
develop:develop 分支就叫 develop 分支
### 辅助分支:
#### Feature 分支
`feature/v1.16.0_xxx`,
`feature/v1.16.0_yyy`,
`feature/v1.16.0_zzz`
`v1.16.0` 表示当前迭代的版本号,
`xxx/yyy/zzz` 表示当前迭代的功能或业务单元的名称
#### Release 分支
`release/v1.17.0`,
`release/v1.18.0`
`v1.17.0`,`v1.18.0` 根据上线需求和系统上线计划,合理规划版本号,每个大版本号表示一次上线正常上线过程.
#### Hotfix 分支
`hotfix/v1.17.1`,
`hotfix/v1.17.2`
`v1.17.1`,`v1.17.2` 表示v1.17.0 这个版本做了2次线上问题热修复.
# 总结
+ 并行开发:依据迭代的发版计划和任务分解,创建feature(不同迭代需通过版本号隔离,同一个迭代内要上线的功能需要通过feature隔离)
+ 保持迭代内代码的可预见性&可控制性: 迭代内,只允许主迭代的feature代码提交到develop分支
+ 哪里有问题改哪里,改完后及时合并到主分支: release(fit)环境的问题修复:应从release分支拉出分支进行问题修复,修复后及时合并到develop主分支 master环境的问题修复:应从生产环境对应的tag(一般为最新的版本号)拉出分支进行问题修复,问题修复后及时合并代码至develop主分支和master主分支
