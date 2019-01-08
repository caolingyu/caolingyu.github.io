---
title: elasticsearch--从安装到使用
date: 2018-06-14 17:48:15
categories: Tech
tags:
  - ElasticSearch
---

最近在做一个实体链接的项目，主要是先用命名实体识别的模型去识别文本中的特定实体，然后再将识别出来的实体链接到知识图谱中对应的节点。之所以要这么做是因为往往识别出来的实体名字并不和图谱中的节点完全对应。关于实体链接的具体细节在这里不多赘述，因为不是本文的重点，大致就是对每个识别出的实体从图谱中选出一些候选节点，计算相似度然后选最相似的。  

这里主要说一下挑选候选节点这一步，之所以要用到elasticsearch，是因为我们的图谱目前还不支持模糊搜索，而es的match提供了很好的模糊搜索功能，并且还能给每个结果打分。

我的系统是macOS 10.13.5，安装的es版本是5.6.4。在macOS上有两种主流的安装方法，一种是从官网直接下载压缩包，另一种是用homebrew安装，本文使用的是前一种方法。  
首先去[官网](https://www.elastic.co/downloads/past-releases/elasticsearch-5-6-4)下载对应版本，下载解压缩完以后我把放在用户根目录下，所以路径是~/elasticsearch-5.6.4/，这时候其实已经可以运行了，执行elasticsearch-5.6.4/bin/elasticsearch就可以启动es。但是有一个问题，es默认的analyzer对中文的分词不是很友好，往往会在搜索的时候把中文分成一个个字，这显然不是我们想要的，好在有ik插件，解决了这个问题。安装ik插件也有两种方法，一种是手动从官网下载安装包放到指定文件夹，另一种可以用elasticsearch-plugin命令来安装（需要安装5.5.1版本以上的es）  
``./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v5.6.4/elasticsearch-analysis-ik-5.6.4.zip``  
因为我安装的es高于5.5.1，所以我采用了这种方法，很方便。具体可以参考[官方repo](https://github.com/medcl/elasticsearch-analysis-ik#install)

接下来就是es的使用了，首先了解一下es中的索引，它是ES中的一个存储类型，与数据库类似，内部包含类型字段，类型中包含各种文档。如果和关系型数据库进行类比的话，索引就是数据库，类型就是数据库中的表，文档就是每张表中的每一行记录。  
下面介绍一些常用的操作  

- 查看所有索引  
``curl 'localhost:9200/_cat/indices?v'``  

- 创建一个名为country的索引  
``curl -XPUT 'localhost:9200/country?pretty'``  

- 在country中设置一个名为city的类型，并写入一条数据  
```
curl -XPUT 'localhost:9200/country/city/1?pretty' -d '
{
  "name": "London"
}'
```
	
- 查询  
```
curl -XGET 'localhost:9200/country/city/1?pretty'
{
  "_index" : "country",
  "_type" : "city",
  "_id" : "1",
  "_version" : 1,
  "found" : true, "_source" : { "name": "London" }
}
```

- 删除索引  
``curl -XDELETE 'localhost:9200/customer?pretty'``

另外如果需要在python中使用es，可以参考以下文章  
- [python操作Elasticsearch (一、例子)](https://www.cnblogs.com/yxpblog/p/5141738.html)  
- [Elasticsearch使用备忘](https://www.cnblogs.com/cswuyg/p/5651620.html)  
- [基于Python操作ElasticSearch](https://blog.csdn.net/YHYR_YCY/article/details/78882011)  
还有一篇讲解es中的映射和分析的，我觉得写的也不错  
- [ElasticSearch映射和分析](https://blog.csdn.net/hzrandd/article/details/47128895)