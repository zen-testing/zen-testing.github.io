---
title: 'openai tts'
date: 2024-04-08 11:11:37
tags: [AI,Docker]
published: true
hideInList: false
feature: https://s21.ax1x.com/2024/04/08/pFLnWBn.png
isTop: false
---
```yml
version: '3.8'
name: tts
services:
  tts-service:
    image: registry.hf.space/ysharma-openai-tts-new:latest
    platform: linux/amd64
    command: python app.py
    ports:
      - "7860:7860"  #:左侧的端口可以自定义
    volumes:
            - '/f/data/tts:/tmp' #会报错但是省掉下载步骤
    stdin_open: true
    tty: true
```