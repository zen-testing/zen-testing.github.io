---
title: 'virtualbox各种网络模式的区别'
date: 2023-05-24 20:39:49
tags: [VirtualBox]
published: true
hideInList: false
feature: 
isTop: false
---
# virtualbox可选的网络模式有七种

## 无网络 `Not attached`

`Not attached` 模式类似于没插网线,所以网络是断的,没法连接主机和外网,但ip地址什么的是有的.

## 网络地址转换`Network Address Translation (NAT)`

`NAT `模式下可以访问主机和外网,但主机\外网及其他虚拟机都不能直接访问该虚拟机,这也是virtualbox的默认网络模式.

## NAT网络`NAT Network`

`NAT Network` 模式和 NAT 类似,唯一的区别是在该模式下,虚拟机之间可以相互访问.

## 网桥`Bridged networking`

`Bridged networking` 模式下,虚拟机类似于内网的一台其他机器,所以它可以访问内网中的其他机器以及外网,内网中的其他机器也可以直接访问它,在该模式下,虚拟机之间也是可以访问的.该模式可以说是virtualbox网络功能最全的模式,如果嫌配置网络麻烦,直接用这个模式就好了.

## 内部网络`Internal networking`

`Internal networking` 模式下,只有虚拟机之间可以相互访问.

## 仅主机`Host-only networking`

`Host-only networking` 模式下,只有虚拟机<=>主机 虚拟机<=>虚拟机之间可相互访问.

## 通用网络`Generic networking`

`Generic networking` 模式,当选择Generic networking网络模式时,会创建一个完全隔离的内部网络供虚拟机使用.外界无法访问这段内部网络,也无法访问外界网络.
  这种方式提供了以下几个优点:

+ 安全:由于网络隔离,可以防止未经授权的外部访问.
+ 简单:无需配置网卡或交换机等,开箱即用.
+ 正常通信:虚拟机之间可以正常通信,进行测试等.
另外,我们还可以为这段内部网络分配网段信息,如:
- IPv4网络:192.168.xxx.0/24
- IPv6网络:fd00::xxx:0/64
然后在虚拟机的网络设置中,将适配器连接至"Generic networking"网络,并配置静态IP或DHCP以获取网络地址.

---- 

一台虚拟机可设置多张网卡,比如设置两张网卡,第一张网卡选NAT模式,所以虚拟机可以访问外网,第二张网卡选Host-only networking模式,所以虚拟机可访问主机和其他虚拟机,反之也可以访问.

有关在不同的网络模式下,虚拟机\主机\局域网/外网之间的可访问规则,官方文档给了一个非常好的图表,这里也给大家看下:
![](https://ask.qcloudimg.com/http-save/yehe-5449215/mh64wznhht.png)