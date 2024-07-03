---
title: '安卓手机通过图形界面查看电池历史记录'
date: 2022-09-26 15:19:39
tags: [Android]
published: true
hideInList: false
feature: 
isTop: false
---

>应广大网友要求,从头到尾实现了一遍这个工具,因为Docker在Windows上和macOS上都有相应的Docker Desktop图形管理工具,难度也不会太大,所以直接使用Linux端作为范本,Linux会了其他就不成问题了

开始
----
# 安装docker

这里没什么难点,直接跟随官网的[安装文档](https://docs.docker.com/engine/installation/)安装就可以了

# 下载镜像

```shell
$ docker pull gcr.io/android-battery-historian/stable:3.0
```

这里有可能因为墙的原因一直无法连接下载服务器

解决方法如下

```
# mkdir -p /etc/systemd/system/docker.service.d
# touch /etc/systemd/system/docker.service.d/proxy.conf
```

其中`proxy.conf`的内容为

```shell
[Service]
Environment="HTTP_PROXY=http://proxy.example.com:8080/"
Environment="HTTPS_PROXY=http://proxy.example.com:8080/"
# http://proxy.example.com:8080 更换成你自己的代理
# 可选填
# Environment="NO_PROXY=localhost,127.0.0.1,.example.com"
```

# 运行容器

```shell
docker run -p <port>:9999 gcr.io/android-battery-historian/stable:3.0 --port 9999
```

`<port>`更换为你自己喜欢的端口号,比如

```shell
docker run -p 2147:9999 gcr.io/android-battery-historian/stable:3.0 --port 9999
```

# 本机浏览器访问

随便打开一个浏览器输入网址
`localhost:2147`
或
`127.0.0.1:2147`
就会打开一个网页

像这样

![首页](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/battery-historian/index.webp)

# Browse 导入你的错误报告

那么问题来了,错误报告去哪找?

![错误报告](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/battery-historian/bugReport.webp)

或者直接使用ADB工具

```shell
# Android 7.0 或更高
$ adb bugreport bugreport.zip
```

```shell
# Android 6.0 或更低
$ adb bugreport > bugreport.txt
```

# 选中后点击右边提交

![提交](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/battery-historian/submit.webp)

# 完整的电池历史记录报告生成了

导出,打印,截图,发朋友圈,随你怎么折腾
![效果](https://raw.githubusercontent.com/zhangyiming748/zhangyiming748.github.io/master/img/battery-historian/done.webp)

----

竟然还有人反馈docker方案太难,那你们可以去[项目源地址](https://github.com/google/battery-historian)下载代码自己编译安装,不说精通Golang和Python,最起码一门语言一本书
