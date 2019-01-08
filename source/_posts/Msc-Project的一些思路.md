---
title: Msc Project的一些思路
date: 2017-05-23 21:11:09
categories: Misc
tags:
  - Python
  - PyQt
---
这篇文章主要讲一下我研究生毕业论文的思路
<!-- more -->
期末考试结束，研究生生涯就剩下一个项目和论文了。

项目的题目是*Workflows for analysis of neuronal high density multielectrode array recordings*。听起来很高大上，但是实际上只需要将现有的一个GUI进行修改。

[项目repo](https://github.com/caolingyu/herding-spikes)

在和导师聊了两次以后，有了一个大致的思路...

- 原先是读取cluster过的数据，需要在GUI中集成clustering的功能，以便直接读取原始数据

- 加入对数据clustering过程中参数的设置，以及添加subsetting功能，以便对原始数据的某一子集进行clustering

- 对主视图的某一部分选中并重新clustering

- 对PCA和waveform显示窗口进行改进

