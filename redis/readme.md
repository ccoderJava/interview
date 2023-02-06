## 1. Redis使用场景
+ 缓存
+ 分布式锁
  + lua
  + setnx
  + redlock
  + zookeeper
  + etcd 
  + consul
+ 排行榜（zset）
+ 计数（incrby）
  + 限流
  + 访问量
  + 点赞
  + 购物车
+ 消息队列（stream）
+ 理位置（geo）
+ 访客统计（hyperloglog）


## 2. Redis数据类型
### 2.1 5种基本数据类型
+ String 字符串
+ Hash 散列
+ List 列表
+ Set 集合
+ Zset 有序集合

### 2.2 8种基本数据结构

| String |  List  |  Hash   | Set   | Zset |
|--------|-----|-----|-------|------|
| SDS    |  LinkedList/ZipList/QuickList	   |   Hash Table、ZipList	  | ZipList、Intset	 |   ZipList、SkipList|

+ 简单动态字符串（SDS）
  + 二进制安全
  + 保存字符串长度
  + 保存字符串内容
  + 保存字符串结尾的空字符
+ 双向链表（LinkedList）
    + 保存节点的指针
    + 保存节点的值
    + 保存前置节点的指针
    + 保存后置节点的指针
+ 字典（Hash Table）
+ 跳跃表（SkipList）
+ 整数集合（Intset）
+ 压缩列表（ZipList）
+ 快速列表（QuickList）
