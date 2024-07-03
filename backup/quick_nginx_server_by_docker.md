---
title: '快速开启一个nginx服务器'
date: 2024-03-01 22:06:23
tags: [Docker,nginx]
published: true
hideInList: false
feature: 
isTop: false
---
在宿主机配置nginx.conf文件
# /home/zen/nginx/nginx.conf
```shell
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log;
pid /run/nginx.pid;
include /usr/share/nginx/modules/*.conf;
events {
    worker_connections 1024;
}
http {
    charset utf-8;
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    access_log  /var/log/nginx/access.log  main;
    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;
    default_type        application/octet-stream;
    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;
    server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;
        location / {
            root    /usr/share/nginx/html/download;
        autoindex on;    #开启索引功能
        autoindex_exact_size off;  #关闭计算文件确切大小（单位bytes），只显示大概大小（单位kb、mb、gb）
        autoindex_localtime on;   #显示本机时间而非 GMT 时间
        }
        error_page 404 /404.html;
            location = /40x.html {
        }
        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
}
```

启动参数
```shell
docker run --name nginx -v /home/zen/nginx/nginx.conf:/etc/nginx/nginx.conf -v /home/zen/nginx/download/:/usr/share/nginx/html/download -p 80:80 -d nginx:latest
```
或者
```shell
version: '3.9'
services:
    nginx:
        image: 'nginx:latest'
        ports:
            - '80:80'
        volumes:
            - '/home/zen/nginx/download/:/usr/share/nginx/html/download'
            - '/home/zen/nginx/nginx.conf:/etc/nginx/nginx.conf'
        container_name: nginx
 ```
使用docker-compose up -d .启动