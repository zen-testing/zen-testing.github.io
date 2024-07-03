---
title: '查看一个已经运行的容器run启动命令'
date: 2024-03-10 13:14:30
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
sudo apt install python3 python3-pip
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
pip install runlike --break-system-packages
echo 'PATH=$PATH:/home/zen/.local/bin' >> /home/zen/.bash_profile
runlike <container name>
```