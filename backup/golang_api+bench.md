---
title: 'Golang的API压测工具 hey'
date: 2022-09-26 16:53:13
tags: [Golang]
published: true
hideInList: false
feature: 
isTop: false
---

[工具地址](https://github.com/rakyll/hey)

## 实例
```
`hey -n 200 -c 2 -m POST -T "application/x-www-form-urlencoded" -d ‘userId=&uuid=&action=*****’ http://127.0.0.1:9090/api/recommend/v1/xxx
```
## 参数

|参数|功能|
|:---:|:---:|
|-n|要运行的请求数<br>默认是200|
|-c|并发运行的请求数<br>请求的总数不能小于并发级别<br>默认是50|
|-q|速率限制<br>以每秒查询(QPS)为单位<br>默认没有限制|
|-z|发送请求的应用程序配置<br>当时间到了<br>应用程序停止并退出<br>如果指定持续时间,则忽略n<br>例子:- z 10s - z 3m|
|-o|输出类型<br>如果没有提供,则打印摘要<br>"csv"是唯一受支持的替代方案<br>转储文件的响应以逗号分隔值格式的度量|
|-m|HTTP method<br>one of GET, POST, PUT, DELETE, HEAD, OPTIONS|
|-H|自定义HTTP头<br>您可以通过重复标记指定所需的数量<br>如`-H "Accept: text/html" -H "Content-Type: application/xml" `|
|-t|每个请求的超时时间(以秒为单位)<br>默认值是20,使用0表示无穷大|
|-A|HTTP Accept header|
|-d|HTTP request body|
|-D|HTTP request body from file<br>如`/home/user/file.txt` or `./file.txt`|
|-T|Content-type<br>defaults to "text/html"|
|-a|Basic authentication<br>username:password|
|-x|HTTP Proxy address as host:port|
|-h2|Enable HTTP/2|
|-host|HTTP Host header|
|-disable-compression|禁用压缩|
|-disable-keepalive|禁用keep-alive<br>防止重用TCP不同HTTP请求之间的连接|
|-disable-redirects|禁用HTTP重定向的后续操作|
|-cpus|使用的cpu核数<br>当前机器默认为48核|
