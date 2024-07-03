---
title: 'arp欺骗'
date: 2022-09-26 15:28:06
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---
# 命令

```shell
$ arpspoof -i <网卡名> -t <目标ip> <网关ip>
如 我要攻击树莓派:
$ arpspoof -i eth0 -t 192.168.1.5 192.168.1.1
```

# 获取局域网内其他ip

```shell
$ namp <局域网段>
如:
$ nmap 192.168.1.5-11
```