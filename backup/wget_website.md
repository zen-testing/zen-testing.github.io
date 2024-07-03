---
title: '利用wget复制网站'
date: 2022-09-26 15:57:02
tags: [Linux]
published: true
hideInList: false
feature: 
isTop: false
---

```shell
$ wget -E -c -r -p -k -np -l 100  http://localhost/example/
```

|参数|说明|
|:---:|:---:|
|-E,--adjust-extension|如果下载了一个网页文件,但是没有后缀,使用这个选项会自动调整后缀为html.这个选项在处理动态网站的时候很有用|
|-c,--continue|续传|
|-r,--recursive|递归下载,使用这个选项之后,wget会自动找到当前页面中的链接,并下载链接对应的文件|
|-p,--page-requisites|下载正常显示页面所需要的所有资源文件,比如内置图片\css文件等等|
|-k,--convert-links|将链接中的绝对路径转换为相对路径,这样下载的文件可以放置在任何位置访问|
|-np,--no-parent|不下载指定url的父目录中的文件,在本例中,这个选项表示只下载目标网站example/目录下的文件|
|-l,--level=NUMBER|最大递归深度|