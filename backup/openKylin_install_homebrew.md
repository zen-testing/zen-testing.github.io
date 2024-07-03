---
title: '开放麒麟1.0安装homebrew'
date: 2023-08-18 13:56:36
tags: [openKylin]
published: true
hideInList: false
feature: 
isTop: false
---
# 安装一个能用的curl版本

```bash
# 在普通用户下运行
apt install -y curl git
git config --global http.sslVerify false
```

# 准备好环境变量

```bash
# 在root用户下运行
echo -e 'export # Set PATH, MANPATH, etc., for Homebrew.\nHOMEBREW_API_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles/api"\nexport HOMEBREW_BOTTLE_DOMAIN="https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles"\nexport HOMEBREW_BREW_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git"\nexport HOMEBREW_CORE_GIT_REMOTE="https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git"\nexport HOMEBREW_PIP_INDEX_URL="https://pypi.tuna.tsinghua.edu.cn/simple"\nexport HOMEBREW_NO_AUTO_UPDATE=true\nexport HOMEBREW_NO_INSTALL_CLEANUP=true\nexport HOMEBREW_INSTALL_FROM_API=true\n' >> /etc/profile
source /etc/profile
```

# 安装安装工具

```bash
# 在普通用户下运行
source /etc/profile
cd ~
git clone --depth=1 https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/install.git brew-install
/bin/bash brew-install/install.sh
rm -rf brew-install
```

# 设置环境变量

```bash
# 在root用户下运行
(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /etc/profile
apt install -y build-essential
```

# 安装新版curl

```bash
# 在普通用户下运行
brew install curl
sudo apt remove curl
# 验证curl版本
curl --version
```

# 设置brew使用新版curl

```bash
# 在root用户下运行
echo 'export HOMEBREW_CURL_PATH=/home/linuxbrew/.linuxbrew/bin/curl' >> /etc/profile
```

# 演示效果

可以通过`brew`安装新版`bash`
```bash
brew install bash
# 打开一个新的终端
bash --version
```
![bash](https://s1.ax1x.com/2023/07/07/pCci3Gt.png)