---
title: '环境变量备份'
date: 2024-03-01 22:14:17
tags: [macOS,Windows,Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# ~/.gitconfig
```bash
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

# ~/.bash_profile

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
alias la="ls -al"
alias proxy='export all_proxy=http://127.0.0.1:8889'
alias unproxy='unset all_proxy'
alias isproxy='curl cip.cc'
alias curl='curl -C'
alias yt-dlp='yt-dlp --no-playlist --proxy 192.168.1.5:8889'
export PATH=$PATH:/Users/zen/Documents/phantomjs/bin
# 慎重
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi
```

# ~/.vimrc

```shell
set number
set ts=4
set noexpandtab
```

# ~/.ssh/config

```shell
# 必须是 github.com
Host github.com
HostName github.com
User git

ProxyCommand nc -v -x 127.0.0.1:1089 %h %p
```