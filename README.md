####  redis

##### redis常用的数据结构 
| 结构类型 | 结构存储的值 | 读写能力 |
| ------ | ------ | ------ |
| <a href='#string'>String</a> |  字符串，整数，浮点数 | 对字符串部分或者全部执行操作;对整数或者浮点数进行自增或者自减操作。 |
| <a href='#list'>list</a> | 链表，链表有多个节点组成，每个节点存储一个字符串 | 从链表的两端进行移除移入操作.根据偏移量进行链的修建操作，查询单个或者多个数据，根据值对数据进行查找移除 |
| Set | 无序,字符串，每个元素独一无二| 添加，移除，获取单个元素；检查一个元素是否存在；计算交集，并集，差集;随机获取元素|
|Hash|包含键值队的无序散列表|添加，获取，移除单个键值对，获取所有键值对|
|Zset|字符串与浮点数值有序映射，集合按照浮点数值进行排序，由小到大|增删改查单个数据，根据分值范围获取大部分数据|

- 各种数据常用命令
  - <a name='string' >字符串</a>

  |命令|用例以及描述|
  |------ | -------- |
  |INCR| INCR KEY-NAME : 将键存储值加1|
  |DECR| DECR KEY-NAME : 将键存储值减1|
  |INCRBY|INCRBY KEY-NAME : 将键存储值加number|
  |DECRBY|DECRBY KEY-NAME : 将键存储值减number|
  |INCRBYFLOAT|INCRBYFLOAT KEY-NAME : 将键存储值加number(浮点数)，version>2.6可用|

  - <a name='#list'>list</a>
 
  |命令|用例以及描述|
  |------ | -------- |
  |RPUSH| RPUSH KEY-NAME VALUE [ VALUE .....]: 将一个或多个值推入list的右端|
  |LPUSH| LPUSH KEY-NAME VALUE [ VALUE .....] : 将一个或多个值推入list的左端|
  |RPOP|RPOP KEY-NAME : 移除并返回list最右边的元素|
  |LPOP|LPOP KEY-NAME : 移除并返回list最左边的元素|
  |LINDEX|LINDEX KEY-NAME  OFFSET：返回偏移量为offset的元素，你可以理解为下标，但他不是下标|
  |RANGE|RANGE KEY-NAME  START END:返回偏移量在start以及end之间的所有元素，包括start和end|
  |LTRIM|LTRIM KEY-NAM  START END:修建list只保留移量在start以及end之间的所有元素，包括start和end|

  列表之间也可以进行数据转移，主要是使用以下几个命令

  |命令|用例以及描述|
  |------ | -------- |
  |RPUSH| RPUSH KEY-NAME VALUE [ VALUE .....]: 将一个或多个值推入list的右端|
  |LPUSH| LPUSH KEY-NAME VALUE [ VALUE .....] : 将一个或多个值推入list的左端|
  |RPOP|RPOP KEY-NAME : 移除并返回list最右边的元素|
  |LPOP|LPOP KEY-NAME : 移除并返回list最左边的元素|
  |LINDEX|LINDEX KEY-NAME  OFFSET：返回偏移量为offset的元素，你可以理解为下标，但他不是下标|
  |RANGE|RANGE KEY-NAME  START END:返回偏移量在start以及end之间的所有元素，包括start和end|
  |LTRIM|LTRIM KEY-NAM  START END:修建list只保留移量在start以及end之间的所有元素，包括start和end|

 
