---
title: commit了一个大文件导致本地仓库无法推送到github的问题解决方法
date: '2022-12-15'
slug: git-commit-large-file-error
tags:
  - Troubleshooting
  - Misc
  - Git
---
# 报错
```shell
枚举对象中: 57, 完成.
对象计数中: 100% (57/57), 完成.
使用 8 个线程进行压缩
压缩对象中: 100% (37/37), 完成.
写入对象中:  28% (11/38)
写入对象中: 100% (38/38), 365.92 MiB | 4.85 MiB/s, 完成.
总共 38（差异 23），复用 0（差异 0），包复用 0
remote: Resolving deltas: 100% (23/23), completed with 17 local objects.
remote: error: Trace: 6448613dc94eb67bde9d616c155fb2439e91be5f08cd3779c6c437de550ab696
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File xxx.zip is 369.06 MB; this exceeds GitHub's file size limit of 100.00 MB
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
To https://github.com/xxx.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: 无法推送一些引用到 'https://github.com/xxx.git'
```

# 解决方案
因为该大文件不是必须的，删除该文件。然后撤销commit，最后重新提交即可。

## 撤销commit
先查看一下最近提交的commit的版本号。

```shell
❯ git log 

commit 9f094ff19482703f6bdb171972ba0277d40a2d2e (HEAD -> master)
Author: YaKaiLi <jkliyakai@163.com>
Date:   Thu Dec 15 12:17:48 2022 +0800

    commit_comment1

commit b2ce60fe770ef618798141a5ec78c5e7112b3540
Author: YaKaiLi <jkliyakai@163.com>
Date:   Thu Dec 15 12:11:22 2022 +0800

    commit_comment2

```

commit 9f094ff19482703f6bdb171972ba0277d40a2d2e这个id就是添加大文件的commit，退回到它之前的commit b2ce60f这个即可

```shell
❯ git reset b2ce60f
```

## 重新提交
```git
git add .
git commit -m "comment1"
git push -u origin master
```
