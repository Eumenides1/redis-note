# Hash
## 基本概念
- 散列相当于Java中的HashMap，内部是无序字典。实现原理跟HashMap一致。一个哈希表有多个节点，每个节点保存一个键值对。
- 与Java中的HashMap不同的是，rehash 的方式不一样，因为 Java 的 HashMap 在字典很大时，rehash 是个耗时的操作，需要一次性全部 rehash。Redis 为了高性能，不能堵塞服务，所以采用了渐进式 rehash 策略。
- 渐进式 rehash 会在 rehash 的同时，保留新旧两个 hash 结构，查询时会同时查询两个 hash 结构，然后在后续的定时任务中以及 hash 操作指令中，循序渐进地将旧 hash 的内容一点点迁移到新的 hash 结构中。当搬迁完成了，就会使用新的hash结构取而代之。
- 当 hash 移除了最后一个元素之后，该数据结构自动被删除，内存被回收。
## 应用场景
- Hash也可以同于对象存储，比如存储用户信息，与字符串不一样的是，字符串是需要将对象进行序列化（比如json序列化）之后才能保存，而Hash则可以讲用户对象的每个字段单独存储，这样就能节省序列化和反序列的时间。
- 此外还可以保存用户的购买记录，比如key为用户id，field为商品id，value为商品数量。同样还可以用于购物车数据的存储，比如key为用户id，field为商品id，value为购买数量等等。
## 操作指令
> [!tip]
> 指令:
> - 设置属性
>   - hset keyname field1 value1 field2 value2
> - 获取某个属性值
>   - hget keyname field
> - 获取所有属性值
>   - hgetall keyname
> - 删除某个属性
>   - hdel keyname field
> - 获取属性个数
>   - hlen keyname
> - 按照步长自增/自减某个属性（该属性必须是数字）
>   - hincrby keyname field step
----
## 实操
```shell
# 插入 hash 数据
>hset userInfo username zhangsan age 18 address bj
"3"
# 获取 hash 单条 field 数据
>hget userInfo username
"zhangsan"
>hget userInfo age
"18"
# 获取 hash 多个 field 数据
>hmget userInfo username age
1) "zhangsan"
2) "18"
# 获取 hash 所有 field 数据
>hgetall userInfo
1) "username"
2) "zhangsan"
3) "age"
4) "18"
5) "address"
6) "bj"
# 获取 hash 的 field 个数
>hlen userInfo
"3"
# 自增 hash 的某个 field
>hincrby userInfo age 2
"20"
>hincrby userInfo age 2
"22"
# 自减 hahs 的某个 field（通过自增负步长达到）
>hincrby userInfo age -2
"20"
# 删除 hash 的某个 field
>hdel userInfo age
"1"
# 删除 hash 所有数据
>del userInfo
"1"

```



