---
title: 用springboot写一个 demo
date: 2021-02-18 14:36:28
tags: springboot
categories: 技术
toc: true
---

## 添加依赖
1. 创建一个 Maven 项目，并在 pom.xml 中添加以下依赖：

```
    <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
```
## 创建主程序
2. 创建一个 Spring Boot 应用程序类，例如 App.java，并使用 @SpringBootApplication 注解来声明它是一个 Spring Boot 应用程序：
```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }
}

```
## 创建 controller
3. 创建一个 Controller 类，例如 HelloController.java，并使用 @RestController 和 @RequestMapping 注解来声明一个 RESTful 接口：

```

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello World!";
    }
}

```

4. 运行应用程序，访问 http://localhost:8080/hello，你应该能看到浏览器显示 "Hello World!"。

```
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    @RestController
    public class HelloController {
        @RequestMapping("/hello")
        public String hello() {
            return "Hello World!";
        }
    }
    ```