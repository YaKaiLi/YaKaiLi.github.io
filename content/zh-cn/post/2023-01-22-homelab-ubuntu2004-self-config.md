---
title: Homelab Ubuntu20.04系统安装后自用配置
date: '2023-01-22'
slug: homelab-ubuntu2004-self-config
tags:
  - Misc
  - Homelab
---

# 换国内源
配置中科大源
```shell
sudo sed -i 's@//.*archive.ubuntu.com@//mirrors.ustc.edu.cn@g' /etc/apt/sources.list
sudo apt update
```

# ssh配置
## 安装ssh
```shell
sudo apt update
sudo apt install openssh-server vim
```
## 配置密钥
```shell
ssh-keygen
cd .ssh
cat id_rsa.pub >> authorized_keys
chmod 600 authorized_keys
chmod 700 ~/.ssh
```

```shell
sudo vim /etc/ssh/sshd_config
```

`sshd_config`文件内修改：
```
RSAAuthentication yes #开启密钥登陆
PubkeyAuthentication yes #开启密钥登陆

PasswordAuthentication no # 禁用密码登陆

PermitRootLogin no # 禁用root用户登录
```

```shell
service sshd restart
```
然后在客户端使用id_rsa文件作为密钥登陆即可

# 远程桌面设置
可以使用ubuntu自带的屏幕共享功能(基于Vino)，但有可能需要安装下才会在菜单中显示。
## 安装vino
```shell
sudo apt install vino
```
### 配置vino
首先在设置里配置屏幕共享
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/22/19-01-10-8843c84ce098b51bef1af8cc813a5b3b-8510c3.png)

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/22/19-01-33-d4b043531d93248a487c588b9ac68ab2-66c732.png)
密码最多可以设置8位

然后在终端中再进行配置
```shell
gsettings set org.gnome.Vino require-encryption false
# 关闭vino的require-encryption选项
```

参考：https://www.cnblogs.com/jzcn/p/16624641.html
https://blog.csdn.net/Naisu_kun/article/details/123007055

## 安装todesk
```shell
wget https://newdl.todesk.com/linux/todesk-v4.3.1.0-amd64.deb
sudo apt-get install ./todesk-v4.3.1.0-amd64.deb
todesk #启动
```

## 安装向日葵
```shell
wget https://dl-cdn.oray.com/sunlogin/linux/SunloginClient_11.0.1.44968_amd64.deb
sudo apt install ./SunloginClient_11.0.1.44968_amd64.deb
```

## 安装teamviewer
```shell
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
sudo apt install ./teamviewer_amd64.deb
```

# 精简 Ubuntu 20.04 -- 删除不必要的自带软件

系统预装了一些无用或者用处很少的软件
执行下面这行命令可以删除它们

```shell
sudo apt remove remmina libreoffice-common thunderbird totem rhythmbox simple-scan gnome-mahjongg aisleriot gnome-mines cheese transmission-common gnome-sudoku
```
```
#根据个人习惯自行决定是否删除
remmina	远程桌面
libreoffice	办公软件
thunderbird	邮件客户端
totem	视频播放
rhythmbox	音乐播放器
simple-scan	文档扫描仪
gnome-mahjongg	对对碰游戏
aisleriot	接龙游戏
gnome-mines	扫雷
cheese	茄子(拍照)
transmission-common	bt下载
gnome-sudoku	数独
```

然后自动卸载不需要的依赖
```shell
sudo apt --purge autoremove
```

最后更新软件包
```shell
sudo apt upgrade	#更新软件仓库
```


# 安装docker
docker官方的源比较慢，采用阿里云的docker源进行安装。

https://developer.aliyun.com/mirror/docker-ce
```shell
# step 1: 安装必要的一些系统工具
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
# step 2: 安装GPG证书
curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
# Step 3: 写入软件源信息
sudo add-apt-repository "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
# Step 4: 更新并安装Docker-CE
sudo apt-get -y update
sudo apt-get -y install docker-ce
```

设置非root账户执行docker命令
```shell
# 1.创建名为docker的组，如果之前已经有该组就会报错，可以忽略这个错误：
sudo groupadd docker

# 2.将当前用户加入组docker：
sudo gpasswd -a ${USER} docker

# 3.重启docker服务
sudo systemctl restart docker

# 4.添加访问和执行docker sock的权限：
sudo chmod a+rw /var/run/docker.sock

```
# 安装Anaconda
下载安装：
```shell
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
bash Anaconda3-2022.10-Linux-x86_64.sh
```
配置conda国内源：清华源。

https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/
```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

conda config --set show_channel_urls yes

conda clean -i # 清除索引缓存
```

