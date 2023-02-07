---
title: PicGO 上传图片前自动压缩
date: '2023-01-31'
slug: picgo-automatically-compresses-pictures
tags:
  - Misc
mathjax: true
---
# 安装插件
采用picgo-plugin-compress插件，在PicGo-gui上直接搜索该插件并安装。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/07/10-23-29-45c4250830b0804d463f688523e4322a-8e9308.png)

# 配置
点击插件配置选择压缩方式
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/07/10-27-42-535c7dbc3e62c75d72fe7d0031e1c717-d0e531.png)

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_e6mOlz/2023/02/07/10-29-30-8c877e03951d270d2df9d771930057f5-8d9e06.png)

压缩方式有：
+ tinypng 无损压缩，需要上传到 tinypng
+ imagemin 压缩过程不需要经过网络，但是图片会有损耗
+ image2webp 本地有损压缩，支持 GIF 格式有损压缩 注意：有些图床（比如 sm.ms）不支持 webp 图片格式，会上传失败

