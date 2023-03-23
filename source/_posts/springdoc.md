---
title: SpringBoot 集成 OpenAPI
date: 2023-03-07 10:17:38
tags: [openapi,swagger3]
categories: 技术
toc: true
---
## 1. 项目介绍
本项目是一个基于SpringBoot的项目，用于演示如何使用SpringBoot集成open-api，包括swagger3和springdoc。

## 版本信息

- jdk版本：openjdk19
- springboot版本：3.0.4.RELEASE
- springdoc版本：2.0.2

## 简单步骤


### 添加依赖
    
```xml
<dependency>
  <groupId>org.springdoc</groupId>
  <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
  <version>2.0.2</version>
</dependency>

```



### 编写controller

```
 @Operation(summary = "Get specific user object by it's id.")
    @GetMapping("/users/{id}")
    public User user(@Parameter(description = "id of the user.") @PathVariable("id") long id) {

        User user = new User();
        user.setName("xxx");
        return user;
    }
```
使用 openapi 的好处就是不需要额外的额皮质,使用swagger3的时候会增加 config 这里不需要.
### 访问地址:
默认地址

```
# swagger-ui custom path
springdoc.swagger-ui.path=/swagger-ui.html

```

直接访问
`http://localhost:8080/swagger-ui/index.html `效果如下:

![image](https://user-images.githubusercontent.com/9412449/223302078-7e443ea2-8bc0-49bb-ad23-a12046e3a290.png)
