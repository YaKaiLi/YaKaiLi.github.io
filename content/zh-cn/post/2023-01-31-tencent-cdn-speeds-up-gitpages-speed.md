---
title: 腾讯云CDN加速hugo的github pages
date: '2023-01-31'
slug: tencent-cdn-speeds-up-gitpages-speed
tags:
  - Misc
  - Blog
---

# 前言
通过网站测速发现很多地方访问非常慢，[点击查看](https://www.17ce.com/site/http/20230131_836e6700a11111ed9608d9f7b39b2ff3:1.html)测速详情。需要对github pages进行CDN加速。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_TwbGm7/2023/01/31/10-49-19-5eaee042cd262880bec3bc2ce000fe73-a2f596.png)

注意：腾讯云加速全球站需要网站备案，选择腾讯云加速主要是因为域名是在腾讯云注册的。
参考：https://zhuanlan.zhihu.com/p/393779644

# 配置腾讯云 CDN 服务器

点击 `域名管理` -> `添加域名`。然后在 `域名配置` 选 `中国境外`，填上自己的域名，然后选择 `CDN网页小文件`。

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/31/10-43-51-461e861cbf3afdf19df638bc0f382a7c-1b08ab.png)

github pages的ip地址列表为：
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
这里不要选择`HTTPS`，因为腾讯云的`HTTPS`是单独按次计费的，无法使用免费的10G流量。如果选择`HTTPS`，在未开通`HTTPS`服务下，网站会出现`514`状态码报错。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_tLFMYI/2023/01/31/11-27-59-8369ba2b8931e446a63f847178f67d64-6bfa4e.png)

全部文件的缓存方式改为遵循源站。
然后在推荐配置里的 `文件后缀` 里添加 `html` 的后缀。因为如果把 `index.html` 也缓存了，部署后看到还是上一个版本的 `html`。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/31/11-09-52-adb8836d184c30d3459d16ef634c3f16-7c225f.png)

修改域名DNS解析，境内CNAME为腾讯云的CDN地址`www.gnn.ac.cn.cdn.dnsv1.com.`，境外为github的地址`yakaili.github.io`。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_1m66CF/2023/01/31/11-08-43-4e32d202fe9bfeeb1138e2d2258c3e85-dbede3.png)

测速后转为全绿，CDN加速效果明显。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/20-09-22-9d406853e30d05f0671b3416c610b901-e4892e.png)

# HTTPS

## 申请阿里云免费HTTPS证书
多次申请腾讯云免费SSL证书一直签发不成功，转为申请阿里云SSL证书。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-22-10-5ec936f698f48a6260fa5afe8c26f0be-7c9225.png)

依次填写所需字段，提交审核。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-23-25-e759a14dc3ae88f775e301117aadb70a-41e463.png)
然后在域名解析中添加要求的解析字段，然后点击验证。等待大约10分钟即可签发成功。
ps：比腾讯云体验好多了QAQ，腾讯云试了好几次，每次都是验证成功后等大概两天后才通知我验证失败，可能是我哪没有配置对吧。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-25-08-c75a9de4201fef14894a36e17ed49195-1f5738.png)

## 下载并部署证书

选择`其他`栏下载证书，其中包含签名证书（.pem格式）和签名私钥（.key格式）。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-47-27-356ddbff4672a52ef64b4630265fde58-872278.png)
点击腾讯云SSL的上传证书，输入签名证书内容（.pem格式文件）和签名私钥内容（.key格式文件），点击确定即可托管证书成功。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-55-12-7d7ba721d8415756b197f711adda7eac-ba1658.png)
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-54-30-762b40d01475bb9e31733aafd592d600-e90b9f.png)

在腾讯云CDN的控制台中，对加速域名进行管理。
打开HTTPS开关并配置证书。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-56-21-e048fc4b360b440e29e8faa52e42f842-6adc00.png)
配置证书时选择上步骤托管的证书。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/02/06/19-57-39-fc3d14c4689b9e951d42be1017fe367a-d7ccfa.png)
最后等待腾讯云CDN部署完成。

访问主页不会显示https证书错误了。
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_VF6cte/2023/02/06/20-05-03-3e4a5210a31a23bfa395628ec55396ae-451414.png)
