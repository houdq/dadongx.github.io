---
title: springboot-docker
date: 2023-01-07 15:30:35
tags: docker
---
# docker run springboot

## 创建springboot 项目

创建项目 从 https://start.spring.io/

启动类配置如下：`
src/main/java/hello/Application.java
`

    package hello;
    
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    
    @SpringBootApplication
    @RestController
    public class DemoApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(DemoApplication.class, args);
        }
    
        //return current time
        @RequestMapping("/time")
        public String time() {
            return new Date().toString();
        }
    
    }

## docker 启动
### dockerfile 编写
```dockerfile
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

1. 将app.jar拷贝到容器
2. 引用 jdk

### build&run

`docker build -t ddx/demo`

```sh
➜  ~ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ddx/demo     latest    1b4b076fd19f   2 hours ago   122MB
mysql        latest    7484689f290f   4 weeks ago   538MB
jenkins      2.60.3    cd14cecfdb3a   4 years ago   696MB

```

`docker run -p 8080:8080 `

```sh
➜  ~ docker ps
CONTAINER ID   IMAGE      COMMAND                CREATED             STATUS             PORTS                    NAMES
62fa2f9c4bfc   ddx/demo   "java -jar /app.jar"   About an hour ago   Up About an hour   0.0.0.0:8080->8080/tcp hardcore_zhukovsky
```

访问 localhost:8080/time

    ➜  ~ curl localhost:8080/time
    Fri Jan 06 06:18:31 GMT 2023%

本文参考： https://spring.io/guides/gs/spring-boot-docker/


