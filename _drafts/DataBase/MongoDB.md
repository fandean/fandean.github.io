## MongoDB

MongoDB是面向文档的数据库，而非关系型数据库。它扩展了关系型数据库的众多有用功能，如辅助查询、范围查询和排序。

它将原来的行的概念换成更加灵活的文档模型。它没有模式：文档的键不会事先定义也不会固定不变。

MongoDB 将数据存储为一个文档，数据结构由键值(key=>value)对组成。MongoDB 文档类似于 JSON 对象。字段值可以包含其他文档，数组及文档数组。

有些关系型数据库的常见功能MongoDB并不具备，比如联接(join)和复杂的多行事务。

MongoDB 的扩展性强，其采用的面向文档的数据模型使其可以自动在多台服务器之间分割数据。

MongoDB性能优越。它将内存管理工作交由操作系统处理；它利用查询优化器记住执行查询最高效的方式；它利用预分配数据文件的方式(用空间)换取性能的稳定。

MongoDB的管理理念就是尽可能的让服务器自动配置，简化数据库的管理。比如如果主服务器挂掉，它会自动切换到备份服务器上，并且将备份服务器提升为活跃服务器。



> **NoSQL简介**      
> NoSQL(NoSQL = Not Only SQL )，意即"不仅仅是SQL"。但事实上很多NoSQL数据库都放弃了对 SQL语言的支持。



## MongoDB安装启动和卸载

[Install MongoDB Community Edition ](https://docs.mongodb.com/manual/administration/install-community/ "Install MongoDB Community Edition — MongoDB Manual 3.4")

[How to Install MongoDB on Ubuntu 16.04 - DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04 )

[How to Install and Configure MongoDB on Ubuntu 16.04](https://www.howtoforge.com/tutorial/install-mongodb-on-ubuntu-16.04/ "How to Install and Configure MongoDB on Ubuntu 16.04")



开启mongod：

```shell
sudo service mongod start
```

进入mongo shell：

```shell
mongo
```

列出数据库：

```shell
show dbs
```

显示当前数据库对象：

```
db
```

默认是 test 。

切换数据库：

```shell
use <database>
```

停止 mongod：

```
sudo service mongod stop
```

或者：

```
# 切换到admin数据库（让自己具有管理员权限）
use admin
db.shutdownServer()
```



> 刚安装的mongodb并没有开启用户权限验证；所以进入时不需要认证。



## MongoDB的基本概念

在mongodb中基本的概念是文档、集合、数据库。

| SQL术语/概念    | MongoDB术语/概念 | 解释/说明                   |
| ----------- | ------------ | ----------------------- |
| database    | database     | 数据库                     |
| table       | collection   | 数据库表/集合                 |
| row         | document     | 数据记录行/文档                |
| column      | field        | 数据字段/域                  |
| index       | index        | 索引                      |
| table joins |              | 表连接,MongoDB不支持          |
| primary key | primary key  | 主键,MongoDB自动将_id字段设置为主键 |



### 文档

文档类似于关系数据库中的行。多个键及其关联的值有序的放置在一起便是文档。**在JS中，文档表示为对象**。

每个文档都有一个特殊的键`_id`，它在文档所处的集合中是唯一的。



**几个重要的概念：**

* 文档中的键/值对是**有序的**。

* 文档的键是字符串。一般情况键可以使用UTF-8字符。

  * 键不能有`\0`空字符。它是用来表示键的结尾。
  * `.`和`$`只有在特定环境才能使用
  * 以`_`开头的键是保留的

* MongoDB不但**区分类型**，也**区分大小写**。下面是两组不同的文档：

  ```javascript
  {"foo":3}
  {"foo":"3"}
  ```

  ```javascript
  {"foo":3}
  {"Foo":3}
  ```

  ​

* MongoDB的文档**不能有重复的键**。





### 集合

集合可以被看作没有模式的表。



**子集合：**

组织集合的一种惯例是使用 `.` 字符分开的命名空间划分的**子集合**。比如：

blog.post和blog.authors，这样做只是了使组织结构更好些，也就是说blog这个集合（这里根本就不需要存在）及其子集合没有任何关系。



### 数据库

一个MongoDB实例可以承载多个数据库。不同的数据库存放在不同的文件中

要记住数据库名最终会变成文件系统里的文件，所以数据库名必须遵守一些约定。



保留的特殊数据库：

* admin：从权限角度上看，这是 root 数据库。
* local：这个数据库永远不会被复制，可以用来存储限于本地服务器的任意集合。
* config：但Mongo用于分片设置时，config数据库在内部使用，用于保存分片的相关信息。



命名空间：把数据库的名字放到集合名前面，得到的集合的完全限定名称。





### 数据类型

MongoDB的文档类似于JSON，在概念上和JavaScript中的对象神似。MongoDB在保留JSON基本的键/值对特性的基础上，添加了其它一些数据类型。在不同的编程语言下这些类型表示有些许差异。







## 数据库管理

默认数据目录 `/data/db`，并使用27017端口。它还会启动一个非常基本的http服务器，监听数字比主端口号高 1000 的端口，比如 28017 端口。



### MongoDB Shell

MongoDB自带一个 JavaScript shell，可以从命令行与MongoDB实例交互。它也是一个完备的JS解释器，可以运行任何JS程序。

开启的时候，shell会连接到MongoDB服务器的 test 数据库，并将这个数据库连接**赋值给全局变量 db** 。这个变量是通过 shell 访问 MongoDB的主要入口点。

shell还提供了一些语法糖，比如选择数据库的 `usr dbName` ，执行该操作后 db 变量的值也会发生改变。

```sql
# 运行 mongo 启动 shell
mongo

# 列出数据库
show dbs
# 切换数据库，如果该数据库不存在则创建该数据库
use imooc
# 删除数据库
db.dropDatabase()
```





## 增删改查











## 学习资料

《MongoDB权威指南》 

[MongoDB 教程 - 菜鸟教程](http://www.runoob.com/mongodb/mongodb-tutorial.html "MongoDB 教程 - 菜鸟教程")

官方手册：[The MongoDB  Manual ](https://docs.mongodb.com/manual/)

[MongoDB中文社区 - 中文社区](http://www.mongoing.com/)

[MongoDB中文网](http://www.mongodb.org.cn/)



[Mongodb最佳实践-麦子学院](http://www.maiziedu.com/course/395/ "Mongodb最佳实践-Mongodb最佳实践教程-麦子学院")

[MongoDB基础教程-慕课网课程](http://www.imooc.com/course/list?c=mongodb)





