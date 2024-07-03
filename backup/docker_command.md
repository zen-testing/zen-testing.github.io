---
title: 'docker常用命令'
date: 2022-09-26 16:08:10
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
# 导入镜像

```shell
$ docker load -i ./openEuler-docker.aarch64.tar.xz
```

# 创建一个新的容器并启动

```shell
$ docker run --name=openEuler --cpus=2 --memory=5120M -p 2222:22 -v /Users/zen/container:/mnt --privileged -it openeuler-22.03-lts /bin/bash
```

# 插曲

openEuler设置了超时这个奇葩设定,也就是600秒不操作当前终端连着整个容器都给你关掉
解决方法就是注释掉`/etc/bashrc`最后一行关于超时的设定

# linux上设置pull镜像

1. 创建或修改 /etc/docker/daemon.json 文件,修改为如下形式
```shell
{
    "builder": {
        "gc": {
            "defaultKeepStorage": "20GB", 
            "enabled": true
        }
    }, 
    "experimental": false, 
    "registry-mirrors": [
        "https://mirror.baidubce.com", 
        "https://registry.docker-cn.com", 
        "https://docker.mirrors.ustc.edu.cn", 
        "http://hub-mirror.c.163.com", 
        "https://cr.console.aliyun.com/"
    ]
}
```

2. 重启docker服务使配置生效

```shell
$ sudo systemctl restart docker.service
```

<center>docker run -dti --privileged --net=host -v /dev/bus/usb:/dev/bus/usb --name=gsmsystem gsmsystem:1.2</center>

|参数|说明|
|:---:|:---:|
|-d|在后台运行容器并打印容器 ID|
|-t|分配一个伪 TTY|
|-i|即使没有连接,也保持 STDIN 打开|
|--privileged|授予此容器扩展权限|
|--net=bridge/host|设置容器的网络模式|
|-v|绑定挂载卷|
|--name|为容器分配名称|
|--cpus|限制可使用的cpu数量,如1.5|
|--memory|限制可使用的内存,如5120M|

# 删除镜像

```shell
docker rmi [image]
```
# 修改好的容器提交为新的镜像

```shell

docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

如

$ docker commit -a zen -m "更换安装源为阿里云" ubuntu_chinese ubuntu_chinese:1.0.0

```

`-a` :提交的镜像作者

`-c` :使用Dockerfile指令来创建镜像

`-m` :提交时的说明文字

`-p` :在commit时,将容器暂停

# 把制作好的镜像保存为文件

```shell
docker save -o filename.tar <image>
```

# tips
+ 不要把本地目录挂载到`/tmp`
+ 需要先安装`ca-certificates`或者apt源使用http(而不是https)

# 实例

```shell
$ docker run --name=ubuntu_chinese --cpus=2 --memory=2048M -p 2222:22 -v /Users/zen/container:/mnt --privileged --hostname dubuntu -it ubuntu /bin/bash
$ docker commit -a zen -m "本地化初始状态ubuntu" ubuntu_chinese ubuntu_chinese:latest
$ docker tag ubuntu_chinese 1324567980/ubuntu_chinese:0.0.1
$ docker push 1324567980/ubuntu_chinese:0.0.1
$ docker run -dit -v /Users/zen/container/ql:/ql/data -p 5700:5700 --name qinglong --hostname qinglong --restart unless-stopped whyour/qinglong:latest
```
