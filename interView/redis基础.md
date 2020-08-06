五种数据类型：String、List、Hash、Set和ZSet

#### String

String表示的是一个可变的字节数组，初始化字符串的内容，可以拿到字符串的长度，可以获取String的子串，可以覆盖String的子串内容，可以追加子串

Redis的字符串是动态字符串，是可以修改的字符串，内部结构实现上类似于Java的ArrayList，采用预分配冗余空间的方式来减少内存的频繁分配

```redis
初始化字符串
set ireader ireader beijing.zhangyue.keji.gufen.youxian.gongsi
获取字符串
get ireader
获取字符串的长度
strlen ireader
获取子串【开始位置-结束位置】
getrange ireader 28 34
覆盖子串
setrang ireader 28 wooxian
追加子串
append ireader .hao
```

计数器 如果字符串的内容是一个整数，那么还可以将字符串当成计数器来使用

过期和删除：

- del指令进行主动删除
- 使用expire指令设置过期时间，自动删除
- ttl指令获取字符串的寿命

```redis
expire ireader  60
```

#### List

列表的存储结构用的是链表而不是数组，链表是双向链表

**列队/堆栈** 链表可以从表头和表尾追加和移除元素，结合使用rpush/rpop/lpush/lpop四条指令

```redis
# 右进左出
> rpush ireader go
(integer) 1
> rpush ireader java python
(integer) 3
> lpop ireader
"go"
> lpop ireader
"java"
> lpop ireader
"python"
# 左进右出
> lpush ireader go java python
(integer) 3
> rpop ireader
"go"
...
# 右进右出
> rpush ireader go java python
(integer) 3
> rpop ireader 
"python"
...
# 左进左出
> lpush ireader go java python
(integer) 3
> lpop ireader
"python"
...
```

