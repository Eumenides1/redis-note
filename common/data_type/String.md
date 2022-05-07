# 字符串（strings）类型
- 字符串是Redis最简单的储存类型，它存储的值可以是字符串、整数或者浮点数，对整个字符串或者字符串的其中一部分执行操作；对整数或者浮点数执行自增（increment）或者自减（decrement）操作。
- Redis的字符串是一个由字节组成的序列，跟java里面的ArrayList有点类似，采用预分配冗余空间的方式来减少内存的频繁分配，如图中所示，内部为当前字符串实际分配的空间 capacity 一般要高于实际字符串长度 len。当字符串长度小于 1M 时，扩容都是加倍现有的空间，如果超过 1M，扩容时一次只会多扩 1M 的空间。需要注意的是字符串最大长度为 512M 。
## 应用场景
- 字符串类型在工作中使用广泛，主要用于缓存数据，提高查询性能。比如存储登录用户信息、电商中存储商品信息、可以做计数器（想知道什么时候封锁一个IP地址(访问超过几次)）等等。
## 操作指令
> [!tip]
> 指令:
> - set key value: 添加一条String类型数据
> - get key: 获取一条String类型数据
> - mset key1 value1 key2 value2: 添加多条String类型数据
> - mget key1 key2: 获取多条String类型数据
> - incr key: 自增（+1）
> - incrby key step: 按照步长（step）自增
> - decr key: 自减（-1）
> - decrby key step: 按照步长（step）递减
----
## 实操
```shell
# 插入字符串  
>set username zhangsan  
"OK"  
​  
# 获取字符串  
>get username  
"zhangsan"  
​  
# 插入多个字符串  
>mset age 18 address bj  
"OK"  
​  
# 获取多个字符串  
>mget username age  
 1)  "zhangsan"  
 2)  "18"  
​  
# 自增  
>incr num  
"1"  
>incr num  
"2"  
​  
# 自减  
>decr num  
"1"  
​  
# 指定步长自增  
>incrby num 2  
"3"  
>incrby num 2  
"5"  
​  
# 指定步长自减  
>decrby num 3  
"2"  
​  
# 删除  
>del num  
"1"

```
