---
title: 安装vulfocus靶场
date: '2023-07-31'
slug: install-vulfocus
tags:
  - Pentest
---

docker pull vulfocus/vulfocus:latest

docker run -d -p 80:80 -v /var/run/docker.sock:/var/run/docker.sock  -e VUL_IP=192.168.1.105 vulfocus/vulfocus

#如果端口被占用，则命令执行不成功
#-v /var/run/docker.sock:/var/run/docker.sock 为 docker 交互连接。
#-e DOCKER_URL 为 Docker 连接方式，默认通过 unix://var/run/docker.sock 进行连接，也可以通过 tcp://xxx.xxx.xxx.xxx:2375 进行连接（必须开放 2375 端口）。
#-v /vulfocus-api/db.sqlite3:db.sqlite3 映射数据库为本地文件。
#-e VUL_IP=xxx.xxx.xxx.xxx 为 Docker 服务器 IP ，不能为 127.0.0.1
#默认账户密码为 admin/admin

