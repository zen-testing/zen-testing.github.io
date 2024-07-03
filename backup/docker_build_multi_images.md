---
title: 'docker build 如何构建一个同时支持在多平台导入的images？'
date: 2024-03-10 15:07:58
tags: [Docker]
published: true
hideInList: false
feature: 
isTop: false
---
要创建一个同时支持在x86、arm64和amd64平台上运行的Docker镜像，你需要使用多阶段构建，并在每个阶段中为不同的架构编译你的应用程序。

以下是一个示例Dockerfile，它使用Go语言编写的应用程序：

```dockerfile
# 第一阶段：获取Go编译器
FROM golang:1.16-alpine AS builder

# 设置工作目录
WORKDIR /app

# 复制源代码到容器中
COPY . .

# 编译应用程序
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o app .

# 第二阶段：创建基础镜像
FROM alpine:latest

# 设置工作目录
WORKDIR /app

# 从第一阶段复制应用程序
COPY --from=builder /app/app .

# 暴露端口
EXPOSE 8080

# 启动应用程序
CMD ["./app"]
```

这个Dockerfile首先使用Go编译器的镜像构建一个名为`builder`的阶段，然后在该阶段中编译应用程序。然后，它创建一个基于Alpine Linux的基础镜像，并从`builder`阶段复制编译后的应用程序。

但是，这个Dockerfile只支持amd64架构。要支持其他架构，你需要为每个架构创建一个单独的阶段，并为每个阶段设置适当的`GOOS`和`GOARCH`环境变量。例如，要添加对arm64的支持，你可以添加以下阶段：

```dockerfile
# 第三阶段：编译arm64架构的应用程序
FROM golang:1.16-alpine AS arm64-builder

# 设置工作目录
WORKDIR /app

# 复制源代码到容器中
COPY . .

# 编译应用程序
RUN CGO_ENABLED=0 GOOS=linux GOARCH=arm64 go build -o app .

# 第四阶段：将arm64架构的应用程序复制到基础镜像
FROM alpine:latest

# 设置工作目录
WORKDIR /app

# 从arm64-builder阶段复制应用程序
COPY --from=arm64-builder /app/app .

# 暴露端口
EXPOSE 8080

# 启动应用程序
CMD ["./app"]
```

最后，你需要使用`docker buildx`命令构建镜像，以便在多个架构上构建和测试镜像。例如：

```bash
# 启用Docker构建实验功能
export DOCKER_BUILDKIT=1

# 构建镜像
docker buildx build --platform linux/amd64,linux/arm64 -t my-app:latest .
```

这将在amd64和arm64架构上构建镜像，并将它们标记为`my-app:latest`。然后，你可以使用`docker run`命令在适当的架构上运行镜像。