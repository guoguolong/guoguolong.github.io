---
title: git clone的depth的妙用
tags: [git, depth]
categories: [IT]
---

在git clone时加上 --depth=1的含义是：

>depth用于指定克隆深度，为1即表示只克隆最近一次commit.

这种方法克隆的项目只包含最近的一次commit的一个分支，体积很小，即可解决文章开头提到的项目过大导致Timeout的问题，但会产生另外一个问题，他只会把默认分支clone下来，其他远程分支并不在本地，所以这种情况下，需要用如下方法拉取其他分支：

```
$ git clone --depth 1 https://github.com/guoguolong/sharpcodes.git
$ git remote set-branches origin 'remote_branch_name'
$ git fetch --depth 1 origin remote_branch_name
$ git checkout remote_branch_name
```