---
title: 通过docker安装alist来挂载网盘
date: '2023-02-06'
slug: docker-install-alist
tags:
  - Misc
  - Homelab
mathjax: true
---

# 安装
新建配置文件存放目录
```shell
mkdir ~/software/alist
```
启动容器
```shell
docker run -d --restart=always -v ~/software/alist:/opt/alist/data -p 5244:5244 --name="alist" xhofe/alist:latest
```

访问ip:5244即可进入alist
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_a6MzTC/2023/02/06/16-41-34-0f74b85b27b985bf47928c46816ea009-1f25bf.png)

输入以下命令查看初始账号密码
```shell
docker logs alist
```


# 配置阿里云盘


进入后点击`管理`添加挂载的网盘。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/16-47-06-4edcd86b015455f266a5111d78dce6e9-a6360e.png)
点击`存储`->`添加`，驱动选择阿里云盘。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/16-48-57-c019b443fcc1d25ee72a581868cdc4c1-49267a.png)
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/16-51-30-822037316ec975b02ef413a579767717-866a81.png)

通过链接[https://alist.nn.ci/zh/guide/drivers/aliyundrive.html](https://alist.nn.ci/zh/guide/drivers/aliyundrive.html)获取刷新令牌并填写

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/16-54-50-1a8947220eb76298f45938d6d672131d-f4d67e.png)

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/17-05-20-5a9b37d18edc45c566ab9e3606691f10-04ac1d.png)

接下来就可以愉快的使用Alist啦！

