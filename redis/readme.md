<!-- TOC -->
  * [1. Redis使用场景](#1-redis使用场景)
  * [2. Redis数据类型](#2-redis数据类型)
    * [2.1 5种基本数据类型](#21-5种基本数据类型)
    * [2.2 8种基本数据结构](#22-8种基本数据结构)
<!-- TOC -->

![](images/Redis.svg)


## 1.数据结构
+ String 字符串
+ hash 散列
+ set 集合
+ list 列表
+ zset 有序集合

## 2.功能
+ bitmap  实现布隆过滤器
+ HyperLogLog 大规模去重统计 UV
+ Geospatial 地理Geo信息
+ pub/sub 订阅发布，可实现消息队列
+ pipeline 批量执行命令 减少请求
+ Lua脚本执行扩展功能，分布式锁
+ 事务 非严格事务

## 3.数据持久化
+ AOF：Append Only File
  + 增量日志
+ RDB：Redis Database
  + 快照

## 4.Key失效机制
+ 主动删除
+ 被动删除

## 5.淘汰策略
+ voltile-lru：加入Key时超限，从配置过期时间Key中删除最久未使用Key
+ voltile-ttl：加入Key时超限，从配置过期时间Key中删除即将过期Key
+ voltile-random：加入Key时超限，过期键集合随机删除
+ allkeys-lfu：加入Key时超限，LFU算法删除最少使用Key
+ allkeys-lru：加入Key时超限，LRU算法删除最久未使用Key
+ allkeys-random：加入Key时超限，所有Key中随机删除
+ noeviction：内存超限时返回错误，不会淘汰任何Key

+ 过期策略
  + 定期删除：定期随机遍历过期Key进行删除
  + 惰性删除：过期Key在访问时进行删除

## 6.Redis4.0 5.0 6.0特性

## 7.redis cluster
### 7.1 主从同步
+ salve的priority越低，优先级越高
+ 相同情况下，salve复制数据越多，优先级越高
+ 相同条件下runid越小越容易选中 
### 7.2 sentinel
+ 一主二从三哨兵
+ 集群监控：兼容master 、salve是否健康
+ 消息通知：节点实例故障时进行告警通知
+ 故障转移：master节点故障，会自动转移到salve 节点
+ 配置中心：故障发生转移时，通知client连接到新的Master节点
### 7.3 master选举

## 8.常见问题
+ 缓存更新
+ 数据一致性问题
+ 缓存穿透
+ 缓存击穿
+ 缓存雪崩
