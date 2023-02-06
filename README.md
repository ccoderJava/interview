# Interview
面试相关知识，interview knowledge


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

## 集合

## JUC多线程、锁

## 网络

## Spring


## Mybatis


## MySQL

## JVM

## Redis

## Kafka

## Zookeeper

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


