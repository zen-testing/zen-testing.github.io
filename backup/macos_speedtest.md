---
title: 'Monterey 测试网速'
date: 2022-09-26 17:50:05
tags: [macOS]
published: true
hideInList: false
feature: 
isTop: false
---
新版macOS已经内置了一个网络情况测试工具`networkQuality`

<!-- more -->

终端执行后,系统会开始同时测试下载和上传速度,并将当前速率实时显示在终端窗口中,形如:

```shell
current download capacity: 247.850 Mbps - current upload capacity: 9.545 Mbps
```

大约半分钟后,测速完成,终端会显示一段测速结果,形如:
```shell
Upload capacity: 16.938 Mbps
Download capacity: 232.850 Mbps
Upload flows: 20
Download flows: 16
Responsiveness: Low (188 RPM)
```
其中
`Upload/download capacity`是指上传/下载的带宽
`Upload/download flows`是指刚才测试中完成传输的测速文件数量.
`Upload/download responsiveness`是指上传和下载的综合响应能力
根据 Apple 的支持文档,它的衡量指标是每分钟往返次数 (RPM),即在正常工作条件下,网络能够在一分钟内完成的连续往返次数或事务数量.

如上所述,networkQuality 工具会使用 Apple 的 CDN 作为测试服务器.
具体而言,该工具默认会从一个外部 [json 格式文件](https://mensura.cdn-apple.com/api/v1/gm/config)获取测试配置,该文件包含三个测试文件地址:
+ [一个小文件]( https://mensura.cdn-apple.com/api/v1/gm/small)大小为1字节内容为字母`x`
+ [一个大文件](https://mensura.cdn-apple.com/api/v1/gm/large)大约4GB内容为字母 `x`的填充
+ [一个上传文件](https://mensura.cdn-apple.com/api/v1/gm/slurp)

此外,networkQuality 命令可以接受一些参数
比较有实际意义的包括:
+ -c 会输出 json 格式的测速详情;
+ -s 会分开测试下载和上传,而非像默认那样对两者同时测试(同时测试更能反映通话等真实应用的场景)
+ -I 可以测试特定网络接口的速度,例如命令`networkQuality -I en0`是指测试内建 Wi-Fi 网络的速度

更多参数和说明,可以用如下命令查阅手册页面`man networkQuality`
