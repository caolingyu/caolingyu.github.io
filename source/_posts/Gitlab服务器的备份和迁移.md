---
title: Gitlab服务器的备份和迁移
date: 2018-06-18 14:01:47
categories: Tech
tags:
  - Gitlab
  - Ubuntu
---

之前在一台Ubuntu的服务器上搭建了一个Gitlab服务器，最近这台服务器即将被回收，所以需要将原来的Gitlab迁移到新的服务器上，由于我是用Omnibus安装的，备份和还原的步骤相对来说比较简单，但也有不少需要注意的点。

首先说一下环境和版本  
- 系统：Ubuntu 16.04
- Gitlab版本：gitlab-ee_10.7.0-ee.0_amd64
- 安装方法：Omnibus

大致流程如下  
1. 在原服务器执行备份
2. 在新服务器安装**相同版本**的Gitlab
3. 将原服务器的备份传输到新服务器
4. 执行还原命令
5. Done

在原服务器进行备份相当简单，只需要执行以下命令  
``gitlab-rake gitlab:backup:create``
默认的备份位置是/var/opt/gitlab/backups，由于原服务器这个分区的空间已经不足了，所以在备份的时候出现报错，这里顺便提一下，第一次报错以后我把backups文件夹删除又创建了，再执行备份命令的时候提示权限不够，执行以下命令可以解决  
```
chown git /var/opt/gitlab/backups
chmod 700 /var/opt/gitlab/backups
```
磁盘空间不足的问题可以通过修改备份的保存位置解决  
打开/etc/gitlab/gitlab.rb文件，找到这一行  
``default['gitlab']['gitlab-rails']['backup_path'] = "/var/opt/gitlab/backups"``
修改后面的路径以后reconfigure一下再备份即可  

在新服务器上安装完gitlab以后，执行以下命令进行还原  
```
sudo gitlab-ctl stop unicorn
sudo gitlab-ctl stop sidekiq
sudo gitlab-rake gitlab:backup:restore BACKUP='your_backup_file'
sudo gitlab-ctl restart
```
如果要备份和还原配置文件的话只需要将/etc/gitlab文件夹打包传输到新服务器，解压放到新服务器相同的目录下。可以将新gitlab产生的配置文件夹备份一下以备不时之需。
