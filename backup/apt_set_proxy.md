---
title: 'apt设置代理'
date: 2023-09-29 20:07:07
tags: [Proxy]
published: true
hideInList: false
feature: 
isTop: false
---
# 创建代理配置文件

创建文件`/etc/apt/apt.conf.d/10proxy`,`在文件中添加如下内容

```bash
Acquire::http::Proxy::dl.google.com "http://127.0.0.1:8889/";
Acquire::https::Proxy::dl.google.com "http://127.0.0.1:8889/";
Acquire::http::Proxy::download.docker.com "http://127.0.0.1:8889/";
Acquire::https::Proxy::download.docker.com "http://127.0.0.1:8889/";
Acquire::http::Proxy::download.sublimetext.com "http://127.0.0.1:8889/";
Acquire::https::Proxy::download.sublimetext.com "http://127.0.0.1:8889/";
```
`sed -i 's/127.0.0.1/192.168.1.20/g' /etc/apt/apt.conf.d/10proxy`
上面的配置表示在apt对dl.google.com进行访问时,通过127.0.0.1的8889端口走http(s)流量访问

一把梭

```shell
echo -e 'Acquire::http::Proxy::dl.google.com "http://192.168.1.20:8889/";\nAcquire::https::Proxy::dl.google.com "http://192.168.1.20:8889/";\nAcquire::http::Proxy::download.docker.com "http://192.168.1.20:8889/";\nAcquire::https::Proxy::download.docker.com "http://192.168.1.20:8889/";\nAcquire::http::Proxy::download.sublimetext.com "http://192.168.1.20:8889/";\nAcquire::https::Proxy::download.sublimetext.com "http://192.168.1.20:8889/";\nAcquire::http::Proxy::mega.nz "http://192.168.1.20:8889/";\nAcquire::https::Proxy::mega.nz "http://192.168.1.20:8889/";\nAcquire::http::Proxy::packages.microsoft.com "http://192.168.1.20:8889/";\nAcquire::https::Proxy::packages.microsoft.com "http://192.168.1.20:8889/";\nAcquire::http::Proxy::packagecloud.io "http://192.168.1.20:8889/";\nAcquire::https::Proxy::packagecloud.io "http://192.168.1.20:8889/";\nAcquire::http::Proxy::ppa.launchpadcontent.net "http://192.168.1.20:8889/";\nAcquire::https::Proxy::ppa.launchpadcontent.net "http://192.168.1.20:8889/";\nAcquire::http::Proxy::ports.ubuntu.com "http://192.168.1.20:8889/";\nAcquire::https::Proxy::ports.ubuntu.com "http://192.168.1.20:8889/";\nAcquire::http::Proxy::ppa.launchpadcontent.net "http://192.168.1.20:8889/";\nAcquire::https::Proxy::ppa.launchpadcontent.net "http://192.168.1.20:8889/";\n' > /etc/apt/apt.conf.d/10proxy
```