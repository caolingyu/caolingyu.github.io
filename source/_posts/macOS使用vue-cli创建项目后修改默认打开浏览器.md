---
title: macOS使用vue-cli创建项目后修改默认打开浏览器
date: 2018-04-10 14:16:54
categories: Tech
tags:
  - macOS
  - Vue
---
用vue-cli创建项目以后会用系统默认浏览器打开，我在mac上用safari作日常浏览器，开发调试一般用chrome，这里介绍一个修改npm run dev默认打开浏览器的方法
<!-- more -->
**打开项目文件夹中node_modules/webpack-dev-server/bin中的webpack-dev-server.js文件，找到openOptions，默认为{}，在其中添加app: 'google chrome'。**