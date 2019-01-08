---
title: Win10+Ubuntu双系统卸载Ubuntu
date: 2017-05-24 20:33:25
categories: Tech
tags: 
  - Ubuntu
  - Windows10
  - 双系统
---
安装Windows10和Ubuntu双系统以后卸载Ubuntu的方法
<!-- more -->
之前跑Machine translation深度学习训练时候在我平时打游戏的独显笔记本上安装了Ubuntu双系统，用的是UEFI的启动方法。

跑完任务以后发现Ubuntu出了点问题...于是决定卸载了。由于遇到了一些坑，所以在这里记录一下。

1. 首先打开windows的磁盘工具将Ubuntu的四个分区中能格式化的三个全部格式化，剩下的那个就是比较难搞的UEFI启动项。
2. 接下来按win键+R，在运行窗口里输入Diskpart。
3. 进入命令行以后首先输入`list disk`，就会看到可选的磁盘，由于我将Ubuntu装在磁盘1上，所以输入`select disk 1`选择磁盘1。接下来输入`list partition`来显示这个磁盘有哪些分区，要删除的分区应该可以根据容量大小判断出来，于是输入`select partition X`。最后输入`delete partition override`从而删除该分区。
4. 删除了分区以后可以再打开磁盘工具进行确认。然后使用easyUEFI软件删除Ubuntu的启动项即可。

--

Reference: [CSDN博客](http://blog.csdn.net/qq_28057541/article/details/51723914) 






