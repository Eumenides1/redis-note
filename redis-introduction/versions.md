# Redis各个版本
## Redis2.6
- Redis2.6在2012年正是发布，经历了17个版本，到2.6.17版本，相对于Redis2.4，主要特性如下：
  - 服务端支持Lua脚本。
  - 去掉虚拟内存相关功能。
  - 放开对客户端连接数的硬编码限制。
  - 键的过期时间支持毫秒。
  - 从节点支持只读功能。
  - 两个新的位图命令：bitcount和bitop。
  - 增强了redis-benchmark的功能：支持定制化的压测，CSV输出等功能。
  - 基于浮点数自增命令：incrbyfloat和hincrbyfloat。
  - redis-cli可以使用–eval参数实现Lua脚本执行。
  - shutdown命令增强。
  - 重构了大量的核心代码，所有集群相关的代码都去掉了，cluster功能将会是3.0版本最大的亮点。
  - info可以按照section输出，并且添加了一些统计项
  - sort命令优化

----
## Redis2.8
- Redis2.8在2013年11月22日正式发布，经历了24个版本，到2.8.24版本，相比于Redis2.6，主要特性如下：
  - 添加部分主从复制的功能，在一定程度上降低了由于网络问题，造成频繁全量复制生成RDB对系统造成的压力。
  - 尝试性的支持IPv6.
  - 可以通过config set命令设置maxclients。
  - 可以用bind命令绑定多个IP地址。
  - Redis设置了明显的进程名，方便使用ps命令查看系统进程。
  - config rewrite命令可以将config set持久化到Redis配置文件中。
  - 发布订阅添加了pubsub。
  - Redis Sentinel第二版，相比于Redis2.6的Redis Sentinel，此版本已经变成生产可用。

----
## Redis3.0（里程碑）
- Redis3.0在2015年4月1日正式发布，相比于Redis2.8主要特性如下：
  - Redis Cluster：Redis的官方分布式实现。
  - 全新的embedded string对象编码结果，优化小对象内存访问，在特定的工作负载下载速度大幅提升。
  - Iru算法大幅提升。
  - migrate连接缓存，大幅提升键迁移的速度。
  - migrate命令两个新的参数copy和replace。
  - 新的client pause命令，在指定时间内停止处理客户端请求。
  - bitcount命令性能提升。
  - cinfig set设置maxmemory时候可以设置不同的单位（之前只能是字节）。
  - Redis日志小做调整：日志中会反应当前实例的角色（master或者slave）。
  - incr命令性能提升。

----
## Redis3.2
- Redis3.2在2016年5月6日正式发布，相比于Redis3.0主要特征如下：
  - 添加GEO相关功能。
  - SDS在速度和节省空间上都做了优化。
  - 支持用upstart或者systemd管理Redis进程。
  - 新的List编码类型：quicklist。
  - 从节点读取过期数据保证一致性。
  - 添加了hstrlen命令。
  - 增强了debug命令，支持了更多的参数。
  - Lua脚本功能增强。
  - 添加了Lua Debugger。
  - config set 支持更多的配置参数。
  - 优化了Redis崩溃后的相关报告。
  - 新的RDB格式，但是仍然兼容旧的RDB。
  - 加速RDB的加载速度。
  - spop命令支持个数参数。
  - cluster nodes命令得到加速。
  - Jemalloc更新到4.0.3版本。

----
## Redis4.0
- 可能出乎很多的意料，Redis3.2之后的版本是4.0，而不是3.4、3.6、3.8。一般这种重大版本号的升级也意味着软件或者工具本身发生了重大改革。下面是Redis4.0的新特性：
  - 提供了模块系统，方便第三方开发者拓展Redis的功能。
  - PSYNC2.0：优化了之前版本中，主从节点切换必然引起全量复制的问题。
  - 提供了新的缓存剔除算法：LFU（Last Frequently Used），并对已有算法进行了优化。
  - 提供了非阻塞del和flushall/flushdb功能，有效解决删除了bigkey可能造成的Redis阻塞。
  - 提供了memory命令，实现对内存更为全面的监控统计。
  - 提供了交互数据库功能，实现Redis内部数据库的数据置换。
  - 提供了RDB-AOF混合持久化格式，充分利用了AOF和RDB各自优势。
  - Redis Cluster 兼容NAT和Docker。

----
## Redis5.0
- 新的Stream数据类型。[1]5.0
- 新的Redis模块API：Timers and Cluster API。
- RDB现在存储LFU和LRU信息。
- 集群管理器从Ruby（redis-trib.rb）移植到C代码。可以在redis-cli中。查看redis-cli —cluster help了解更多信息。
- 新sorted set命令：ZPOPMIN / MAX和阻塞变量。
- 主动碎片整理V2。
- 增强HyperLogLog实现。
- 更好的内存统计报告。
- 许多带有子命令的命令现在都有一个HELP子命令。
- 客户经常连接和断开连接时性能更好。
- 错误修复和改进。
- Jemalloc升级到5.1版

----
## Redis6.0
- 多线程IO。Redis 6引入多线程IO。但多线程部分只是用来处理网络数据的读写和协议解析，执行命令仍然是单线程。之所以这么设计是不想因为多线程而变得复杂，需要去控制 key、lua、事务，LPUSH/LPOP 等等的并发问题。
- 重新设计了客户端缓存功能。实现了Client-side-caching（客户端缓存）功能。放弃了caching slot，而只使用key names。
- RESP3协议。RESP（Redis Serialization Protocol）是 Redis 服务端与客户端之间通信的协议。Redis 5 使用的是 RESP2，而 Redis 6 开始在兼容 RESP2 的基础上，开始支持 RESP3。
- 支持SSL。连接支持SSL，更加安全。
- ACL权限控制
  - 支持对客户端的权限控制，实现对不同的key授予不同的操作权限。
  - 有一个新的ACL日志命令，允许查看所有违反ACL的客户机、访问不应该访问的命令、访问不应该访问的密钥，或者验证尝试失败。这对于调试ACL问题非常有用。
- 提升了RDB日志加载速度。根据文件的实际组成（较大或较小的值），可以预期20/30%的改进。当有很多客户机连接时，信息也更快了，这是一个老问题，现在终于解决了。
- 发布官方的Redis集群代理模块 Redis Cluster proxy。在 Redis 集群中，客户端会非常分散，现在为此引入了一个集群代理，可以为客户端抽象 Redis 群集，使其像正在与单个实例进行对话一样。同时在简单且客户端仅使用简单命令和功能时执行多路复用。
- 提供了众多的新模块（modules）API
