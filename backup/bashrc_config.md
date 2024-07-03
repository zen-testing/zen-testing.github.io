---
title: '个人电脑配置文件记录'
date: 2022-09-26 15:34:52
tags: [macOS,knowledge]
published: true
hideInList: false
feature: 
isTop: false
---

# `.gitconfig`

```shell
[user]
      email = zhangyiming748@gmail.com
      name = zen
[http]
      proxy = http://127.0.0.1:8889
[https]
       proxy = http://127.0.0.1:8889
[core]
        editor = sublime -n -w
        compression = 0
[filter "lfs"]
    process = git-lfs filter-process
    required = true
    clean = git-lfs clean -- %f
    smudge = git-lfs smudge -- %f

```

# `.bash_profile`

```shell
# set alias
alias umount='diskutil unmount'
alias fmtgo='find /Users/zen -name "*.go" -exec gofmt -w {} \;'
alias ds='find . -name ".DS_Store" -print'
alias 4k='find . -type f -name ".*" -size -10k -print'
alias rmds='find . -name ".DS_Store" -exec rm {} \;'
alias rm4k='find . -type f -name ".*" -size -10k -exec rm -f {} \;'
alias tarxz="XZ_OPT='-9ek --threads=10' tar -Jcvf"
alias ll="ls -l"
alias ytd="youtube-dl --proxy 127.0.0.1:8889"
alias la="ls -al"
alias golinux="CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build"
# alias gowindows="CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build"
alias gowin32="CGO_ENABLED=1 GOOS=windows GOARCH=386 go build"
alias gowin64="CGO_ENABLED=1 GOOS=windows GOARCH=amd64 go build"
alias goraspi="CGO_ENABLED=0 GOOS=linux GOARCH=arm go build"
alias pi="ssh pi@192.168.1.5"
alias euler="ssh root@192.168.1.15"
alias openwrt='ssh root@192.168.1.2'
alias kodi='ssh root@192.168.1.6'
# alias goarm="CGO_ENABLED=0 GOOS=linux GOARCH=arm go build"
alias proxy='export all_proxy=http://127.0.0.1:8889'
alias unproxy='unset all_proxy'
alias isproxy='curl cip.cc'
alias curl='curl -C -'
alias ydl='youtube-dl --proxy 127.0.0.1:8889 -f best'
#alias targz='tar zcvf'
#alias untargz='tar zxvf'
alias bz2='tar -jcvf'
alias unbz2='tar -jxvf'
alias startmysql='mysql.server start'
alias stopmysql='mysql.server stop'
alias startredis='/usr/local/opt/redis@4.0/bin/redis-server /usr/local/etc/redis.conf'
# alias allproxy="export all_proxy=http://127.0.0.1:8889"
export PATH=$PATH:/Users/zen/Documents/phantomjs/bin
```

# `.vimrc`

```shell
set number
set ts=4
set noexpandtab
```

# `.ssh/config`

```shell
# 必须是 github.com
Host github.com
HostName github.com
User git

ProxyCommand nc -v -x 127.0.0.1:1089 %h %p
```
