---
title: 缓存的本质和缓存实践
date: 2023-02-20 14:04:35
tags: [cache,缓存]
categories: 技术
toc: true
---

## 为什么要用缓存?
### 缓存的本质
> 通俗理解计算机缓存,可以比喻成水库.



### CPU缓存和系统机构缓存

## 缓存编程实现
### 编程法
采用各种reis 客户端和 API.比如Jredis api

### Spring 注入

Spring Data Redis 是 Spring Data 家族的一个项目，它为 Spring 应用程序提供了与 Redis 数据存储交互的支持。Spring Data Redis 通过 RedisTemplate 和 RedisConnectionFactory 为 Redis 提供了高级的 Redis 操作接口。
- 添加依赖
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>

```

- RedisTemplate源码
```
@Autowired
private RedisTemplate<String, Object> redisTemplate;

public void setValue(String key, Object value) {
    redisTemplate.opsForValue().set(key, value);
}

public Object getValue(String key) {
    return redisTemplate.opsForValue().get(key);
}

```
-注入RedisTemplate
```

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Component;

@Component
public class RedisService {

    @Autowired
    private RedisTemplate<String, String> redisTemplate;

    public void setValue(String key, String value) {
        redisTemplate.opsForValue().set(key, value);
    }

    public String getValue(String key) {
        return redisTemplate.opsForValue().get(key);
    }
}
```

### 注解法
如果你用 springboot,使用 @Cacheable 注解来实现 Redis 缓存非常简单，您只需要按照以下步骤即可：

1. 添加依赖：首先，在 pom.xml 文件中添加 spring-boot-starter-cache 和 spring-boot-starter-data-redis 依赖。

2. 配置 Redis：在 application.properties 或 application.yml 文件中配置 Redis 连接信息。

3. 创建缓存配置：在您的应用程序中创建一个缓存配置类，并使用 @Configuration 和 @EnableCaching 注解进行标注。在这个类中，您可以使用 CacheManagerBuilder.build() 方法来创建一个 RedisCacheManager 对象。

4. 使用 @Cacheable：在需要缓存的方法上使用 @Cacheable 注解，指定缓存名称以及需要缓存的数据 key。
下面是一个使用 @Cacheable 注解来实现 Redis 缓存的示例：


```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    @Cacheable(value = "user", key = "#id")
    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }

    // 其他业务方法...
}
```
## 访问缓存的模式

### 双读双写
一般采用这种写法
![image](https://user-images.githubusercontent.com/9412449/220018370-696f2a8d-440e-4a83-8d97-c7d058a5b362.png)
## 异步更新
![image](https://user-images.githubusercontent.com/9412449/220019055-6353b1e1-80b4-473a-83d5-56df60182373.png)
## 串联模式
![image](https://user-images.githubusercontent.com/9412449/220019109-48d675d4-fd23-44b0-887f-67e11772df34.png)

<!--  -->
## 分片模式

### 客户端分片

### 代理分片

### 集群分片

## 迁移方案

### 平滑迁移

### 一致性哈希