# Redis_command_命令



安装单机版redis

1、编译redis

cd /opt/

tar zxvf redis-3.0.6.tar.gz 

cd redis-3.0.6

make

2、创建redis目录

cd src/

mkdir /usr/local/redis

cp redis-cli /usr/local/redis/

cp redis-server /usr/local/redis/

cd ..

cp redis.conf /usr/local/redis/

3、修改配置文件

cd /usr/local/redis/

vim redis.conf 

    daemonize yes

4、运行redis

./redis-server redis.conf

5、简单测试

./redis-cli 

    127.0.0.1:6379> set name tom
    
    OK
    
    127.0.0.1:6379> get name
    
    "tom"

主从模式的redis

1、在主从服务器上安装redis

2、修改从服务器配置文件

cd /usr/local/redis

vim redis.conf

    slaveof 192.168.8.61 6379(主)

3、重启redis

4、查看主从状态

info replication

配置sentinel模式的集群（所有节点都配置）

1、创建sentinel.conf文件

cd /usr/local/redis

vim redis.conf

    daemonize yes
    
    sentinel monitor test1 192.168.8.61 6379 1

2、启动redis-sentinel

cp /opt/redis-3.0.6/src/redis-sentinel /usr/local/redis/

cd /usr/local/redis/

./redis-sentinel sentinel.conf

3、查看节点状态

info replication

## widowns解压启动

```
redis-server.exe redis.windows.conf 
```

 安装 redis 到 windows 服务

```
redis-server --service-install redis.windows.conf
```

```
redis-server --service-start
redis-server --service-stop
redis-cli.exe -h 127.0.0.1 -p 6379 

Can't handle RDB format version 7
del 删除 /home/marco/dump.rdb
```

## 常用命令

```
keys * 查看所有键
keys apple* 匹配通配符的键
```

### key命令

| 命令      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| DEL       | 若键存在的情况下，该命令用于删除键                           |
| DUMP      | 用于序列化给定 key ，并返回被序列化的值                      |
| EXISTS    | 用于检查键是否存在，若存在则返回 1，否则返回 0               |
| EXPIRE    | 设置 key 的过期时间，以秒为单位                              |
| EXPIREAT  | 该命令与 EXPIRE 相似，用于为 key 设置过期时间，不同在于，它的时间参数值采用的是时间戳格式。 |
| KEYS      | 此命令用于查找与指定 pattern 匹配的 key                      |
| MOVE      | 将当前数据库中的 key 移动至指定的数据库中（默认存储为 0 库，可选 1-15中的任意库） |
| PERSIST   | 该命令用于删除 key 的过期时间，然后 key 将一直存在，不会过期 |
| PEXPIRE   | 设置 key 的过期，以毫秒为单位                                |
| RANDOMKEY | 从当前数据库中随机返回一个 key                               |
| RENAME    | 修改 key 的名称                                              |
| SCAN      | 基于游标的迭代器，用于迭代数据库中存在的所有键，cursor 指的是迭代游标 |
| TTL       | 用于检查 key 还剩多长时间过期，以秒为单位                    |
| TYPE      | 该命令用于获取 value 的数据类型                              |

### String 命令

