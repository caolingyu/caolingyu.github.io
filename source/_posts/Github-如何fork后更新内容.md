---
title: Github 如何fork后更新内容
date: 2017-07-08 22:23:09
categories: Tech
tags: 
  - Github
---
在github上fork了一个仓库以后更新内容的方法
<!-- more -->
- 给fork配置远程库
	- 使用  
	`git remote -v`  
	查看远程状态
	- 确定一个将被同步给fork远程的上游仓库  
	`git remote add upstream URL`  
	- 再次查看状态确认是否配置成功  
- 同步fork
	- 从上游仓库fetch分支和提交点，提交给本地master，并会被存储在一个本地分支upstream/master  
	`git fetch upstream`  
	- 切换到本地主分支（如果不在的话）  
	`git checkout master`  
	- 把upstream/master分支合并到本地master上，这样就完成了同步，并且不会丢掉本地修改的内容  
	`git merge upstream/master`  
	- 如果想更新到github的fork上  
	`git push origin master`

Reference: [知乎](https://www.zhihu.com/question/28676261)
	
