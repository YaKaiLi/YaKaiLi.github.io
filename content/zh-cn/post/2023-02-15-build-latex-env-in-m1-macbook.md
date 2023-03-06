---
title: Macbook（M1）搭建LaTex运行环境
date: '2023-02-15'
slug: build-latex-env-in-m1-macbook
tags:
  - Misc
  - Software
---
# MacTex安装
## 官网下载安装包
通过中科大源下载MacTex：https://mirrors.ustc.edu.cn/CTAN/systems/mac/mactex/MacTeX.pkg

官方网址：https://www.tug.org/mactex/mactex-download.html

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/03/07/01-10-21-973b73ee1ec80fd2bc5d7f7e88767f2e-d99e8f.png)


安装完之后会新增四个图标：
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_4C9Ydy/2023/03/07/01-14-48-e4f93db9baf261a57a86ae8d909e8c54-1ad964.png)

## 使用brew安装
```shell
brew install mactex --cask
```
等待安装完成即可。


## 验证MacTeX有没有安装成功

```shell
latex -v
```
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_PqC2yN/2023/03/07/01-32-51-7a9ae4a1c20766fbbdf7a9082f86ca42-a5cbbf.png)


# Texifier配置
Texifier无需配置，会自动选择MacTex作为排版器。

使用Texifier编译发现和Overleaf编译速度相差无几，而且也熟悉了Overleaf，遂抛弃本地方案。

