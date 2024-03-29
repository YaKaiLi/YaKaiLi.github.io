---
title: Simple install hugo with Multi-language support
date: '2022-11-27'
slug: hugo-simple-install
tags:
  - Misc
  - Software
---

just use other's confige
直接拷贝已有好的配置～

```
git clone --recurse-submodules https://github.com/CyrusYip/cyrusyip-blog.git
```
## 添加 favicon
利用https://realfavicongenerator.net/ 将头像做成favicon，然后放到static目录里
## 修改标题
修改config.toml
## 评论系统
### disqus配置（评论配置）

注册disqus账号，新建一个网站
将config.toml中的相关配置修改为disqus中自己的shortname：
```
disqusShortname = "star5o"
```
注意：需要在disqus中将自己的域名添加到收信任列表，见[官方网站](https://help.disqus.com/en/articles/1717206-how-to-use-trusted-domains)

### utteranc
首先必须在 github 上进行安装 utterances，访问 [utterances应用程序](https://github.com/apps/utterances) 然后点击 Install 按钮进行安装。
在这里可以选择可以关联的存储库，可以选择我们所拥有的库(也包括未来建立的库)或者某一个仓库，这里只选择某一个需要进行评论的库，这样比较好。

然后将配置文件`config.toml`中`params.utteranc`的`repo`参数修改为博客仓库名称，如`YaKaiLi/YaKaiLi.github.io`

## 发布并托管到Github
### 修改配置文件
参见[Hugo官方文档](https://gohugo.io/hosting-and-deployment/hosting-on-github/),配置Hugo将网页生成在名为/docs的子目录中，然后直接push到master branch。这样就可以让Github Pages加载我们想要托管的/public子目录中的网页。

在config.toml中添加如下一行配置，使得生成的网页默认保存在/docs子目录下：
```
echo "publishDir = 'docs'" >> config.toml
```
自此运行hugo命令后生成的网页文件将保存在/docs子目录下。
### 发布并托管到Github
上传到Github之前，先在Github中添加一个空白repository，仓库名为：username.github.io，注意不要添加如README，.gitignore等文档。由此得到Github中该repository的网址：https://github.com/YaKaiLi/YaKaiLi.github.io.git

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/%E6%88%AA%E5%B1%8F2022-11-25%2022.11.58.png)
复制该网址后，在本地网站文档根目录中初始化git：

```
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/YaKaiLi/YaKaiLi.github.io.git
git push -u origin master
```

至此所有源文档就都push到Github上了。然而此时Github对待这些源文档跟其他任何普通的repository中的代码并没有任何不同，并不会将public子目录中的网页托管在Github Pages上。

将所有文档push到Github的master branch，进入Github对应repository的Settings标签菜单，在Pages选项的Source栏选择master branch /docs folder:
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/%E6%88%AA%E5%B1%8F2022-11-25%2022.29.36.png)




## 配置个人域名

### hugo配置
在本地仓库docs子目录中需要添加一个名为CNAME的文档
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_gpHTEu/2022/11/25/22-53-41-61d7aee7cdd4839e45edeae9bac52ae4-ef8ceb.png)
然后回到网站目录进行git同步
```
git add .
git commit -m "commit"
git push -u origin master
```

### 域名解析
1、添加A记录（即地址记录，用来指定域名的IP地址），主机记录（Name）栏填www，记录值(Target)那栏填Github服务器IP地址（即your_name.github.io的IP地址）
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_ikHhPb/2022/11/25/22-56-43-d6d5169f3a39225b581fad8452028ed2-552c42.png)
2、添加CNAME记录（用于将一个域名映射到另一个域名），主机记录栏填@，记录值那栏填yakaili.github.io
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_Mi97Kd/2022/11/25/22-59-06-e34743664fae9b43c3fafadb22862b15-515bf5.png)


## 新建文章
```
hugo new --kind post zh-cn/post/my-article.md
```