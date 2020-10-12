---
title: mongodb常用的数据库操作命令
date: 2019-08-06 23:31:51
tags: ["mongodb","nodejs"]
---

#### mongodb作为NoSQL中一个比较流行和使用广泛的数据库，因为是非关系型数据库，所以mongodb的查询并不是使用sql语句。

#### ***下面简单介绍一下mongodb操作数据库的常用命令：***

```bash
#首先打开mongodb服务，然后进入mongo shell
$ sudo systemctl start mongod
$ mongo
>
#这里简单介绍一下数据库的打开和关闭，这里介绍两种方式：
> service mongod start	#打开mongodb数据库
> service mongod stop	#关闭mongodb数据库
> sudo systemctl start mongod	#打开数据库
> sudo systemctl stop mongod	#关闭数据库
```

```bash
#输出可用的命令列表：
> help
#输出数据库服务器上面数据库的名称到连接的控制台上【默认是localhost:27017】，也就是显示数据库列表：
> show dbs
```

```bash
#切换到某个数据库【db_name是数据库的名称】：
> use db_name
#创建数据库【同切换其实一样，只是如果不存在切换的数据库就是创建了】：
> use dataBase_name
#删除数据库：
> db.dropDatabase()	#删除当前选择的数据库
```

```bash
#mongodb创建集合：
> use db_name	#选择要创建集合的数据库
> db.createCollection(name, options)
>#参数：name指的是集合名称，options是可选参数，是指定内存大小和索引的选项
>
#删除集合：
> db.collection_name.drop() ##这种方式在一些复杂的集合名称使用时会报错
#删除集合，还可以使用下面这种：
> db.getCollection("collection_name").drop();
```

```bash
#显示当前数据库集合的列表：
> show collections
#查找集合中所有匹配条件的数据：
> db.collection_name.find(query)
#查找集合中一条匹配条件的数据【返回第一条匹配的数据】：
> db.collection_name.findOne(query)
#在collection_name集合中插入一条数据：
> db.collection_name.insert(document)
#保存一条数据到collection_name集合中[简写为：upsert(no_id)或者insert(with_id)]：
> db.collection_name.save(document)
#用data数据更新匹配条件的collection_name集合中的数据：
> db.collection_name.update(query, {$set: data})
#删除collection_name集合中所有匹配条件的数据：
> db.collection_name.remove(query)
#输出参数文档：
>printjson(document)
```

```bash
#还可以编写javaScript脚本来操作脚本，比如存储变量或赋值等：
> var a = db.collection_name.findOne()
> printjson(a)
> a.text = 'hello world!'
> printjson(a)
> db.collection_name.save(a)
>#这样就修改了a对应的这条数据，这里是增加了text键对应"hello world!"的值
```

```bash
#创建数据库集合索引：
> db.collection_name.ensureIndex({KEY:1})	#这里的KEY值是你要创建的索引字段，1为升序，-1为降序。
```

#### 索引还有复合索引的用法，也就是索引有多个。

* 集合中索引最多是64个
* 索引名长度不可超过125个字符
* 一个复合索引最多可以有31个字段

```bash
#mongodb聚合【aggregate() 方法】：
> db.collection_name.aggregate(options)
```

#### 聚合的有关参数表达式：

{% asset_img options.png%}

#### *mongodb数据库操作的基本简单命令大概就是以上了...*

