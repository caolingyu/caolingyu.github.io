---
title: NEXT主题的一处小瑕疵
date: 2017-05-22 22:04:57
categories: Tech
tags:
  - NEXT
  - Hexo  

---
在使用NEXT主题中发现的一处小瑕疵，研究以后发现了解决方法
<!-- more -->
# 问题

昨天把Hexo部署好并且安装了NEXT主题，整体感觉非常棒。然而今天想测试一下标签和分类功能的时候，发现了一处小bug。如下图所示：

![Pic](http://caolingyu.me/images/post3_1.png)

强迫症的我表示完全不能忍，遂百度谷歌一通搜索，然而无果。

于是来到了NEXT的github仓库，想在issue里看一下有没有人提问，万万没想到竟然没有人提出类似的问题！莫非这是一个新版本更新造成的新bug？

再看了几个使用同样主题的博客以后，我发现他们均未出现此问题，万般无奈之下，只能开始琢磨源代码！

# 解决方案

```swig
{% block title %}{{ __('title.category') }}: {{ page.category }} | {{ config.title }}{% endblock %}

{% block content %}

  <section id="posts" class="posts-collapse">
    <div class="collection-title">
      <{% if theme.seo %}h2{% else %}h1{% endif %}>{#
      #}{{ page.category }}{#
      #}<small>{{  __('title.category')  }}</small>
      </{% if theme.seo %}h2{% else %}h1{% endif %}>
    </div>
```

以上代码来自**layout/category.swig**这个文件。同一目录下的**tag.swig**也包含类似的代码。问题就在于这段代码里的h1和h2。接下来找到**source/css/_common/components/post/post-collapse.styl**这个文件，发现里面含有`h2 { margin-left: 20px; }`这行代码，但是并没有定义h1。我想这应该就是造成这个问题的原因。于是我加入了`h1 { margin-left: 20px; }`。果然问题迎刃而解！如下图：

![Pic](http://caolingyu.me/images/post3_2.png)



