+++
title = 'Java基础面试题（转载自学精灵）'

categories=["java"]

tags=["java学习"]

draft=false

date = 2024-06-06T11:12:50+08:00

+++

## Java基础

**基础**

Java中==和equals有什么区别？（难度：★ 频率：★★★）

[Java中==和equals有什么区别](https://learn.skyofit.com/archives/2224)

**String**

String, StringBuffer, StringBuilder区别（难度：★ 频率：★★★）

[Java-String, StringBuffer, StringBuilder的区别](https://learn.skyofit.com/archives/62)

String对象数目（难度：★★★ 频率：★）

[Java–创建对象的个数及其原理](https://learn.skyofit.com/archives/196)

intern方法的作用（难度：★★★ 频率：★）

[Java之String系列-intern方法的作用及原理](https://learn.skyofit.com/archives/211)

如何修改String对象的数据？（难度：★★★ 频率：★★）

[Java-String不可变的含义、原因、好处](https://learn.skyofit.com/archives/266)

**static**

static的5种用法（难度：★★ 频率：★）

[Java-static-用法/使用位置/实例](https://learn.skyofit.com/archives/277)

为什么静态方法不能调用非静态方法和变量？（难度：★★★ 频率：★★★）

与类加载顺序有关，加载静态方法时，非静态的未初始化。见：[JVM原理-类加载过程(有实例)](https://learn.skyofit.com/archives/406)

**异常**

异常有哪两大类？Throwable和Exception是什么关系？常见的RuntimeException有哪些？常见的Error有哪些？（难度：★★ 频率：★★★★）

[Java-异常/Exception-类型/原理](https://learn.skyofit.com/archives/290)

catch里return了，finally是否执行？（难度：★★ 频率：★）

[Java-异常/Exception-try/catch/finally的return顺序](https://learn.skyofit.com/archives/297)

**IO**

字节流与字符流区别？（难度：★★ 频率：★★）

[Java-IO-字节流与字符流的区别](https://learn.skyofit.com/archives/299)

BIO, NIO, AIO 区别？（难度：★★★ 频率：★）

[Java-BIO、NIO、AIO-区别/使用/实例](https://learn.skyofit.com/archives/301)

**JDK8**

JDK8新特性（难度：★★ 频率：★★）

接口允许default和static；lambda；stream；时间新API（LocalDateTime等）CompletableFuture；等

JDK8接口的default和static（难度：★★ 频率：★）

[Java-接口(JDK8新特性等)-详解/实例](https://learn.skyofit.com/archives/303)

JDK8 Stream API 流操作包括哪些部分？项目中怎么用的Stream？（难度：★★ 频率：★）

[Java-Stream(流)-使用/实例/流操作](https://learn.skyofit.com/archives/306)

**语法**

项目中对泛型的使用（难度：★★ 频率：★★）

[Java-泛型的应用](https://learn.skyofit.com/archives/349)

接口与抽象类的区别？（难度：★★ 频率：★）

[Java-接口与抽象类的区别](https://learn.skyofit.com/archives/351)

**反射**

Java反射：forName和classLoader的区别（难度：★★★ 频率：★）

[Java-通过反射实例化对象](https://learn.skyofit.com/archives/355)

反射机制中可以获取private成员的值吗？（难度：★★★ 频率：★）

- 可以。法1：通过Field类提供的set()和get()方法 法2：通过setter和getter
- 见：[Java反射系列-应用](https://learn.skyofit.com/archives/2673#修改属性)

**其他**

拆箱与装箱（难度：★ 频率：★）

[Java-自动拆箱/装箱/实例化顺序/缓存](https://learn.skyofit.com/archives/358)

## 集合

**List**

List与Set的区别（难度：★ 频率：★）

[ArrayList与LinkedList以及List与数组、Set的区别](https://learn.skyofit.com/archives/361)

ArrayList与LinkedList异同点？（难度：★ 频率：★★）

[ArrayList与LinkedList以及List与数组、Set的区别](https://learn.skyofit.com/archives/361)

List与数组的区别？（难度：★ 频率：★）

[ArrayList与LinkedList以及List与数组、Set的区别](https://learn.skyofit.com/archives/361)

ArrayList是否线程安全？如何线程安全地操作ArrayList？（难度：★★★ 频率：★★★★★）

[Java-ArrayList保证线程安全的方法](https://learn.skyofit.com/archives/363)

ArrayList扩容机制（难度：★★★ 频率：★★★★）

[Java-ArrayList扩容的原理](https://learn.skyofit.com/archives/368)

List.subList的坑？（难度：★★ 频率：★）

[Java的List之坑-subList与原始List相互影响](https://learn.skyofit.com/archives/370)

List如何安全删除（难度：★★ 频率：★）

[Java-安全删除的方法](https://learn.skyofit.com/archives/372)

List如何去重？（难度：★ 频率：★★）

stream，或：[Java-去重的方法](https://learn.skyofit.com/archives/374)

List如何实现排序（难度：★ 频率：★★）

stream，或：[Java-排序的方法](https://learn.skyofit.com/archives/376)

为什么引入迭代器？（难度：★★ 频率：★）

[Java类集-为什么引入迭代器](https://learn.skyofit.com/archives/378)

**Map**

HashMap、TreeMap、LinkedHashMap的区别？（难度：★★ 频率：★★★★★）

[HashMap,TreeMap,LinkedHashMap的区别](https://learn.skyofit.com/archives/380)

JDK8的HashMap的改变？（难度：★★ 频率：★★★★）

[Java-JDK7与JDK8的HashMap的区别](https://learn.skyofit.com/archives/382)

HashMap数据结构、哈希冲突解决方法（难度：★★★ 频率：★★★★）

[Java-HashMap的底层原理](https://learn.skyofit.com/archives/387)

[hash冲突的4种解决方案](https://learn.skyofit.com/archives/392)

HashMap扩容的原理（难度：★★★ 频率：★★★★）

[Java-HashMap扩容的原理](https://learn.skyofit.com/archives/394)

HashMap为什么线程不安全？如何线程安全地操作？（难度：★★★ 频率：★★★★★）

[Java-HashMap保证线程安全的方法](https://learn.skyofit.com/archives/396)

ConcurrentHashMap的原理？JDK8有什么改变？（难度：★★★ 频率：★★★★★）

[Java-ConcurrentHashMap的原理](https://learn.skyofit.com/archives/384)

HashMap和HashSet的区别及其实现原理？（难度：★★ 频率：★）

- HashMap：将key.hashCode()作为hash值存放，将value直接作为value。
- HashSet：调用HashMap的put方法；将key.hashCode()作为hash值存放，将HashSet类的final变量PRESENT作为value。

HashMap如果使用对象最为key，要注意什么？（难度：★★ 频率：★）

- 重写hashCode和equals。

对象比较为什么重写hashCode和equals？（难度：★★ 频率：★）

- 重写equals方法时需要重写hashCode方法，主要是针对Map、Set等集合类型的使用；
  - a: Map、Set等集合类型存放的对象必须是唯一的；
  - b: 集合类判断两个对象是否相等，是先判断HashCode是否相等，如果HashCode返回TRUE，还要再判断equals返回值是否ture，只有两者都返回ture，才认为该两个对象是相等的。

## JVM

**运行时数据区**

运行时数据区是怎样的？线程安全（即线程私有）的有哪些？（难度：★★ 频率：★★★★）

[JVM原理-运行时数据区域](https://learn.skyofit.com/archives/403)

对象实例、类信息、常量、静态变量分别在运行时数据区的哪个位置？（难度：★★ 频率：★★）

[JVM原理-运行时数据区域](https://learn.skyofit.com/archives/403)

**类加载**

Java类加载流程？初始化流程？（难度：★★ 频率：★★★★★）

[JVM原理-类加载过程(有实例)](https://learn.skyofit.com/archives/406)

JVM双亲委派模型（难度：★★★ 频率：★）

[JVM原理-双亲委派模型](https://learn.skyofit.com/archives/409)

**内存泄露**

Java内存泄露什么时候会发生？（难度：★★ 频率：★★）

[Java-内存泄露的原因及解决方案(大全)](https://learn.skyofit.com/archives/1337)

为什么内部类持有外部类可能内存泄露？如何解决？（难度：★★ 频率：★）

[Java-内部类持有外部类导致内存泄露的原因和解决方案](https://learn.skyofit.com/archives/412)

为什么ThreadLocal会导致内存泄露？如何解决？（难度：★★★ 频率：★★）

[Java-ThreadLocal导致内存泄露的原因和解决方案](https://learn.skyofit.com/archives/439)

**垃圾回收**

JDK8垃圾回收器的流程？（难度：★★★ 频率：★★★★）

[JVM-内存模型/垃圾回收流程](https://learn.skyofit.com/archives/441)

引用类型及其含义（难度：★★ 频率：★★★）

[Java引用类型(强引用、软引用、弱引用、虚引用)的区别](https://learn.skyofit.com/archives/446)

finalize方法做什么用的？（难度：★ 频率：★）

- 垃圾回收时会调用此方法

可以作为GC.Roots的对象有哪些？（难度：★★★ 频率：★）

[JVM-可作为GC Roots的对象](https://learn.skyofit.com/archives/453)

调用System.gc()会立刻垃圾回收吗？（难度：★★ 频率：★）

[JVM-Java垃圾回收的原理与触发时机](https://learn.skyofit.com/archives/456)

Minor GC和Full GC的触发时机。（难度：★★★ 频率：★★）

[JVM-Java垃圾回收的原理与触发时机](https://learn.skyofit.com/archives/456)

频繁Full GC如何排查（难度：★★★★ 频率：★）

[Java线上问题排查-系统问题排查的方法/步骤](https://learn.skyofit.com/archives/459)

JDK默认的垃圾回收器是什么？（难度：★★ 频率：★）

[JVM-垃圾回收器的详解/对比](https://learn.skyofit.com/archives/462)

CMS和G1区别（难度：★★★ 频率：★★★）

[JVM-CMS和G1垃圾回收器的区别和执行流程](https://learn.skyofit.com/archives/465)

CMS与其他老年代垃圾回收器的区别？（难度：★★★ 频率：★）

[JVM-垃圾回收器的详解/对比](https://learn.skyofit.com/archives/462)

**JVM调优**

JVM通常设置哪些参数来调优？（难度：★★ 频率：★★★★）

[JVM调优系列-常用的设置](https://learn.skyofit.com/archives/475)

**其他**

怎么分配堆外内存（难度：★★ 频率：★）

[Java堆外内存–使用/作用](https://learn.skyofit.com/archives/478)

## 多线程

**综合**

 项目中哪些地方用到了多线程？（难度：★★★ 频率：★★★★★）

- 定时任务。  比如：定时处理数据进行统计等
- 异步处理。  比如：发邮件， 记录日志， 发短信等。比如注册成功后发激活邮件
- 批量处理，缩短响应时间。比如：[SpringBoot-多线程处理](https://learn.skyofit.com/archives/481)

线程的安全性问题体现在哪些方面？（难度：★★ 频率：★）

[Java多线程-内存模型(JMM)-详解](https://learn.skyofit.com/archives/503)

死锁产生的条件？（难度：★★ 频率：★）

[Java多线程-基础知识](https://learn.skyofit.com/archives/506)

i++是否线程安全？（难度：★ 频率：★）

- 不是线程安全的。要线程安全可以用java.util.concurrent.atomic

JMM内存结构（难度：★★★ 频率：★★）

[Java多线程-内存模型(JMM)-详解](https://learn.skyofit.com/archives/503)

**synchronized**

synchronized用于静态方法与普通方法有区别吗？（难度：★★ 频率：★★）

[Java-synchronized的使用](https://learn.skyofit.com/archives/508)

synchronized锁的升级是怎样的？（难度：★★★ 频率：★）

[Java-synchronized之锁的升级](https://learn.skyofit.com/archives/510)

**类库**

SimpleDateFormat线程安全吗？怎么保证线程安全？（难度：★★★ 频率：★★★）

[SimpleDateFormat-线程安全的操作方法(有实例)](https://learn.skyofit.com/archives/353)

**线程池**

线程池缺点（难度：★★ 频率：★★）

[Java-为什么使用线程池？优缺点是什么？](https://learn.skyofit.com/archives/514)

线程池有哪些参数？（难度：★★ 频率：★★★★★）

[Java线程池-核心参数/大小设置/使用示例](https://learn.skyofit.com/archives/488)

CPU密集与IO密集的场景如何设置线程池参数？（难度：★★★ 频率：★★★）

[Java线程池-核心参数/大小设置/使用示例](https://learn.skyofit.com/archives/488)

线程池有哪几种？它们分别对应什么队列？（难度：★★ 频率：★★★）

[Java线程池-种类(Executors的用法)](https://learn.skyofit.com/archives/516)

[Java-阻塞队列(BlockingQueue)的用法(有实例)](https://learn.skyofit.com/archives/523)

什么时候触发最大线程条件？（难度：★★ 频率：★★★★★）

[Java-线程池的原理(执行流程/状态转换)](https://learn.skyofit.com/archives/531)

线程池拒绝策略有哪些？默认是哪个？（难度：★★ 频率：★★★★）

[Java线程池-饱和策略(拒绝策略)的使用(有实例)](https://learn.skyofit.com/archives/490)

线程池里的异常时如何处理的？（难度：★★ 频率：★）

[Java-线程池全局异常处理的方法(有实例)](https://learn.skyofit.com/archives/537)

**JUC**

ReentrantLock显著缺点？（难度：★★★ 频率：★★）

[Java-ReentrantLock的用法和原理](https://learn.skyofit.com/archives/539)

CAS和AQS了解吗？原理是什么（难度：★★★ 频率：★★）

[Java-CAS的原理和优缺点](https://learn.skyofit.com/archives/544)

[Java-AQS的原理](https://learn.skyofit.com/archives/546)

synchronized与ReentrantLock区别？（难度：★★ 频率：★★）

[synchronized与volatile、ReentrantLock的区别](https://learn.skyofit.com/archives/549)

有哪些原子类？用过哪个？（难度：★★★ 频率：★）

[Java-原子类(atomic)的用法(有实例)](https://learn.skyofit.com/archives/551)

项目里用了哪些锁？（难度：★★★ 频率：★★★）

- 单体项目里用到了ReentrantLock、synchronized；
- 单例模式里用到了synchronized

JDK8新增的异步编程了解吗？（难度：★★★ 频率：★）

[Java异步-CompletableFuture-实例](https://learn.skyofit.com/archives/554)

多线程顺序交替执行的方法（有三个线程A,B,C，依次打印出A,B,C）（难度：★★★ 频率：★）

- 方案1：
  - [Java-使用阻塞队列实现顺序消费-方法/实例](https://learn.skyofit.com/archives/484)
- 方案2：模拟阻塞队列
  - 使用Object的wait(), notify()，使用一个互斥锁。

## MySQL

**综合问题**

MyISAM与InnoDB区别（难度：★ 频率：★★★★）

[MySQL存储引擎-MyISAM和InnoDB的区别](https://learn.skyofit.com/archives/556)

sql注入怎么解决？（难度：★★★ 频率：★★）

[数据库-防止SQL注入的方案](https://learn.skyofit.com/archives/558)

三大范式（难度：★★ 频率：★）

[数据库-三大范式-介绍/使用/实例](https://learn.skyofit.com/archives/560)

怎么样幂等（难度：★★★ 频率：★★）

[数据库-幂等-方案](https://learn.skyofit.com/archives/569)

一条SQL查询语句的执行流程（难度：★★ 频率：★★）

[MySQL一条SQL查询语句的执行流程](https://learn.skyofit.com/archives/573)

为什么不要用外键？（难度：★★★ 频率：★）

[数据库-外键-用法/缺点](https://learn.skyofit.com/archives/586)

批量往数据库导入1000万条数据方法？（难度：★★ 频率：★）

- 存储过程

数据库优化方式（难度：★★★ 频率：★）

- 建立索引、字段冗余（减少联表查询）、使用缓存、读写分离、分库分表

怎么调试存储过程（难度：★★ 频率：★）

使用工具：dbForge Studio for MySQL

MySQL的三种驱动类型 难度：★★ 频率：★）

[MySQL-时区/连接器/驱动类型](https://learn.skyofit.com/archives/590)

**事务**

隔离级别是怎样的？脏读、幻读是什么意思？（难度：★★★ 频率：★★★★★）

[MySQL隔离级别-未提交读，提交读，可重复读，序列化-详解(有示例)](https://learn.skyofit.com/archives/592)

隔离级别如何选用？（难度：★★ 频率：★★）

[MySQL隔离级别-未提交读，提交读，可重复读，序列化-详解(有示例)](https://learn.skyofit.com/archives/592)

ACID（难度：★★ 频率：★）

[数据库-事务的ACID-介绍/详解](https://learn.skyofit.com/archives/598)

隔离级别是如何实现的？（MVCC）（难度：★★★★ 频率：★★）

[MySQL隔离级别的实现方式-MVCC](https://learn.skyofit.com/archives/600)

快照读与当前读 是怎样的？（难度：★★★★ 频率：★★）

[MySQL隔离级别的实现方式-MVCC](https://learn.skyofit.com/archives/600)

**索引**

索引的种类（难度：★★ 频率：★★★）

[MySQL索引的类型](https://learn.skyofit.com/archives/606)

数据库使用索引的缺点？（难度：★★ 频率：★★★）

[MySQL-索引的优点/缺点/创建索引的原则](https://learn.skyofit.com/archives/608)

创建索引的原则（难度：★★ 频率：★★★★）

[MySQL-索引的优点/缺点/创建索引的原则](https://learn.skyofit.com/archives/608)

索引什么时候会失效（难度：★★ 频率：★★★★★）

[MySQL-索引失效的原因/解决方案](https://learn.skyofit.com/archives/610)

创建了A, B, C联合索引，使用B,C能否索引（难度：★★★ 频率：★★★★★）

[MySQL联合索引-使用/原理/优化](https://learn.skyofit.com/archives/611)

LIKE什么时候走索引，什么时候不走索引？（难度：★★★ 频率：★★★）

[MySQL索引的优化-LIKE模糊查询](https://learn.skyofit.com/archives/614)

ORDER BY是否走索引？（难度：★★★ 频率：★★）

[MySQL索引的优化-ORDER BY](https://learn.skyofit.com/archives/617)

聚集索引是什么？什么是回表？（难度：★★★★ 频率：★★★★）

[MySQL-聚集索引/辅助索引/回表查询/覆盖索引(原理及优化)](https://learn.skyofit.com/archives/620)

大表分页的优化方法？（难度：★★★★ 频率：★）

[MySQL-大数据量的分页优化方案](https://learn.skyofit.com/archives/631)

索引原理；为什么采用B+树？（难度：★★★★ 频率：★）

[MySQL原理-索引的原理](https://learn.skyofit.com/archives/634)

**锁**

共享锁与独占锁的区别？（难度：★★ 频率：★）

[MySQL-行级锁与表级锁](https://learn.skyofit.com/archives/639#共享锁与独占锁)

什么时候会死锁？（难度：★★★★ 频率：★）

[MySQL-死锁的原因及解决方法](https://learn.skyofit.com/archives/641)

**分库分表**

什么时候考虑分库分表？分库分表要考虑什么问题？（难度：★★★ 频率：★）

[数据库-分库分表-方案/切分方式/注意的问题](https://learn.skyofit.com/archives/643)

原来没分库分表，后期如何分库分表？（难度：★★★★ 频率：★★）

[数据库-单表转分库分表](https://learn.skyofit.com/archives/645)

分库分表的中间件（难度：★★ 频率：★★）

- Sharding-JDBC、Mycat

水平分表，有哪些规则？（难度：★★★ 频率：★★★★★）

[数据库-分库分表-垂直分表与水平分表](https://learn.skyofit.com/archives/649)

如何维护全局的id（难度：★★★ 频率：★★★★★）

[分布式-生成数据库全局唯一ID的方案](https://learn.skyofit.com/archives/671)

**语句**

语句类笔试题（难度：★★★ 频率：★）

[MySQL-常见业务/笔试题](https://learn.skyofit.com/archives/657)

OR与IN的效率？（难度：★★★ 频率：★）

[MySQL-SQL语句优化-大全](https://learn.skyofit.com/archives/661)

内联结，全（外）联结，左联结，右联结，的含义？（难度：★★ 频率：★）

[MySQL-内联结/全联结/左联结/右联结的区别](https://learn.skyofit.com/archives/663)

## Redis

**基本问题**

Redis数据类型及其使用场景（难度：★★★ 频率：★★★★★）

[Redis-数据类型及其使用场景](https://learn.skyofit.com/archives/693)

Redis的数据类型对应的底层结构是怎样的？（难度：★★★★ 频率：★★★）

[Redis原理-数据类型的底层结构](https://learn.skyofit.com/archives/700)

Redis为什么很快？（难度：★★ 频率：★★★★★）

[Redis原理-为什么性能高，速度快？](https://learn.skyofit.com/archives/702)

Redis是单线程为什么速度依然快？（难度：★★ 频率：★★）

[Redis原理-为什么性能高，速度快？](https://learn.skyofit.com/archives/702)

Redis持久化AOF，RDB区别（难度：★★ 频率：★★★★）

[Redis持久化-AOF和RDB的区别](https://learn.skyofit.com/archives/705)

持久化：长久下来AOF文件会很大怎么办？（难度：★★★ 频率：★★）

使用重写机制。见：[Redis-重写机制（减小AOF文件大小）](https://learn.skyofit.com/archives/707)

Redis有哪些原子命令？（难度：★★★ 频率：★）

- Redis所有单个命令都是原子性的。

穿透、无底洞、雪崩、击穿 解决方案？（难度：★★★ 频率：★★★★★）

- [Redis-缓存穿透-含义/原因/解决方案](https://learn.skyofit.com/archives/710)
- [Redis-无底洞-含义/原因/解决方案](https://learn.skyofit.com/archives/734)
- [Redis-缓存雪崩-含义/原因/解决方案](https://learn.skyofit.com/archives/745)
- [Redis-缓存击穿-含义/原因/解决方案](https://learn.skyofit.com/archives/749)

Redis的发布订阅机制及其使用场景（难度：★★★★ 频率：★★）

[Redis-发布订阅-原理/使用场景](https://learn.skyofit.com/archives/751)

内存回收机制是怎样的？（或者说：淘汰策略）（难度：★★★ 频率：★★★★）

[Redis–内存回收原理（淘汰策略）](https://learn.skyofit.com/archives/756)

给一个key怎么知道是用的哪种数据类型？（难度：★ 频率：★）

- 用type命令。例如：type key1

为什么使用Redis，不用Memcache和MongoDB？（难度：★★ 频率：★★）

[Redis，Memcache，MongoDB三者的区别](https://learn.skyofit.com/archives/760)

Redis与数据库如何同步？各个方式的缺点是什么？（难度：★★★ 频率：★★★）

[Redis-保证缓存与数据库的一致性-解决方案](https://learn.skyofit.com/archives/762)

Redis很慢，如何排查及解决？（难度：★★★★ 频率：★★）

[Redis-变慢原因及排查方法](https://learn.skyofit.com/archives/767)

多线程操作同一个Key如何保证一致性？（微服务部署多个实例时如何保证一致性？）（难度：★★★★ 频率：★）

[Redis-多线程竞争同一key-解决方案](https://learn.skyofit.com/archives/779)

秒杀的时候怎么使用Redis？（难度：★★★★ 频率：★★★）

[Redis-秒杀的解决方案](https://learn.skyofit.com/archives/782)

布隆过滤器原理？什么时候会误判？（难度：★★★★ 频率：★★★）

[Redis-布隆过滤器-使用/原理/实例](https://learn.skyofit.com/archives/716)

用Redis如何实现延迟队列？（难度：★★★★ 频率：★）

[Redis高级-延迟队列](https://learn.skyofit.com/archives/784)

**分布式锁**

Redis做分布式锁如何处理超时时间？比如：超时时间是5秒，但要执行20秒，相当于没锁住；超时时间是20秒，但只需执行5秒（浪费）（难度：★★★★ 频率：★★★）

- 设置中等长度的时间，线程执行完删除这个值；另起线程，定期去刷新这个值。Redisson的分布式锁就是这个方案，见：[Redisson-分布式锁的原理](https://learn.skyofit.com/archives/786)

Redis实现分布式锁，集群环境如何处理主节点宕机这种情况？（难度：★★★★★ 频率：★）

- 使用RedLock红锁算法：若过半的Redis节点能够加锁成功则表示获取锁成功，类似于zk实现分布式锁方式。见：[Redisson-红锁(Redlock)-使用/原理](https://learn.skyofit.com/archives/1338)

**集群**

多节点有哪些部署方式？（难度：★★ 频率：★）

- 主从、哨兵、集群（Cluster）

集群不支持事务，如何解决？（难度：★★★★ 频率：★）

[Redis集群-使用/注意事项](https://learn.skyofit.com/archives/788)

主从集群中主节点死了以后，是否还能使用？如何解决？（难度：★★★ 频率：★）

- 可以使用哨兵部署，自动故障转移。

读写分离时读写分别在哪个节点（难度：★★ 频率：★）

- 在主节点上写，在从节点上读。

**集群（Cluster）**

集群（Cluster）的数据是怎样分布的？（难度：★★★★ 频率：★）

[Redis集群-数据分布](https://learn.skyofit.com/archives/2684)

集群（Cluster）如何进行节点通信？（难度：★★★★ 频率：★★）

[Redis集群-节点通信的过程(原理)](https://learn.skyofit.com/archives/823)

集群（Cluster）如何进行扩展（伸缩）？（难度：★★★ 频率：★★）

[Redis集群-伸缩的过程(原理)](https://learn.skyofit.com/archives/790)

集群（Cluster）如何进行故障转移？（难度：★★★★ 频率：★★）

[Redis集群-故障转移的过程(原理)](https://learn.skyofit.com/archives/829)

## 设计模式

项目里用到了哪些设计模式，怎么用的？（难度：★★★ 频率：★★★★★）

[Java设计模式-在项目中的应用](https://learn.skyofit.com/archives/856)

设计模式的原则（难度：★★ 频率：★）

- 这个我老是记不住，我用这个口诀：单开里依接合迪。对应每个原则的第一个字。
- 见：[Java设计模式-原则](https://learn.skyofit.com/archives/1339)

设计模式的类别（难度：★★ 频率：★）

[Java设计模式-分类及功能](https://learn.skyofit.com/archives/863)

单例模式的写法？（难度：★★ 频率：★★★★）

[Java设计模式-单例模式(6种写法)](https://learn.skyofit.com/archives/278)

手写双重检验单例（为什么用volatile，为什么两次if判断）（难度：★★★ 频率：★★★）

[Java设计模式-单例模式(6种写法)](https://learn.skyofit.com/archives/278)

静态代理与动态代理区别？（难度：★★★ 频率：★★★★★）

[Java-代理模式(静态代理与动态代理)的使用](https://learn.skyofit.com/archives/865)

## 框架

### Spring

**IOC**

Spring循环依赖解决方法及原理（难度：★★★★ 频率：★★★★）

- [Spring-循环依赖的解决方案-实例](https://learn.skyofit.com/archives/877)
- [Spring循环依赖的原理(三)-原理概述](https://learn.skyofit.com/archives/887)

Spring的循环依赖用的是三级缓存，为什么不是两级？（难度：★★★★ 频率：★★）

- [Spring循环依赖的原理(四)-为什么用三级缓存，而不是二级](https://learn.skyofit.com/archives/888)

FactoryBean和BeanFactory区别（难度：★★★★ 频率：★★）

- [Spring-BeanFactory-使用/原理/详解](https://learn.skyofit.com/archives/957)
- [Spring-FactoryBean-使用/原理/详解](https://learn.skyofit.com/archives/955)

BeanFactory和ApplicationContext区别？（难度：★★★★ 频率：★）

[Spring-ApplicationContext-使用/教程/原理](https://learn.skyofit.com/archives/959)

bean的生命周期是怎样的（难度：★★★ 频率：★）

[Spring-Bean生命周期-流程/原理](https://learn.skyofit.com/archives/925)

Spring几种scope区别（难度：★★★ 频率：★）

[Spring-Bean的作用域(scope)-使用/详解](https://learn.skyofit.com/archives/962)

Spring容器的生命周期是怎样的？（难度：★★★ 频率：★）

[Spring容器生命周期-Lifecycle](https://learn.skyofit.com/archives/963)

**AOP** 

AOP有哪几种通知，如果方法执行报异常，哪个通知不会执行？（难度：★★★★ 频率：★）

- 前置，后置，环绕，返回，异常。若报异常，返回不会执行。见：[这里](https://learn.skyofit.com/archives/966)

SpringAOP的使用场景是什么？用AOP开发过什么功能（难度：★★★ 频率：★★★）

[Spring之AOP系列-使用场景/原理](https://learn.skyofit.com/archives/971)

AOP原理？（难度：★★★★ 频率：★★★★★）

[Spring之AOP的原理(一)-概述](https://learn.skyofit.com/archives/910)

**事务** 

Spring默认数据里隔离级别是什么？项目里用的哪个？（难度：★★★ 频率：★★）

默认采用数据库的隔离级别。项目里就是用的默认的。见：[MySQL隔离级别-未提交读，提交读，可重复读，序列化-详解(有示例)](https://learn.skyofit.com/archives/592)

Spring事务什么时候会失效？如何解决？（难度：★★★★ 频率：★★★★）

[Spring事务失效-原因/解决方案](https://learn.skyofit.com/archives/974)

Spring事务传播机制？（难度：★★★★ 频率：★★）

[Spring事务传播机制详解](https://learn.skyofit.com/archives/977)

**其他**

SpringBoot如何热更新配置？（更新配置后无需重启服务）（难度：★★★ 频率：★）

有四种方案。详见：[这里](https://learn.skyofit.com/archives/2377#动态更新配置的方法)

SpringBoot自动配置原理？（难度：★★★★★ 频率：★）

[SpringBoot原理-自动配置](https://learn.skyofit.com/archives/928)

### **SpringMVC**

SpringMVC流程（难度：★★★★ 频率：★★★）

[SpringMVC的请求流程](https://learn.skyofit.com/archives/982)

servlet的过滤器、拦截器、AOP的执行顺序 （难度：★★★ 频率：★★）

[SpringBoot-过滤器/拦截器/AOP-用法](https://learn.skyofit.com/archives/988)

### SpringBoot

SpringBoot的启动流程？（难度：★★★★ 频率：★★★★）

[SpringBoot原理-启动流程](https://learn.skyofit.com/archives/902)

SpringBoot的动态代理默认用的哪个（cglib还是JDK）？（难度：★★★★ 频率：★★★★）

SpringBoot 1.5.x：默认使用JDK代理；SpringBoot 2.x：默认使用CGLIB代理。见：[Spring之AOP系列-使用场景/原理](https://learn.skyofit.com/archives/971)

怎么自己写SpringBootStarter（难度：★★★★ 频率：★）

[SpringBoot-自定义Spring Boot Starter](https://learn.skyofit.com/archives/994)

### MyBatis

MyBatis的#与$有什么区别？（难度：★★ 频率：★★★★）

[MyBatis-#与$的区别](https://learn.skyofit.com/archives/998)

MyBatis的原理？（Mapper是个接口，它的实现类在哪？）（难度：★★★★ 频率：★★）

[Spring-MyBatis源码对FactoryBean的应用](https://learn.skyofit.com/archives/956)

为什么MyBatis与Spring整合二级缓存会失效 ？（难度：★★★★ 频率：★）

[MyBatis原理-缓存机制](https://learn.skyofit.com/archives/999)

## 中间件

### MQ

**综合**

RabbitMQ，RocketMQ和Kafka区别（难度：★★ 频率：★★★★★）

[RabbitMQ，RocketMQ，Kafka的区别](https://learn.skyofit.com/archives/1004)

**RabbitMQ**

RabbitMQ有哪些交换器？RabbitMQ的交换器与队列的关系？（难度：★★ 频率：★★★）

[RabbitMQ的交换器类型与队列模式](https://learn.skyofit.com/archives/1005)

RabbitMQ的消息异常（丢失、重复、顺序、堆积）如何处理？（难度：★★★ 频率：★★★★★）

- [RabbitMQ消息丢失的原因与解决方案](https://learn.skyofit.com/archives/1018)
- [RabbitMQ消息重复的原因与解决方案](https://learn.skyofit.com/archives/1030)
- [RabbitMQ保证消息顺序的方案](https://learn.skyofit.com/archives/1031)
- [RabbitMQ消息堆积的解决方案](https://learn.skyofit.com/archives/1034)

RabbitMQ消息是否会过期？（难度：★★★ 频率：★★）

- 默认不会过期。可以设置过期时间。
- 详见：[RabbitMQ消息的过期时间(TTL)-使用/原理](https://learn.skyofit.com/archives/1035)

RabbitMQ的消息什么时候会放到死信队列？（难度：★★★ 频率：★）

[RabbitMQ死信队列-使用/原理](https://learn.skyofit.com/archives/1036)

RabbitMQ的延迟队列是怎样的？（难度：★★★ 频率：★★）

[RabbitMQ延迟队列-使用/原理](https://learn.skyofit.com/archives/1039)

RabbitMQ的集群有哪几种部署方式？（难度：★★ 频率：★）

- 多机多节点，单机多节点

**Kafka**

为什么Kafka性能很高（难度：★★★ 频率：★★★）

[Kafka为什么吞吐量大、速度快？](https://learn.skyofit.com/archives/1042)

Kafka的消息异常（丢失、重复）如何处理？（难度：★★★ 频率：★★★★）

- [Kafka消息丢失-原因/解决方案/零丢失的配置](https://learn.skyofit.com/archives/1050)
- [Kafka消息重复-原因/解决方案](https://learn.skyofit.com/archives/1051)

Kafka不支持延迟队列，如果用到延迟队列，该如何实现？（难度：★★★★★ 频率：★★★）

[Kafka延迟队列的实现方式](https://learn.skyofit.com/archives/1052)

### Shiro

Shiro怎么根据url对应权限，流程是什么？（难度：★★★ 频率：★★★）

[Shiro整合jwt-通过url控制权限](https://learn.skyofit.com/archives/1123)

session存放在哪里？（难度：★★ 频率：★）

一般放在Redis。见：[Shiro整合shiro-redis](https://learn.skyofit.com/archives/1073)

## 分布式

### 综合

**分布式**

CAP理论是什么？Zookeeper和Eureka分别放弃了什么？（难度：★★★ 频率：★★★）

- [分布式-CAP定理](https://learn.skyofit.com/archives/1141)
- [注册中心-Eureka、Zookeeper、Nacos、Consul的区别](https://learn.skyofit.com/archives/1145)

分布式锁实现方式（难度：★★★ 频率：★★★★★）

[分布式锁的实现方案](https://learn.skyofit.com/archives/1147)

2PC、3PC、TCC的区别及使用场景？（难度：★★★★ 频率：★★）

[分布式事务-理论](https://learn.skyofit.com/archives/1169)

分布式session共享解决方案（难度：★★★ 频率：★★）

[分布式Session的实现方案](https://learn.skyofit.com/archives/1189)

为什么微服务一定要有网关？（难度：★★★ 频率：★）

[微服务为什么要有网关](https://learn.skyofit.com/archives/1191)

**配置中心**

如何把微服务的公共配置给拿出来？（难度：★★ 频率：★）

1. 用spring.profiles.include，将公共的配置包含进去。
2. 使用Nacos，Nacos支持公共配置

**Nacos**

Nacos如何续期？（难度：★★★ 频率：★★）

- 这个地方我没看，回答的Eureka的： 见：[Spring Cloud Eureka原理-续期/自我保护](https://learn.skyofit.com/archives/1146)

Nacos支持AP还是CP？（难度：★★★ 频率：★★）

- 两者都支持，选一种即可。（默认是AP）

**Zookeeper**

Zookeeper注册中心挂了，服务还能否调用？（难度：★★★ 频率：★★）

- 可以，因为客户端还有缓存。

ZK分布式锁，leader节点宕机了，会发生什么？（难度：★★★★ 频率：★）

- 进行选举（过半选举）

**RPC**

RPC框架有哪些？SpringCloud是否是RPC框架？（难度：★★ 频率：★）

- Dubbo（阿里的）、gRPC（谷歌的），RMI（JAVA自带）、Thrift（Apache的）
- SpringCloud不是rpc框架，它是分布式一整套解决方案，它的feign组件是rpc框架。

SpringCloud与Dubbo的区别？（难度：★★ 频率：★）

[Dubbo与SpringCloud区别](https://learn.skyofit.com/archives/1193)

HTTP与RPC方式的区别？（难度：★★★ 频率：★）

[分布式-RPC](https://learn.skyofit.com/archives/1194)

### SpringCloud

主要是：服务注册、负载均衡、限流、降级、熔断。首先要看其原理。

**服务注册（Eureka）**

Eureka都挂了，服务还能否调用？（难度：★★★ 频率：★★）

- 可以，因为客户端还有缓存。见：[Eureka服务端挂了，为什么微服务还能调通？(原理分析)](https://learn.skyofit.com/archives/1197)

微服务关闭了，但请求还会进来，如何解决？（难度：★★★ 频率：★）

[Spring Cloud Eureka-关闭微服务后请求还会进来](https://learn.skyofit.com/archives/1199)

如何续期？如何自我保护？（难度：★★★ 频率：★★）

[Spring Cloud Eureka原理-续期/自我保护](https://learn.skyofit.com/archives/1146)

熔断（Hystrix）（难度：★★★★★ 频率：★）

[Spring Cloud-hystrix熔断的原理](https://learn.skyofit.com/archives/1205)

负载均衡（Ribbon）（难度：★★★★★ 频率：★）

[Spring Cloud Ribbon-负载均衡的原理](https://learn.skyofit.com/archives/1206)

SpringCloud限流用哪些组件？（难度：★★★ 频率：★）

- sentinal、hystrix

**配置中心**

配置中心的配置修改后，服务不重启可以获得最新配置吗？（难度：★★ 频率：★）

- 可以的。有四种方案，见：[这里](https://learn.skyofit.com/archives/2377)

**降级**

## **ELK**

正排索引与倒排索引的区别？（难度：★★★ 频率：★）

[ES-正排索引与倒排索引](https://learn.skyofit.com/archives/1209)

ES如何与数据库（如MySQL）同步数据？（难度：★★★ 频率：★★★）

[ES-与MySQL同步](https://learn.skyofit.com/archives/1212)

ES集群的健康状态，绿色、黄色、红色分别什么含义？（难度：★★★ 频率：★★★）

[ES-排查集群健康状态是Red、Yellow的问题](https://learn.skyofit.com/archives/1213)

ES写入数据的流程（难度：★★★★★ 频率：★★★）

[ES-写入数据的流程(原理)](https://learn.skyofit.com/archives/1230)

ES查询数据的流程（难度：★★★★★ 频率：★★）

[ES-查询数据的流程(原理)](https://learn.skyofit.com/archives/1234)

## 综合

有没有遇到过什么比较复杂的问题，如何排查的？（难度：★★★★ 频率：★★★★★）

[Java后端接口响应慢的排查方法及解决方案](https://learn.skyofit.com/archives/1235)

阅读过哪些源码？（难度：★★★★ 频率：★★★★）

- Spring循环依赖的原理。见：[此文](https://learn.skyofit.com/archives/887)
- MyBatis的原理。见：[此文](https://learn.skyofit.com/archives/956)
- Hystrix的原理。见：[此文](https://learn.skyofit.com/archives/1205)
- feign负载均衡的原理。见：[此文](https://learn.skyofit.com/archives/1206)

OOM如何排查？（难度：★★★ 频率：★★）

- 使用jprofiler，查看OOM时的堆输出。

Java进程消失，如何排查？（难度：★★★ 频率：★）

[Java进程突然消失的原因与排查方案](https://learn.skyofit.com/archives/1238)

一个微服务起了多个实例，怎么让定时任务只在一个实例上执行？（难度：★★★ 频率：★）

- 用定时任务中间件。常用的有：XXL-JOB、PowerJob、quartz

如何处理SpringMVC中的异常？ （难度：★★ 频率：★★★）

- 用[全局异常处理](https://learn.skyofit.com/archives/1560)：@ControllerAdvice + @ExceptionHandler。

从用户请求到数据返回的整个流程（难度：★★ 频率：★★★）

[用户请求到出现页面流程](https://learn.skyofit.com/archives/1246)

IaaS，PaaS和SaaS是什么？（难度：★★ 频率：★）

[IaaS,Paas,SaaS,DaaS-区别](https://learn.skyofit.com/archives/1250)

网站常见的安全漏洞有哪些？（难度：★★★ 频率：★）

[网站安全漏洞-大全](https://learn.skyofit.com/archives/1253)

oauth2是干什么用的，流程是怎样的？（难度：★★★★★ 频率：★★）

[OAuth2-流程/原理](https://learn.skyofit.com/archives/1259)

如何不停机更新服务？（难度：★★★★ 频率：★）

[SpringBoot项目-如何不停服更新应用？](https://learn.skyofit.com/archives/1200)

限流算法有哪些？（难度：★★★★★ 频率：★★★）

[常见的限流算法的原理以及优缺点](https://learn.skyofit.com/archives/1267)

## 杂项

**HTTP**

HTTPS的详细流程（难度：★★★★ 频率：★★）

[HTTPS-流程/原理](https://learn.skyofit.com/archives/1273)

HTTP消息结构（难度：★★ 频率：★）

[HTTP-报文结构](https://learn.skyofit.com/archives/1277)

HTTP状态码及其含义（难度：★★ 频率：★★）

简记：正完重客服。（1xx：**正**在处理请求；2xx：请求处理**完**毕（成功）；3xx：**重**定向（需要附加操作）；4xx：**客**户端错误（导致服务器无法处理请求）， 5xx：**服**务器错误（服务器处理请求出错））。详见：[此文](https://www.runoob.com/http/http-status-codes.html)

WebCocket，HTTP，Socket区别与联系？（难度：★★ 频率：★）

[Http，Socket，Websocket-区别](https://learn.skyofit.com/archives/1281)

HTTP1.0和HTTP2.0的区别？（难度：★★ 频率：★）

[HTTP1.1与HTTP2.0区别](https://learn.skyofit.com/archives/1283)

**Linux**

Linux的5种IO模型（难度：★★★★ 频率：★）

[Linux五种IO模型-原理/区别/详解](https://learn.skyofit.com/archives/1284)

**数据结构与算法**

常见排序算法的复杂度及稳定性（难度：★★★ 频率：★★）

[排序算法-Java实例/原理](https://learn.skyofit.com/archives/1291)

常见查找算法的复杂度及稳定性（难度：★★★ 频率：★★）

[查找算法-Java实例/原理](https://learn.skyofit.com/archives/1311)

**网络**

网络的5层协议的体系结构（难度：★ 频率：★★★）

[计算机网络-体系结构(五层模型/七层模型)](https://learn.skyofit.com/archives/1313)

TCP握手与挥手流程？为什么要三次？四次？（难度：★★★ 频率：★★）

[TCP-三次握手和四次挥手](https://learn.skyofit.com/archives/1315)

TCP如何保证可靠传输？（难度：★★★ 频率：★）

[TCP协议如何保证可靠传输](https://learn.skyofit.com/archives/1318)

服务器怎么主动向客户端主动推送？（难度：★★ 频率：★）

- 客户端去轮询（每秒查询一次）；WebSocket；TCP长连接；UDP内网穿透

DNS劫持是怎样的？（难度：★★★ 频率：★）

- 攻击DNS服务器或者客户端设备，修改域名对应的IP，导致通过域名访问到假IP，从而破坏原有服务。

Linux无法通过curl获得服务器主页数据如何排查？（难度：★★ 频率：★）

- 关防火墙、看host文件里边是否ip和域名绑定了

两个同网段Linux服务器在不安装客户端情况下如何传递文件？（难度：★ 频率：★）

- scp命令

**Linux命令**

查看文本文件头部n行。（难度：★ 频率：★）

- head -n 200 filename //200可替换为任一数字

查看文本文件末尾n行。（难度：★ 频率：★）

- tail -n 200 filename //200可替换为任一数字

查看文本文件行数。（难度：★ 频率：★）

- wc -l filename

**Netty**

Netty 是如何解决 TCP的拆包/粘包问题的？（难度：★★★ 频率：★）

[Netty-原理-TCP-粘包与拆包](https://learn.skyofit.com/archives/1327)

编程题（难度：★★★ 频率：★★）

[Java笔试题编程题大全(有详细答案)](https://learn.skyofit.com/archives/1331)

**大数据**

大数据量如何统计重复出现的次数？（难度：★★★★★ 频率：★）

[大数据处理方案](https://learn.skyofit.com/archives/1332)

怎么实时统计订单？（难度：★★★★★ 频率：★）

- 使用Storm框架。

要统计10分钟内订单的亏损，你会怎么设计？（难度：★★★★★ 频率：★）

- 使用Storm的窗口模式