| 命令                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [APPEND](http://c.biancheng.net/redis2/append.html)          | 该命令将 value 追加到 key 所存储值的末尾                     |
| [BITCOUNT](http://c.biancheng.net/redis2/bitcount.html)      | 该命令用于计算字符串中，被设置为 1 的比特位的数量。          |
| [DECR](http://c.biancheng.net/redis2/decr.html)              | 将 key 所存储的整数值减 1                                    |
| [DECRBY](http://c.biancheng.net/redis2/decrby.html)          | 将 key 所储存的值减去给定的递减值（decrement）               |
| [GET](http://c.biancheng.net/redis2/get.html)                | 用于检索指定键的值                                           |
| [GETBIT](http://c.biancheng.net/redis2/getbit.html)          | 对 key 所存储的字符串值，获取其指定偏移量上的位（bit）       |
| [GETRANGE](http://c.biancheng.net/redis2/getrange.html)      | 返回 key 中字符串值的子字符                                  |
| [GETSET](http://c.biancheng.net/redis2/getset.html)          | 将给定 key 的值设置为 value，并返回 key 的旧值               |
| [INCR](http://c.biancheng.net/redis2/incr.html)              | 将 key 所存储的整数值加 1                                    |
| [INCRBY](http://c.biancheng.net/redis2/incrby.html)          | 将 key 所储存的值加上给定的递增值（increment）               |
| [INCRBYFLOAT](http://c.biancheng.net/redis2/incrbyfloat.html) | 将 key 所储存的值加上指定的浮点递增值（increment）           |
| [MGET](http://c.biancheng.net/redis2/mget.html)              | 一次性获取一个或多个 key 所存储的值                          |
| [MSET](http://c.biancheng.net/redis2/mset.html)              | 该命令允许同时设置多个键值对                                 |
| [MSETNX](http://c.biancheng.net/redis2/msetnx.html)          | 当指定的 key 都不存在时，用于设置多个键值对                  |
| [SET](http://c.biancheng.net/redis2/set.html)                | 用于设定指定键的值                                           |
| [SETBIT](http://c.biancheng.net/redis2/setbit.html)          | 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)     |
| [SETEX](http://c.biancheng.net/redis2/setex.html)            | 将值 value 存储到 key中 ，并将 key 的过期时间设为 seconds (以秒为单位) |
| [STRLEN](http://c.biancheng.net/redis2/strlen.html)          | 返回 key 所储存的字符串值的长度                              |
| [SETNX](http://c.biancheng.net/redis2/setnx.html)            | 当 key 不存在时设置 key 的值                                 |
| [SETRANGE](http://c.biancheng.net/redis2/setrange.html)      | 从偏移量 offset 开始，使用指定的 value 覆盖的 key 所存储的部分字符串值 |

### Hash 命令

| 命令                                                  | 说明                                          |
| ----------------------------------------------------- | --------------------------------------------- |
| [HDEL](http://c.biancheng.net/redis2/hdel.html)       | 用于删除一个或多个哈希表字段                  |
| [HEXISTS](http://c.biancheng.net/redis2/hexists.html) | 用于确定哈希字段是否存在                      |
| [HGET](http://c.biancheng.net/redis2/hget.html)       | 获取存储在 key 中的哈希字段的值               |
| [HGETALL](http://c.biancheng.net/redis2/hgetall.html) | 获取存储在 key 中的所有哈希字段值             |
| [HINCRBY](http://c.biancheng.net/redis2/hincrby.html) | 为存储在 key 中的哈希表指定字段做整数增量运算 |
| [HKEYS](http://c.biancheng.net/redis2/hkeys.html)     | 获取存储在 key 中的哈希表的所有字段           |
| [HLEN](http://c.biancheng.net/redis2/hlen.html)       | 获取存储在 key 中的哈希表的字段数量           |
| [HSET](http://c.biancheng.net/redis2/hset.html)       | 用于设置存储在 key 中的哈希表字段的值         |
| [HVALS](http://c.biancheng.net/redis2/hvals.html)     | 用于获取哈希表中的所有值                      |

### List 命令

| 命令                                                        | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| [BLPOP](http://c.biancheng.net/redis2/blpop.html)           | 用于删除并返回列表中的第一个元素（头部操作），如果列表中没有元素，就会发生阻塞，直到列表等待超时或发现可弹出元素为止 |
| [BRPOP](http://c.biancheng.net/redis2/brpop.html)           | 用于删除并返回列表中的最后一个元素（尾部操作），如果列表中没有元素，就会发生阻塞，直到列表等待超时或发现可弹出元素为止 |
| [BRPOPLPUSH](http://c.biancheng.net/redis2/brpoplpush.html) | 从列表中取出最后一个元素，并插入到另一个列表的头部。如果列表中没有元素，就会发生阻塞，直到等待超时或发现可弹出元素时为止 |
| [LINDEX](http://c.biancheng.net/redis2/lindex_command.html) | 通过索引获取列表中的元素                                     |
| [LINSERT](http://c.biancheng.net/redis2/linsert.html)       | 指定列表中一个元素在它之前或之后插入另外一个元素             |
| [LLEN](http://c.biancheng.net/redis2/llen.html)             | 用于获取列表的长度                                           |
| [LPOP](http://c.biancheng.net/redis2/lpop.html)             | 从列表的头部弹出元素，默认为第一个元素                       |
| [LPUSH](http://c.biancheng.net/redis2/lpush.html)           | 在列表头部插入一个或者多个值                                 |
| [LPUSHX](http://c.biancheng.net/redis2/lpushx.html)         | 当储存列表的 key 存在时，用于将值插入到列表头部              |
| [LRANGE](http://c.biancheng.net/redis2/lrange.html)         | 获取列表指定范围内的元素                                     |
| [LREM](http://c.biancheng.net/redis2/lrem.html)             | 表示从列表中删除元素与 value 相等的元素。count 表示删除的数量，为 0 表示全部移除 |
| [LSET](http://c.biancheng.net/redis2/lset.html)             | 表示通过其索引设置列表中元素的值                             |
| [LTRIM](http://c.biancheng.net/redis2/ltrim.html)           | 保留列表中指定范围内的元素值                                 |

## ### Set 命令

| 命令                                                         | 说明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [SADD](http://c.biancheng.net/redis2/sadd.html)              | 向集合中添加一个或者多个元素，并且自动去重                  |
| [SCARD](http://c.biancheng.net/redis2/scard.html)            | 返回集合中元素的个数                                        |
| [SDIFF](http://c.biancheng.net/redis2/sdiff.html)            | 求两个或对多个集合的差集                                    |
| [SDIFFSTORE](http://c.biancheng.net/redis2/sdiffstore.html)  | 求两个集合或多个集合的差集，并将结果保存到指定的集合(key)中 |
| [SINTER](http://c.biancheng.net/redis2/sinter.html)          | 求两个或多个集合的交集                                      |
| [SINTERSTORE](http://c.biancheng.net/redis2/sinterstore.html) | 求两个或多个集合的交集，并将结果保存到指定的集合(key)中     |
| [SMEMBERS](http://c.biancheng.net/redis2/smembers.html)      | 查看集合中所有元素                                          |
| [SMOVE](http://c.biancheng.net/redis2/smove.html)            | 将集合中的元素移动到指定的集合中                            |
| [SPOP](http://c.biancheng.net/redis2/spop.html)              | 弹出指定数量的元素                                          |
| [SRANDMEMBER](http://c.biancheng.net/redis2/srandmember.html) | 随机从集合中返回指定数量的元素，默认返回 1个                |
| [SREM](http://c.biancheng.net/redis2/srem.html)              | 删除一个或者多个元素，若元素不存在则自动忽略                |
| [SUNION](http://c.biancheng.net/redis2/sunion.html)          | 求两个或者多个集合的并集                                    |
| [SUNIONSTORE](http://c.biancheng.net/redis2/sunsionstore.html) | 求两个或者多个集合的并集，并将结果保存到指定的集合(key)中   |

### Zset 命令

| 命令                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [ZADD](http://c.biancheng.net/redis2/zadd.html)              | 用于将一个或多个成员添加到有序集合中，或者更新已存在成员的 score 值 |
| [ZCARD](http://c.biancheng.net/redis2/zcard.html)            | 获取有序集合中成员的数量                                     |
| [ZCOUNT](http://c.biancheng.net/redis2/zcount.html)          | 用于统计有序集合中指定 score 值范围内的元素个数              |
| [ZINCRBY](http://c.biancheng.net/redis2/zincrby.html)        | 用于增加有序集合中成员的分值                                 |
| [ZINTERSTORE](http://c.biancheng.net/redis2/zinterstore.html) | 求两个或者多个有序集合的交集，并将所得结果存储在新的 key 中  |
| [ZRANGE](http://c.biancheng.net/redis2/zrange.html)          | 返回有序集合中指定索引区间内的成员数量                       |
| [ZRANGEBYLEX](http://c.biancheng.net/redis2/zrangebylex.html) | 返回有序集中指定字典区间内的成员数量                         |
| [ZRANGEBYSCORE](http://c.biancheng.net/redis2/zrangebyscore.html) | 返回有序集合中指定分数区间内的成员                           |
| [ZRANK](http://c.biancheng.net/redis2/zrank.html)            | 返回有序集合中指定成员的排名                                 |
| [ZREM](http://c.biancheng.net/redis2/zrem.html)              | 移除有序集合中的一个或多个成员                               |
| [ZREMRANGEBYRANK](http://c.biancheng.net/redis2/zremrangebyrank.html) | 移除有序集合中指定排名区间内的所有成员                       |
| [ZREMRANGEBYSCORE](http://c.biancheng.net/redis2/zremrangebyscore.html) | 移除有序集合中指定分数区间内的所有成员                       |
| [ZREVRANGE](http://c.biancheng.net/redis2/zrevrange.html)    | 返回有序集中指定区间内的成员，通过索引，分数从高到低         |
| [ZREVRANK](http://c.biancheng.net/redis2/zrevrank.html)      | 返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序 |
| [ZSCORE](http://c.biancheng.net/redis2/zscore.html)          | 返回有序集中，指定成员的分数值                               |
| [ZUNIONSTORE](http://c.biancheng.net/redis2/zunionstore.html) | 求两个或多个有序集合的并集，并将返回结果存储在新的 key 中    |

## 测试

![](G:\workspaces\wan\picture\test\redis1.png)

```
并发竞争key问题如何解决
1. multi

watch 防止写冲突 乐观锁 发现数据改变, 回滚事务

exec
2. 分布式锁
3.时间戳
4. 消息队列
“Redis 并发竞争” 问题就是高并发写同一个key时导致的值错误。

常用的解决方法：

乐观锁，注意不要在分片集群中使用
分布式锁，适合分布式系统环境
时间戳，适合有序场景
消息队列，串行化处理
```

```

```

> 一个命令可能无法排队，所以在调用 EXEC 之前可能会出错。例如，命令可能在语法上是错误的（参数数量错误，命令名称错误，......），或者可能存在一些严重的情况，例如内存不足的情况（如果服务器配置为使用 maxmemory 指令具有内存限制） .
> 调用 EXEC 后命令可能会失败，例如，因为我们对具有错误值的键执行了操作（例如对字符串值调用列表操作）

从 Redis 2.6.5 开始，服务器会在命令累积过程中检测到错误。 然后它将拒绝执行在 EXEC 期间返回错误的事务，丢弃该事务。

Redis < 2.6.5 的注意事项：在 Redis 2.6.5 之前，客户端需要通过检查排队命令的返回值来检测执行之前发生的错误：如果命令以 QUEUED 回复，则表示正确排队，否则 Redis 返回错误。 如果在排队命令时出现错误，大多数客户端将中止并丢弃事务。 否则，如果客户端选择继续事务，则 EXEC 命令将成功执行所有排队的命令，而不管先前的错误如何。

> `RedisTemplate`根据配置`RedisSerializer`的 s 转换键和值（参见[6.7 序列化程序](http://docs.spring.io/spring-data/redis/docs/current/reference/html/#redis:serializer)）。默认值为 `JdkSerializationRedisSerializer`.
>
> 给定字符串`name`，redis 中的实际键如下所示：
>
> ```
> GenericJackson2JsonRedisSerializer  : "name"
> JacksonJsonRedisSerializer:         : "name"
> Jackson2JsonRedisSerializer:        : "name"
> JdkSerializationRedisSerializer     : \xac\xed\x00\x05t\x00\x04name
> OxmSerializer with XStreamMarshaller: <string>name</string>
> StringRedisSerializer               : name
> ```

redis 持久化

> 持久性是指将数据写入持久存储，例如固态磁盘 (SSD)。Redis 本身提供了一系列持久化选项：
>
> - **RDB**（Redis 数据库）：RDB 持久性以指定的时间间隔执行数据集的时间点快照。
> - **AOF**（Append Only File）：AOF 持久化记录服务器接收到的每个写操作，在服务器启动时再次播放，重建原始数据集。命令使用与 Redis 协议本身相同的格式以仅附加方式记录。当日志变得太大时，Redis 能够在后台[重写日志。](https://redis.io/docs/manual/persistence/#log-rewriting)
> - **无持久性**：如果您愿意，您可以完全禁用持久性，如果您希望您的数据只要服务器正在运行就存在。
> - **RDB + AOF**：可以在同一个实例中结合 AOF 和 RDB。请注意，在这种情况下，当 Redis 重新启动时，AOF 文件将用于重建原始数据集，因为它保证是最完整的。

redis-cluster 根据hash值进行分区

redis-cluster 是弱的一致性  很可能不满足读自己的写的操作, 对于没看到负载倾斜和热点的解决方案 

> 一般解决方案有: 从主库读更新的内容 适用于个人购物车 和 个人的时间主线
>
> 在更新的1min内从主库读
>
> 时间戳

redis-cluster 满足全序广播

redis-bloom 是redis 企业版

JRedisBloom 实现布隆过滤器

| redis-modules-java | Java | Apache License 2 |
| ------------------ | ---- | ---------------- |



canal解决 缓存一致性
