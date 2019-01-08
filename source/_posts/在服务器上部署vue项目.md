---
title: 在服务器上部署vue项目
date: 2018-06-04 21:09:02
categories: Tech
tags:
  - Vue
  - Nginx
---
之前用vue-cli搭建了一个ICD编码和电子病历信息抽取的前端小工具，这里讲一下如何部署在服务器上
<!-- more -->

1. 在本地项目根目录下运行  
`npm run build`  
2. 在ubuntu16.04服务器上用apt-get install nginx安装，这里遇到了一些问题，安装完以后报错无法启动，发现是因为服务器不支持IPV6，需要在配置文件里将相应的行注释掉
3. 把dist里的文件和index.html打包上传至服务器上nginx目录下，我这里的/var/www/，原本的nginx的root路径是/var/www/html，这里修改为/var/www/frontend
4. 浏览器访问http://server_ip/即可

Reference: [知乎](https://www.zhihu.com/question/46630687/answer/102284339)
