---
title: Mac使用拓展坞有线网卡和无线网卡实现内外网同时访问
date: '2023-04-13'
slug: mac-use-two-net-interfeces
tags:
  - Misc
  - Software
---

目标是`10.49.x.x`走拓展坞有线网卡，其余走无线网卡。

## 查看网卡名称
```
ifconfig
```
无线网卡名称为：`en0`，拓展坞有线网卡名称为：`en4`。

## 查看只插有线网卡的路由

```shell
❯ route get 10.49.0.1
   route to: 10.49.0.1
destination: default
       mask: default
    gateway: 192.168.14.254
  interface: en4
      flags: <UP,GATEWAY,DONE,STATIC,PRCLONING,GLOBAL>
 recvpipe  sendpipe  ssthresh  rtt,msec    rttvar  hopcount      mtu     expire
       0         0         0         0         0         0      1500         0
```

## 添加路由
```shell
sudo route add -net 10.49.0.0/16 192.168.14.254
# -interface en4
```


