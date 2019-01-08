---
title: 用flask、gunicorn和nginx在centos上部署API
date: 2018-06-04 21:08:04
categories: Tech
tags:
  - Flask
  - gunicorn
  - Nginx
  - CentOs
---
最近需要把ICD编码和命名实体识别的API部署在公司外网gpu服务器上，服务器是centos系统的，网上的教程大多数都是基于ubuntu的，于是自己研究了一下，简单说一下步骤吧。
<!-- more -->

1. 我用的conda，首先创建一个虚拟环境env
```
conda create -n env python=3.6
source activate env
```
2. 安装flask（如果没有的话）, gunicorn  
``pip install flask gunicorn``
3. 在代码目录中创建一个`wsgi.py`文件，内容如下
```python
from app import app  
if __name__ == "__main__":  
	app.run()
```
4. 试着启动一下（可以在screen或者tmux里）  
``gunicorn --bind 127.0.0.1:8000 wsgi:app``
5. 安装nginx  
``yum install nginx``
添加一个配置文件  
``sudo vim /etc/nginx/conf.d/project.conf``
写入以下内容  
```
server {
	listen 80;
	server_name  your_public_dnsname_here;
	
	location / {
		proxy_pass http://127.0.0.1:8000;
	}
}
```
6. 启动nginx服务，搞定！  
``systemctl start nginx``


