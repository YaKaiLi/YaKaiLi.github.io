---
title: git push error ':' 更新被拒绝，因为您当前分支的最新提交落后于其对应的远程分支
date: '2022-12-15'
slug: git-push-error1-1
tags:
  - Troubleshooting
  - Misc
mathjax: true
---
# 报错
```shell
! [rejected]        master -> master (non-fast-forward)
error: 无法推送一些引用到 'https://github.com/xxx.git'
提示：更新被拒绝，因为您当前分支的最新提交落后于其对应的远程分支。
提示：再次推送前，先与远程变更合并（如 'git pull ...'）。详见
提示：'git push --help' 中的 'Note about fast-forwards' 小节。
```

# 解决方案
因为当前分支的最新提交落后于其对应的远程分支，所以我们先从远程库fetch到更新再和本地库合并，之后git push即可。
```git
git fetch origin
git merge origin/master

```
