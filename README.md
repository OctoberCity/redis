###  redis

#### redis常用的数据结构 
| 结构类型 | 结构存储的值 | 读写能力 |
| ------ | ------ | ------ |
| <a href='#string'>String</a> |  字符串，整数，浮点数 | 对字符串部分或者全部执行操作;对整数或者浮点数进行自增或者自减操作。 |
| <a href='#list'>list</a> | 链表，链表有多个节点组成，每个节点存储一个字符串 | 从链表的两端进行移除移入操作.根据偏移量进行链的修建操作，查询单个或者多个数据，根据值对数据进行查找移除 |
| <a href='#set'>set</a>| 无序,字符串，每个元素独一无二| 添加，移除，获取单个元素；检查一个元素是否存在；计算交集，并集，差集;随机获取元素|
|<a href='#hash'>hash</a>|包含键值队的无序散列表|添加，获取，移除单个键值对，获取所有键值对|
|<a href='#zset'>zset</a>|字符串与浮点数值有序映射，集合按照浮点数值进行排序，由小到大|增删改查单个数据，根据分值范围获取大部分数据|

- #### 各种数据常用命令
  - #### <a name='string' >字符串</a>
  |命令|用例以及描述|
  |------ | -------- |
  |INCR| INCR KEY-NAME : 将键存储值加1|
  |DECR| DECR KEY-NAME : 将键存储值减1|
  |INCRBY|INCRBY KEY-NAME : 将键存储值加number|
  |DECRBY|DECRBY KEY-NAME : 将键存储值减number|
  |INCRBYFLOAT|INCRBYFLOAT KEY-NAME : 将键存储值加number(浮点数)，version>2.6可用|

  - #### <a name='list'>list</a>
 
  |命令|用例以及描述|
  |------ | -------- |
  |RPUSH| RPUSH KEY-NAME VALUE [ VALUE .....]: 将一个或多个值推入list的右端|
  |LPUSH| LPUSH KEY-NAME VALUE [ VALUE .....] : 将一个或多个值推入list的左端|
  |RPOP|RPOP KEY-NAME : 移除并返回list最右边的元素|
  |LPOP|LPOP KEY-NAME : 移除并返回list最左边的元素|
  |LINDEX|LINDEX KEY-NAME  OFFSET：返回偏移量为offset的元素，你可以理解为下标，但他不是下标|
  |RANGE|RANGE KEY-NAME  START END:返回偏移量在start以及end之间的所有元素，包括start和end|
  |LTRIM|LTRIM KEY-NAM  START END:修建list只保留移量在start以及end之间的所有元素，包括start和end|

  > 列表之间也可以进行数据转移，并且可以执行等待阻塞命令知道list中有数据，主要是使用以下几个命令

  |命令|用例以及描述|
  |------ | -------- | 
  |BRPOP|BRPOP KEY-NAME [KEY-NAME .....] : 从第一个非空list中弹出最右端的元素或者等待timeout秒阻塞等待可弹出的元素|
  |BLPOP|BLPOP KEY-NAME [KEY-NAME .....] : 从第一个非空list中弹出最左端的元素或者等待timeout秒阻塞等待可弹出的元素|
  |RPOPLPUSH|RPOPLPUSH LIST1  LIST2：看名字，右出左进，从list1弹出最右端的数据并推入list2左端|
  |BRPOPLPUSH|RPOPLPUSH LIST1  LIST2 timeout：看名字，等待右出左进，从list1弹出最右端的数据并推入list2左端，如果list1没数据，就等待timeout秒阻塞等待可弹出的数据|
 
  - #### <a name='set'>set</a>
  |命令|用例描述|
  |---|---|
  |SADD| SADD KEY-NAME ITEM[ITEM....] : 添加一个或者多个元素，并返回实际添加的元素数量，因为添加的元素可能集合set中已经存在|
  |SREM| SREM KEY-NAME ITEM[ITEM....] : 移除一个或者多个元素，并返回移除的元素数量 |
  |SISMEMBER| SISMEMBER  KEY-NAME ITEM :判断是否存在item元素|
  |SCARD| SCARD KEY-NAME : 返回集合中元素的数量|
  |SMEMBERS|SMEMBERS KEY-NAME:返回集合所有的数量|
  |SRANDMEMBER|SRANDMEMBER KEY-NAME [COUNT]:当count>0 返回一个或者多个元素，元素不会重复，当count<0,元素可能会出现重复|
  |SPOP|SPOP KEY-NAME ：随机移除集合中的一个元素，并返回|
  |SMOVE|SMOVE SET1 SET2 ITEM : 将set1中的item 移除并添加set2中，success返回1，否则0|

  > 集合之间也可以进行操作，就和数学中的集合一样，存在交集并集等关系

  |命令|用例描述|
  |---|---|
  |SDIFF| SDIFF  KEY-NAME [KEY-NAME...] :返回我有其他集合没有的元素(差集)|
  |SDIFFSTORE| SDIFFSTORE  RESULTSET   KEY-NAME [KEY-NAME ....]:将我有其他集合没有的元素添加至RESULTSET|
  |SINTER|SINTER KEY-NAME [ KEY-NAME ....]:返回所有集合都有的元素(交集)|
  |SINTERSTORE|SINTERSTORE  RESULTSET KEY-NAME [KEY-NAME]:将所有集合都有的元素并且添加至RESULTSET|
  |SUNION|SUNION KEY-NAME  [ KEY-NAME ....]：返回所有集合的并集，将所有的集合元素合在一起，并且去除重复|
  |SUNIONSTORE|SUNIONSTORE RESULTSET KEY-NAME [KEY-NAME]：将所有集合的并集，添加至RESULTSET |

  - #### <a name='hash'>hash</a>
  hash散列数据结构是一个键中存储多个键值对
  |命令|用例描述|
  |---|---|
  |HMGET| HMGET KEY-NAME KEY[KEY....] : 获取散列中一个或者多个key的值 |
  |HMSET| HMSET KEY-NAME KEY value [KEY value....] : 设置一个或者多个key-value |
  |HDEL| HDEL  KEY-NAME key[key ...] :删除散列中一个或者多个键值对，成功之后返回其数量 |
  |HLEN| HLEN KEY-NAME : 返回散列键值对的数量  |
  |HEXITS|HEXITS KEY-NAME key :判断散列中是否存在某个键值对  |
  |HKEYS|HKEYS KEY-NAME : 返回散列中所有的的key |
  |HVALS|HVALS KEY-NAME  :返回散列中所有的value|
  |HGETALL|HGETALL KEY-NAME  :返回所有的键值对，如果返回的数据太大不建议使用  |
  |HINCRBY|HINCRBY  KEY-NAME key increment : 给散列中键=key的值加上increment |
  |HINCRBYFLOAT|HINCRBYFLOAT KEY-NAME key increment : 给散列中键=key的值加上incremen(浮点)   |

  - #### <a name='zset'>zset</a>
  有序集合与集合最主要的区别就是根据value排序了,且数据结构有些键值对的映射关系！下面是一些常用的命令，而对于有序集合的集合操作命令就不说了
  |命令|用例描述|
  |---|---|
  |ZADD| ZADD KEY-NAME SCORE MEMBER[SCORE MEMBER....] :  向集合中添加带分值的成员 |
  |ZREM| ZREM KEY-NAME  MEMBER [MEMBER....] :删除指定成员，并返回删除数量|
  |ZCARD| ZCARD  KEY-NAME   : 返回集合中成员数量 |
  |ZINCRBY| ZINCRBY KEY-NAME INCREMENT MEMBER :  将成员MEMBER 的分值加INCREMENT  |
  |ZCOUNT|ZCOUNT KEY-NAME MIN MAX  :返回分值在min-max之间的成员数量  |
  |ZRANK|ZRANK KEY-NAME MEMBER : 返回MEMBER成员在集合的排序|
  |ZSCORE|ZSCORE KEY-NAME  MEMBER :返回MEMBER成员在集合的的分值|
  |ZRANGE|ZRANGE KEY-NAME START END  [WITHSCORES]  :返回分值在start-end之间的成员,如果添加WITHSCORES选项那么连score分值也一起返回|
 
 
