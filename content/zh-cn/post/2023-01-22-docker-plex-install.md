---
title: docker安装plex及设置
date: '2023-01-22'
slug: docker-plex-install
tags:
  - Homelab
  - Misc
---

# 搭建Plex Server
新建文件夹`plex`， 创建`docker-compose.yml`
```shell
mkdir plex && cd plex
touch docker-compose.yml
```
`vim docker-compose.yml`写入下面的配置

```
version: "2.1"
services:
  plex:
    image: linuxserver/plex
    container_name: plex
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM=claim-oqS-kqzp41AmFK7-nX1z
    volumes:
      - ./config:/config
      - /mnt/this:/movies:ro
    restart: unless-stopped
    devices:
      - /dev/dri:/dev/dri #optional
    ports:
      - 32400:32400
```
注意事项
- `PUID`和`PGID`用于配置容器内进程的`UID`和`GID`， 全都设置为`0`表示以`root`用户运行，如果你这里不是很明白的话可以无脑设置为0以避免部分权限问题

- `PLEX_CLAIM`环境变量用于认证自己的服务器，也是可选， 你可以从 [这里](https://www.plex.tv/claim/) 获取(注意需要可用的plex账号)， 另外`claim`的有效期一般只有 4 分钟 ，如果服务器网络不佳，建议先通过执行`docker-compose pull linuxserver/plex`拉取镜像之后再获取，防止过期(虽说过期后再重新claim也行)。

- `/mnt/this:/movies:ro` 将自己本地的影片库映射到`plex container`的`/movies`目录， 并且只读(`ro即read only`)

执行`docker compose up -d`然后静待服务器启动完成， 启动完成后可以访问ip:32400/web进入web界面

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/22/23-15-56-9a5a9608093b5a260007e061b75b823b-96e924.png)


附：直接在主机上安装的方式
```
wget https://downloads.plex.tv/plex-media-server-new/1.25.7.5604-980a13e02/redhat/plexmediaserver-1.25.7.5604-980a13e02.x86_64.rpm
rpm -i plexmediaserver-1.25.7.5604-980a13e02.x86_64.rpm
systemctl enable plexmediaserver.service
systemctl start plexmediaserver.service
```