#### 缓存穿透

缓存穿透就是大量请求得key根本不存在缓存中，导致请求直接到了数据库上，根本没有经过缓存这一层

![缓存穿透情况](../images/缓存穿透情况.png)

##### 解决方案

做好基本参数校验，不合法的参数请求直接抛出异常信息返回给客户端

1. ##### 缓存无效Key

   如果缓存和数据库都查不到某个key得数据就写一个到Redis中去并设置过期时间

   ```shell
   SET key value EX 10086
   ```

   可以解决请求的key变化不频繁得情况，尽量将无效的key得过期时间设置短一点

   ```java
   public Objec getObjectInclNullById(Integer id){
   	//从缓存中获取数据
   	Object cacheValue = cache.get(id);
   	//缓存为空
   	if(cacheValue == null){
   		//从数据库中获取
   		Object storageValue = storage.get(key);
   		//缓存空对象
   		cache.set(key,storageValue);
   		//如果存储数据为空，需要设置一个过期时间
   		if (storageValue == null){
   			//必须设置过期时间，否则有被攻击得风险
   			cache.expire(key,60*5);
   		}
   		return storageValue;
   	}
   	return cacheValue;
   }
   ```

2. ##### 布隆过滤器

   通过布隆过滤器可以非常方便地判断一个给定数据是否存在于海量数据中。

   把所有可能存在的请求的值都存放在布隆过滤器中，当用户请求过来，先判断用户发来的请求的值是否存在于布隆过滤器中，不存在的话，直接返回参数错误信息给客户端，存在的话才会走下面的流程

   ![布隆过滤器](../images/布隆过滤器处理.png)

   布隆过滤器说某个元素存在，小概率会误判。布隆过滤器说某个元素不在，那么这个元素一定不在

   

   