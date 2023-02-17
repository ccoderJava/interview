<!-- TOC -->
  * [专业技能方面](#专业技能方面)
  * [设计模式](#设计模式)
    * [单例模式](#单例模式)
    * [工厂模式](#工厂模式)
    * [抽象工厂模式](#抽象工厂模式)
    * [策略模式](#策略模式)
    * [观察者模式](#观察者模式)
  * [集合](#集合)
  * [JUC多线程、锁](#juc多线程锁)
    * [volatile关键字作用](#volatile关键字作用)
  * [网络](#网络)
  * [Spring](#spring)
    * [介绍下 Spring IoC 的流程](#介绍下-spring-ioc-的流程)
    * [BeanFactory 和 FactoryBean 的区别](#beanfactory-和-factorybean-的区别)
    * [Spring 的 AOP 是怎么实现的](#spring-的-aop-是怎么实现的)
    * [Spring 的事务传播行为有哪些，讲下嵌套事务](#spring-的事务传播行为有哪些讲下嵌套事务)
    * [什么情况下对象不能被代理](#什么情况下对象不能被代理)
    * [Spring 怎么解决循环依赖的问题](#spring-怎么解决循环依赖的问题)
    * [要在 Spring IoC 容器构建完毕之后执行一些逻辑，怎么实现](#要在-spring-ioc-容器构建完毕之后执行一些逻辑怎么实现)
    * [@Resource 和 @Autowire 的区别](#resource-和-autowire-的区别)
    * [@Autowire 怎么使用名称来注入](#autowire-怎么使用名称来注入)
  * [Mybatis](#mybatis)
  * [MySQL](#mysql)
  * [JVM](#jvm)
  * [Redis](#redis)
  * [Kafka](#kafka)
  * [Zookeeper](#zookeeper)
  * [分布式理论](#分布式理论)
  * [数据一致性解决方案](#数据一致性解决方案)
<!-- TOC -->

## 专业技能方面
+ 基础
  + JDK 常用类的原理、源码、使用场景。
+ 设计模式：常用几种的原理、使用场景，单例、动态代理、模板、责任链等。
+ 数据结构：数组、链表、栈、队列、树。
+ 网络：TCP、HTTP、HTTPS、负载均衡算法。
+ 框架：Spring IoC 原理、Spring AOP 原理和使用、Spring 常用的扩展点、MyBatis 的核心流程。
+ 中间件：常用中间件的核心原理与最佳实践，并对其中的 1 到 2 个有深入的学习，Redis、Kafka（RocketMQ、RabbitMQ）、Dubbo、Zookeeper。
+ 数据库（MySQL）：索引原理、隔离级别、锁机制、分库分表、慢 SQL 定位及优化、线上问题解决。
+ Netty：NIO 原理、核心组件、I/O 多路复用（epoll）、零拷贝。
+ JVM：运行时数据区、垃圾回收算法、垃圾回收器（CMS、G1）、常用配置参数、线上问题定位及解决。
+ 稳定性保障：隔离、限流、熔断、降级等。
+ Linux：基本命令的使用、快速定位和排查问题。
+ 分布式理论：CAP、BASE、2PC、3PC、TCC。

## 设计模式
### 单例模式
  保证一个类仅有一个实例，并提供一个全局访问点。使用场景：需要限制实例数量的类。
```java
public class Singleton {
    private volatile static Singleton instance;
  
    private Singleton() {}
  
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```
  + 能够避免实例对象的重复创建，可以减少每次创建对象的时间开销，还能够节约内存空间。
  + 能够避免由于操作多个实例导致的逻辑错误。
  + 如果一个实例对象可能贯穿整个应用程序，并且充当统一管理作用，那么可以考虑单例模式。
  + DCL 双重检查锁定，volatile 防止指令重排序。

### 工厂模式
定义一个用于创建对象的接口，但是让子类决定实例化哪一个类。使用场景：需要动态创建对象的场景。

### 抽象工厂模式
提供一个创建一系列相关或相互依赖对象的接口，而不需要指定它们具体的类。使用场景：当需要生成多个产品对象，且它们是相关联的时候。

### 策略模式
定义了算法家族，分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户。使用场景：许多相关的类仅仅是行为有异。

### 观察者模式
定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。使用场景：当一个对象的改变需要同时改变其他对象，而不知道具

## 集合
+ 经常用到哪些 Map
+ 这几种 Map 的区别
+ ConcurrentHashMap 怎么保证线程安全
+ ConcurrentHashMap 在 JDK 1.8 前后的锁有什么区别
+ 聊下 HashMap 的原理
+ HashMap 在 Put 时，新链表节点是放在头部还是尾部
+ HashMap 扩容时的流程
+ HashMap 在 JDK 1.8 有什么改变
+ ConcurrentHashMap 在 JDK 1.8 有什么改变
+ TreeMap 的原理
+ Map、List、Set 分别说下你知道的线程安全类和线程不安全的类


## JUC多线程、锁
### volatile关键字作用
+ Volatile 关键字是 Java 语言提供的一种线程同步机制。
  + 保证了变量的可见性：当一个线程对变量进行修改时，其他线程能够立即看到这个修改。
  + 禁止了指令重排：在读取一个 volatile 变量之前，编译器和处理器会将之前对这个变量的修改立刻刷新到主存，在写入一个 volatile 变量之后，编译器和处理器会将该变量的值立即刷新到主存，这确保了变量在读写操作中的一致性。
+ 由于 volatile 变量的特殊性，它只能保证变量的可见性和禁止指令重排，但不能保证原子性，如果需要对一个 volatile 变量进行多个操作，需要加锁。
---

+ 线程池使用的是哪种
+ 线程池参数怎么配置 
+ 线程池各个参数的作用
+ 线程池的参数配置要注意什么
+ 线程池的工作流程
+ JDK 中的并发类知道哪些
+ AQS 的底层原理
+ 介绍下悲观锁和乐观锁
+ 使用过哪些锁
+ synchronized 和 Lock 的区别、使用场景
+ synchronized 原理
+ synchronized 作用于静态方法、普通方法、this、Lock.class 的区别
+ 为什么引入偏向锁、轻量级锁，介绍下升级流程
+ 死锁的必要条件，如何预防死锁
> 死锁的必要条件有四个：互斥条件、请求和保持条件、不剥夺条件、环路等待条件。
> + 互斥条件：一个资源每次只能被一个进程使用。
> + 请求和保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
> + 不剥夺条件：进程已获得的资源，在未使用完之前，不能强行剥夺。
> + 环路等待条件：若干进程之间形成一种头尾相接的循环等待资源的关系。
>
> 预防死锁的方法：
> + 避免使用多个资源。
> + 避免持有一个资源并等待另一个资源。
> + 资源按顺序分配，破坏环路等待条件。
> + 强制预防死锁，检测死锁的发生，定期对系统资源进行状态检查，发现死锁及时解决。

+ 介绍下 CountDownLatch 和 CyclicBarrier
> CountDownLatch：一个线程或多个线程等待其他线程完成操作后才执行。计数减少
> CyclicBarrier：多个线程相互等待，任何一个线程完成之前，所有的线程都必须等待。类似于公交车
+ 介绍下 CAS，存在什么问题
+ 介绍下 ThreadLocal，存在什么问题

## 网络
+ HTTPS 是怎么加密的
> SSL/TLS 协议，对称加密和非对称加密
+ 普通 Hash 和一致性 Hash 原理
> 普通 Hash：根据 key 的 hash 值，对服务器进行取模运算，得到服务器的下标，然后根据下标获取服务器。
> 一致性 Hash：一致性 Hash 算法在普通 Hash 算法的基础上，引入了虚拟节点的概念，将每个实际节点映射到多个虚拟节点
+ 一致性 Hash 的缺点
> + 一致性 Hash 算法的缺点是，当服务器节点增加或减少时，会导致大量的缓存失效，因为缓存的 key 与服务器的映射关系发生了变化。
> + 考虑分布均匀问题
+ TCP 三次握手过程，为什么需要三次握手
+ 为什么 TIME_WAIT 状态需要经过 2MSL 才能返回到 CLOSE 状态
> + TIME_WAIT 状态的作用是确保所有的报文都能够被处理完毕，防止连接关闭后还有数据滞留在网络中，导致新连接出现混淆。但是这也会带来一定的性能损失，因为需要等待 2MSL 时间，才能释放该连接
> + 为了避免网络中存在滞留的数据包，导致这个连接上的数据包到达了新的连接，产生数据混淆。所以等待时间设置为 2MSL（Maximum Segment Lifetime），即一个报文最长的生命周期。这个时间确保了这个连接中所有的报文都被彻底销毁，防止在建立新连接时，使用了旧连接的数据。当 TIME_WAIT 时间到达后，主动关闭方进入 CLOSE 状态，关闭连接。
+ TCP 的拥塞控制
> 滑动窗口
+ TCP 如何解决流控、乱序、丢包问题
> + 确认重传
> + 滑动窗口
> + 超时重传
+ 为什么会出现粘包和拆包，如何解决
+ OSI七层模型分别是什么？各自功能

## Spring
### 介绍下 Spring IoC 的流程
### BeanFactory 和 FactoryBean 的区别
+ BeanFactory Spring中主要的容器，负责Bean的生命周期、依赖关系的管理
  + Bean的实例化:提供多种Bean的实例化方式、构造器方式、工厂方法方式、静态工厂方法方式
  + Bean的生命周期管理：会在Bean的创建完成后进行初始化，包括属性值设置、回调函数等。
  + Bean的依赖关系管理：可以通过依赖注入的方式将依赖的Bean注入到当前Bean中。
+ FactoryBean 工厂Bean接口，Spring可以通过该方式创建bean，返回值是通过它创建的bean
  + 自定义实例化Bean: 通过实现FactoryBean可以自己通过编程方式控制Bean的实例化过程
  + Bean对象缓存：FactoryBean可以将创建的Bean对象进行缓存，提高Bean对象创建效率
  + 返回其他类型：可以返回任意类型对象，不仅仅是Bean对象
+ BeanFactory 是一个容器，负责管理 Bean 的生命周期和依赖关系，而 FactoryBean 是一个工厂 Bean 接口，用于创建 Bean 实例，可以自定义 Bean 的创建过程并返回任意类型的对象。

### Spring 的 AOP 是怎么实现的
代理
+ JDK动态代理
  + 接口代理
+ CGLIB动态代理
  + 类代理
+ 对一个对象进行AOP时会对其代理对象，代理对象进行暴露，从而增强日志记录、性能监控、异常监控等处理
+ Interceptor Chain拦截器执行链和代理对象，当对象方法被调用时，会先执行拦截器链，然后再执行代理对象的方法，从而进行增强处理
+ 
### Spring 的事务传播行为有哪些，讲下嵌套事务
事务存在两个及两个以上
+ 支持当前事务
  + REQUIRED 需要有： 有则加入、无则创建
  + SUPPORTS 支持： 有则加入、无则不加入
  + MANDATORY 强制： 有则加入、无则抛出异常
+ 不支持当前事务
  + REQUIRES_NEW 新建： 有则挂起、无则创建
  + NOT_SUPPORTED 不支持： 有则挂起、无则不加入
  + NEVER 不允许： 有则抛出异常、无则不加入
+ 嵌套事务Nested
  + NESTED 嵌套： 有则创建嵌套事务、无则创建


### 什么情况下对象不能被代理
+ JDK动态代理
  + 必须实现接口
  + Spring管理的Bean
+ Cglib代理
  + 被final修饰
  + 没有无参构造
  + synchronized修饰

### Spring 怎么解决循环依赖的问题
+ 循环依赖产生原因
  + 出现循环依赖的Bean必须要是单例
  + 依赖注入的方式不能全是构造器注入的方式
+ 如何解决
  + 三级缓存
  + singletonObjects：缓存某个beanName对应的经过了完整生命周期的bean
  + earlySingletonObjects：缓存某个beanName对应的bean，但是bean的生命周期还没有完全走完
  + singletonFactories：缓存某个beanName对应的ObjectFactory，用于创建bean

### 要在 Spring IoC 容器构建完毕之后执行一些逻辑，怎么实现
https://blog.csdn.net/lzb348110175/article/details/106071906

主要是对于Bean的初始化完成后执行一些业务逻辑
+ 实现BeanPostProcessor接口 重写postProcessorAfterInitialization方法、postProcessorBeforeInitialization方法、postProcessorInitialization方法
+ 实现SmartLifecycle接口，重写start方法、stop方法、isRunning方法、isAutoStartup方法、getPhase方法
+ 实现ApplicationListener接口，重写onApplicationEvent方法
+ 实现ApplicationContextAware接口，重写setApplicationContext方法
+ 实现BeanNameAware接口，重写setBeanName方法
+ 实现BeanFactoryAware接口，重写setBeanFactory方法
+ 实现InitializingBean接口，重写afterPropertiesSet方法
+ 实现DisposableBean接口，重写destroy方法
+ 使用@PostConstruct注解
+ 使用@PreDestroy注解
+ 使用@Bean的initMethod属性
+ 实现CommandRunner接口 实现run方法

### @Resource 和 @Autowire 的区别
+ 作用域需要注入的属性上或setter
+ @Autowire 默认按类型注入，如果有多个类型相同的bean，会按名称注入
+ @Resource 按照BeanName注入，如果没有指定BeanName，会按照类型注入

### @Autowire 怎么使用名称来注入
+ @Qualifier

+ bean 的 init-method 属性指定的方法里用到了其他 bean 实例，会有问题吗
+ @PostConstruct 修饰的方法里用到了其他 bean 实例，会有问题吗
+ Spring 中，有两个 id 相同的 bean，会报错吗，如果会报错，在哪个阶段报错
+ Spring 中，bean 的 class 属性指定了一个不存在的 class，会报错吗，如果会报错，在哪个阶段
+ Spring 中的常见扩展点有哪些


## Mybatis
+ Mybatis 中 # 和 $ 的区别
+ 怎么防止 SQL 注入
+ 使用 Mybatis 时，调用 DAO（Mapper）接口时是怎么调用到 SQL 的
+ Mybatis 的缓存机制
+ Mybatis 的一级缓存和二级缓存
+ 简述Mybatis的插件运行原理，以及如何编写一个插件
+ Mybatis的动态SQL是如何实现的
+ 


## MySQL
### MySQL 索引的数据结构
  + B-Tree 平衡树 ，按照索引顺序存储于树中，效率高
  + B+Tree 平衡树，叶子节点存放数据，非叶子节点存放索引，效率高，适合于范围查找、排序
  + Hash 散列表，效率高，但是不能用于排序
  + R-Tree 矩形树，用于空间索引
  + Full-Text 全文索引，用于全文索引
  + 倒排索引，用于全文索引

### 为什么使用 B+ 树，与其他索引相比有什么优点
### 各种索引之间的区别
### B+ 树在进行范围查找时怎么处理

+ 索引查找的过程
+ MySQL 索引叶子节点存放的是什么
### 联合索引（复合索引）的底层实现
+ 单字段索引类似
+ 联合索引，非叶子节点记录 多个字段前缀值
+ 联合索引第一个字段查找、第二个字段过滤
+ 联合索引字段越多 树高度越高，效率越低
+ 联合索引字段越多，索引占用空间越大
+ 
### MySQL 如何锁住一行数据
+ MySQL行锁方式
+ 先读后写（排他锁）：通过SELECT...FOR UPDATE语句，先读取行的数据，然后再对行的数据进行更新，期间其他事务不能读取和修改该行的数据
+ 先写后读（共享锁）：通过SELECT...LOCK IN SHARE MODE语句，先对行进行共享锁，然后再读取该行的数据，期间其他事务可以读取该行的数据但不能修改该行的数据

### SELECT 语句能加互斥锁吗
+ 不能，select从数据库中查询数据
+ 但是，select for update 会加互斥锁
### 多个事务同时对一行数据进行 SELECT FOR UPDATE 会阻塞还是异常
+ 阻塞等待，需要避免死锁和超时

### MySQL 使用的版本和执行引擎
+ 8.0 InnoDB引擎

### MySQL 不同执行引擎的区别
+ InnoDB 支持事务，支持行级锁，支持外键，支持 MVCC
+ InnoDB 不支持全文索引，不支持空间索引，表行数select count(1) from table_name 会扫描全表
+ InnoDB 适用于事务 并发读写的场景
### MySQL 的事务隔离级别
+ 读未提交 read uncommitted
+ 读已提交 read committed
+ 重复度 repeated read
+ 串行化 serialized
### MySQL 的可重复读是怎么实现的
+ 每个事务transactionID，向InnoDB申请严格递增
+ 行记录有多个版本row trxId
+ 读取数据时，只读取 trxId <= 当前事务 trxId 的数据
+ 通过undo log实现 和 trxId 构建出满足当前隔离界别的数据
+ 可重复度核心是一致性读，事务更新时只能使用current read 当前读，不能使用next read，next read会读取到其他事务的数据
+ 事务更新时，会先将数据写入undo log，然后再更新数据，更新数据时，会将当前事务的trxId写入到行记录中
+ 当前记录的行锁被其他事务占据，当前事务会等待，直到锁被释放
### MySQL 是否会出现幻读
+ 会的 MVCC机制无法控制幻读，仅支持行级别控制
+ 事务A读取数据，事务B插入数据，事务A再次读取数据，会出现幻读

### MySQL 的 gap 锁
+ 间隙锁 会锁住索引范围内的所有记录，但不包括记录本身
+ 间隙锁是为了防止幻读
+ 间隙锁是在索引上加锁，而不是在数据行上加锁
+ next key lock

### MySQL 的主从同步原理
+ binlog
+ 三个线程
  + 主 发送binlog
  + 从 接收binlog
  + 从 从写入数据
### 分库分表的实现方案

### 分布式唯一 ID 方案
+ 唯一性
+ 有序性
+ 可用心
+ 自用性 无中心
+ 安全性
+ 方案
  + 批量缓存自增 根据机器数量分配不同段
  + redis
  + uuid
  + snowflake
    + 41位时间戳
    + 10位机器id
    + 12位序列号
    + 1位符号位
  + Leaf 美团分布式ID发号器
    + 1位标志符
    + 41位时间戳
    + 22位序列号
### 如何优化慢查询
+ 索引优化
+ show_query_log 记录超时log
+ 拆表

### explain 中每个字段的意思
+ id 
+ select_type SQL类型
+ table 表
+ partitions 分区
+ type 类型
+ possible_keys 可能使用的索引
+ ...
### explain 中的 type 字段有哪些常见的值
+ system 系统表 记录一条数据
+ const 常量
+ eq_ref 唯一索引
+ ref 非唯一性索引扫描
+ range 索引范围
+ index 遍历索引树
+ all 全表扫描
+ explain 中你通常关注哪些字段，为什么

## JVM
+ 运行时数据区
+ 服务器使用的什么垃圾收集器
+ CMS 垃圾收集的原理
+ G1 垃圾收集的特点，为什么低延迟
+ 有哪些垃圾回收算法，优缺点
+ 哪些对象可以作为 GC Roots
+ 有哪些类加载器
+ 双亲委派模式，哪些场景是打破双亲委派模式
+ 线上服务器出现频繁 Full GC，怎么排查
+ 定位问题常用哪些命令
+ 介绍下 JVM 调优的过程

## Redis
+ 项目中使用的 Redis 版本
+ Redis 在项目中的使用场景
+ Redis 怎么保证高可用
+ Redis 的选举流程
+ Redis 和 Memcached 的区别
+ Redis 的集群模式
+ Redis 集群要增加分片，槽的迁移怎么保证无损
+ Redis 分布式锁的实现
+ Redis 删除过期键的策略
+ Redis 的内存淘汰策略
+ Redis 的 Hash 对象底层结构
+ Redis 中 Hash 对象的扩容流程
+ Redis 的 Hash 对象的扩容流程在数据量大的时候会有什么问题吗
+ Redis 的持久化机制有哪几种
+ RDB 和 AOF 的实现原理、优缺点
+ AOF 重写的过程
+ 哨兵模式的原理
+ 使用缓存时，先操作数据库还是先操作缓存
+ 为什么是让缓存失效，而不是更新缓存
+ 缓存穿透、缓存击穿、缓存雪崩
+ 更新缓存的几种设计模式

## Kafka

## Zookeeper
+ Zookeeper 的使用场景
+ Zookeeper 怎么实现分布式锁
+ Zookeeper 怎么保证数据的一致性
+ ZAB 协议的原理
+ Zookeeper 遵循 CAP 中的哪些
+ Zookeeper 和 Eureka 的区别
+ Zookeeper 的 Leader 选举
+ Observer 的作用
+ Leader 发送了 commit 消息，但是所有的 follower 都没有收到这条消息，Leader 就挂了，后续会怎么处理

## 分布式理论
+ CAP 理论
+ BASE 理论
+ 分布式事务 2PC 和 TCC 的原理
+ TCC 在 cancel 阶段如果出现失败怎么处理
+ Paxos 算法、Raft 算法

## 数据一致性解决方案
+ 分布式事务：通过两阶段提交协议 (2PC) 和三阶段提交协议 (3PC) 解决分布式系统中的数据一致性问题。
+ 本地消息表：通过本地消息表记录所有操作，再异步地将操作同步到其它数据存储节点，解决数据一致性问题。
+ 基于版本号的解决方案：通过版本号来判断数据是否已经过期，从而决定是否要更新数据。
+ 基于快照的解决方案：通过定期生成快照来解决数据一致性问题。


