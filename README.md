# Redis介绍

> Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件。 它支持多种类型的数据结构，如 字符串（strings），散列（hashes）， 列表（lists）， 集合（sets）， 有序集合（sorted sets） 与范围查询， bitmaps， hyperloglogs 和 地理空间（geospatial） 索引半径查询。 Redis 内置了复制（replication），LUA脚本（Lua scripting），LRU驱动事件（LRU eviction），事务（transactions）和不同级别的 磁盘持久化（persistence）， 并通过Redis哨兵（Sentinel） 和自动分区（Cluster）提供高可用性（high availability）

## 特点
- 内存数据库，速度快，也支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等多种数据结构的存储。
- Redis支持数据的备份（master-slave）与集群（分片存储），以及拥有哨兵监控机制。
- 支持事务

## 优势
- 性能极高 – Redis能读的速度是110000次/s，写的速度是81000次/s 。
- 丰富的数据类型 – Redis支持 Strings、Lists、 Hashes、Sets 、Sorted Sets 等数据类型操作。
- 原子操作 – Redis的所有操作都是原子性的，同时Redis还支持对几个操作合并后的原子性执行。（事务）
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等特性
----

