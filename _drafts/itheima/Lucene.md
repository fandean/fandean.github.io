# Lucene

此为读书笔记。

## 数据分类

**结构化数据**：指具有固定格式或有限长度的数据，如数据库行数据：存在数据库中，可以用二维表结构来逻辑表达实现的数据

**非结构化数据**：指不定长度或者无固定格式的数据，如邮件、word文档、音频、超音频等

**半结构化数据**：对于这种数据可以按照结构化数据来处理，也可以提取纯文本按照非结构化数据来处理，如xml数据



对于非结构化的数据常用的检索方式有**顺序扫描**、**索引（Index）**

对于非结构化数据采用索引检索又可以说是全文检索（Full-Text-Search），在索引过程中，我大致给它分成两大步骤：

- 索引创建（Indexing）：将结构化数据或非结构化数据提取信息创建索引的过程。比如可以将文件系统数据、数据库数据、web数据等，通过索引的创建，形成最终的索引文件

- 搜索索引（Search）根据用户的查询条件，检索已创建的索引，返回查询结果的过程



> 老师上课时详细讲解了一下 索引的概念




## 索引

### 倒排索引（反向索引）

想象一下查字典的过程： 通过音节索引或者部首索引  查找  到想要查找的汉字所在的页码数 --> 翻到对应的页码，查看该汉字的解释。



这种由字符串到文件的映射是文件到字符串映射的反向过程，我们就称这种信息为**反向索引**。 ？？



![](https://raw.githubusercontent.com/fandean/images/master/PicGo/%E5%80%92%E6%8E%92%E8%A1%A8.jpg)



上图中左半部分保存的信息，我们一般称为**字典**，左侧每一个字符串指向右侧的文档链接，此文档链表称为**倒排表**。 

**下面的示例有助于理解此图。**



### 如何创建索引



步骤：

1. 要检索的数据 （Document）
2. 分词技术（Analyzer）
3. 索引组建 （Indexer）



![](https://raw.githubusercontent.com/fandean/images/master/PicGo/20180912113236.png)





第一步数据：Document事例数据：

```
你好！我是小李。
中国在哪里？
你是谁？
lucene基础知识学习课程。
你在中石油上学？
中石油在哪里？
```



第二步：分词技术，这里采用StandarAnalyzer(标准分词)

```
你|好|我|是|小|李|
中|国|在|哪|里|
你|是|谁|
lucene|基|础|知|识|学|习|课|程|
你|在|中|石|油|上|学|
中|石|油|在|哪|里|
```

第三步之：索引创建字典：



![](https://raw.githubusercontent.com/fandean/images/master/PicGo/20180912114102.png)

> Term :  词， 词语



第三步之：索引组建合并词成倒排表：

![](https://raw.githubusercontent.com/fandean/images/master/PicGo/20180912114238.png)

分析上表，`term` 对应之前图示中的**字典**， `id` 对应 **倒排表**。

其中`id` 列 中的 `1>3>5` 表示第 1，3，5 行的源数据中包含此 分词。





### 如何检索

四步曲：**获取检索词（KeyWords**）、**分词技术（Analyzer）**、**检索索引（Aearch）**、**返回结果列表**

![](https://raw.githubusercontent.com/fandean/images/master/PicGo/20180912141635.png)



第一步：KeyWord事例数据

```
中石油
```



第二步：分词技术（因为创建索引的时候，采用的是标准分词，索引在搜索的过程，也应该采用该分词技术）

```
中|石|油|
```



第三步：检索索引搜索记录

![](https://raw.githubusercontent.com/fandean/images/master/PicGo/20180912141827.png)



第四步：返回结果列表

```
中石油在哪里？
你在中石油上学？
```











Lucene 5.3 <=  jdk 8



lucene 与 solr 







 update 操作： 先删除，后增加



Document 对象， 行，类似于文档型数据库。



文档类似于关系数据库中的行。多个键及其关联的值有序的放置在一起便是文档。**在JS中，文档表示为对象**。

每个文档都有一个特殊的键`_id`，它在文档所处的集合中是唯一的。







## 学习资料



- [Lucene案例开发 · 看云](https://www.kancloud.cn/digest/lulei-lucene "Lucene案例开发 · 看云") 强烈推荐
- [Basic Concepts - Lucene Tutorial.com](http://www.lucenetutorial.com/basic-concepts.html "Basic Concepts - Lucene Tutorial.com")













