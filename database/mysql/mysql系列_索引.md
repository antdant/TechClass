## 什么是索引 ？

首先我们来看下索引的概念，索引（在MySQL中也叫做“键 - key”）是存储引擎用于快速找到记录的一种数据结构。这是索引的基本功能，除此之外，索引对于良好的性能非常关键。尤其是当表中的数据量越来越大时，索引对性能的影响愈发重要。

## 索引类型

在MySQL中索引是在**存储引擎**层实现的，所以我们说到索引都是依赖存储引擎，存储引擎不同对索引的实现方式也不同，来看看有哪些MySQL存储引擎。

### B-Tree索引

### hash索引

### R-Tree索引

### 全文索引

## InnoDB索引原理

### 索引数据结构

### B+ Tree 结构



### 主键索引和辅助索引

https://www.jianshu.com/p/23524cc57ca4

主键是聚集索引
唯一索引、普通索引、前缀索引等都是二级索引（辅助索引） 



## Reference

[图解 MySQL 索引：B-树、B+树，终于搞清楚了！](https://mp.weixin.qq.com/s?__biz=MzI3ODcxMzQzMw==&mid=2247494310&idx=2&sn=2a5632199bbd99e6313b19b9d24b74d0&chksm=eb506f90dc27e68621df63556b8096109dd1feec2c5201be9ea9fe98cab181426e1737fe3b93&mpshare=1&scene=1&srcid=0909TC0w00EdDFMFKNprfyIW&sharer_sharetime=1599664422060&sharer_shareid=c71e0673fbaa15e3038063afecc3a033&rd2werd=1#wechat_redirect)

[索引很难么？带你从头到尾捋一遍MySQL索引结构，不信你学不会！](https://mp.weixin.qq.com/s?__biz=MzI4Njc5NjM1NQ==&mid=2247490706&idx=1&sn=d98cd10845923c2bf5d933a8fd963cb5&chksm=ebd623bedca1aaa87256f9729192d024897ba70bc38a0abc314cd59b1a1349c52ec33f1074a1&mpshare=1&scene=1&srcid=0909afLNdmybwIfqAkf4DTIG&sharer_sharetime=1599665154874&sharer_shareid=c71e0673fbaa15e3038063afecc3a033&rd2werd=1#wechat_redirect)

