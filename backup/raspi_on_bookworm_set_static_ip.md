---
title: '树莓派在 Bookworm上设置静态ip'
date: 2023-11-07 09:44:19
tags: [Raspberry]
published: true
hideInList: false
feature: 
isTop: false
---
```bash
sudo nano /etc/network/interfaces.d/eth0
# maybe ethX
```

```bash
allow-hotplug eth0
iface eth0 inet static
address 192.168.1.5
network 192.168.1.1
netmask 255.255.255.0
gateway 192.168.1.1
```

---------------------------------------------------

或者使用流行的`nmcli`命令

```bash
sudo nmcli -p connection show
```

返回应该类似

<center>NetworkManager connection profiles</center>

|NAME|UUID|TYPE|DEVICE|
|:---:|:---:|:---:|:---:|
|Wired connection 1|bd220d18-7d6a-36a5-9820-4f67de2c01fc|ethernet|eth0|
|mywifi|2359440b-8991-4c86-a905-b011dced4587|wifi|wlan0|
|lo|c29ba7c5-98ff-4fa0-8d8e-06b30b8ec384|loopback|lo|

假设修改以太网



```bash
sudo nmcli c mod "Wired connection 1" ipv4.addresses 192.168.1.5/24 ipv4.method manual
# multi ip address
sudo nmcli c mod "Wired connection 1" ipv4.addresses "192.168.1.5/24, 192.168.1.6/24, 10.0.0.222/24" ipv4.method manual

sudo nmcli con mod "Wired connection 1" ipv4.gateway 192.168.1.1

sudo nmcli con mod "Wired connection 1" ipv4.dns "8.8.8.8,8.8.4.4"

# reboot network
sudo nmcli c down "Wired connection 1" && sudo nmcli c up "Wired connection 1"
nmcli -p connection show "Wired connection 1"

# 恢复到自动分配
sudo nmcli con modify "Wired connection 1" ipv4.method auto
sudo nmcli c down "Wired connection 1" && sudo nmcli c up "Wired connection 1"
```