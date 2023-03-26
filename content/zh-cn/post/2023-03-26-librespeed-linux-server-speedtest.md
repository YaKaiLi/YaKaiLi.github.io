---
title: 搭建linux服务器网页测速
date: '2023-03-26'
slug: librespeed-linux-server-speedtest
tags:
  - Misc
  - Software
---


```shell
docker run -d \
  --name=librespeed \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e PASSWORD="password" \
  -p 80:80 \
  -v ~/librespeed/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/librespeed:latest
```