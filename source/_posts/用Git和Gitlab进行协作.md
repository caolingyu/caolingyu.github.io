---
title: 用Git和Gitlab进行协作
tags:
  - Gitlab
originContent: ''
categories:
  - Tech
toc: false
date: 2019-01-08 10:26:50
---


在Gitlab上的远程仓库为每个用户创建分支, 例如dev-xxx
本地clone项目以后用fetch命令将远程分支拉到本地
```
git fetch origin dev-xxx:dev-xxx
```
在本地切换分支
```
git checkout dev-xxx
```
然后进行开发并提交修改
开发完成后提交到远程dev-xxx分支
```
git push -u origin dev-xxx
```
之后可以在网页端提交merge request

**注意**:  为了确保本地dev-xxx分支和远程仓库master分支一致, 请在每次开发前先更新本地仓库(dev-xxx分支)
```
git checkout dev-xxx
git fetch --all
git reset --hard origin/dev-xxx
```