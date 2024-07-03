---
title: '5分钟学会Linux的ps命令'
date: 2023-11-23 17:18:38
tags: [五分钟已经很棒了]
published: true
hideInList: false
feature: 
isTop: false
---
默认输出当前控制台的当前用户任务
-f 显示当前的完整格式输出
-e / -A 展示所有进程

`ps -aux --sort +vsz | tail -n 10`
-a 与当前用户当前终端相关的进程
-u BSD风格
-x 当前终端外所有进程
VSZ = Virtual Memory Size 虚拟内存
RSS = Resident Set Size 物理内存
```bash
root        1363  0.0  0.0 1229336 3224 ?        Sl   Nov17   0:00 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 9000 -container-ip 172.17.0.3 -container-port 9000
root        1377  0.0  0.0 1229592 3212 ?        Sl   Nov17   0:00 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 8000 -container-ip 172.17.0.3 -container-port 8000
root        1294  0.0  0.0 1303384 3232 ?        Sl   Nov17   0:00 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 3000 -container-ip 172.17.0.2 -container-port 3000
root        1383  0.0  0.0 1303384 3208 ?        Sl   Nov17   0:00 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 8000 -container-ip 172.17.0.3 -container-port 8000
zen       982536  0.0  0.2 1310224 9780 ?        Ssl  09:33   0:00 rootlesskit --net=slirp4netns --mtu=65520 --slirp4netns-sandbox=auto --slirp4netns-seccomp=auto --disable-host-loopback --port-driver=builtin --copy-up=/etc --copy-up=/run --propagation=rslave /usr/bin/dockerd-rootless.sh
zen       982643  0.0  0.9 1343480 35500 ?       Ssl  09:33   0:00 containerd --config /run/user/1000/docker/containerd/containerd.toml
zen       982555  0.0  0.2 1383760 8424 ?        Sl   09:33   0:00 /proc/self/exe --net=slirp4netns --mtu=65520 --slirp4netns-sandbox=auto --slirp4netns-seccomp=auto --disable-host-loopback --port-driver=builtin --copy-up=/etc --copy-up=/run --propagation=rslave /usr/bin/dockerd-rootless.sh
root         792  0.0  1.0 1417528 39544 ?       Ssl  Nov17   1:18 /usr/bin/containerd
zen       982606  0.0  1.6 1516000 64932 ?       Sl   09:33   0:00 dockerd
root         852  0.0  1.8 2475808 72532 ?       Ssl  Nov17   0:52 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```
