## redis配置：

##### 基础命令

1.```cd /usr/local/redis/bin/ && ./redis-cli```  链接redis

2.```select 1```  选择几号库,现在是选择一号库

3.```keys *```  查看所有的key值



##### string

1.```SET KEY value```  存入 key=>value

2.```GET KEY``` 获取key

3.```GETSET key value``` 将给定 key 的值设为 value ，并返回 key 的旧值(old value)



##### hash

1.```HDEL key field1 [field2] ```  删除一个或多个哈希表字段

2.```HGET key field1 [field2] ```  获取存储在哈希表中指定字段的值

3.```HGETALL key  ```  取在哈希表中指定 key 的所有字段和值

4.``` HMSET key field1 value1 [field2 value2 ] ``` 同时将多个 field-value (域-值)对设置到哈希表 key 中。





