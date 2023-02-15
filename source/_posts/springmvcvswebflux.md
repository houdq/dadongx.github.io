---
title: springmvcvswebflux
date: 2023-01-06 15:52:44
tags: [springmvc,weblux]
---

Spring WebFlux 和 Spring MVC 对比分析

什么是 Spring WebFlux

Spring MVC is built on the Servlet API and uses a synchronous blocking I/O architecture whth a one-request-per-thread model.

Spring MVC 构建于 Servlet API 之上，使用的是同步阻塞式 I/O 模型，什么是同步阻塞式 I/O 模型呢？就是说，每一个请求对应一个线程去处理。



Spring WebFlux is a non-blocking web framework built from the ground up to take advantage of multi-core, next-generation processors and handle massive numbers of concurrent connections.

Spring WebFlux 是一个异步非阻塞式的 Web 框架，它能够充分利用多核 CPU 的硬件资源去处理大量的并发请求。

WebFlux 的优势&提升性能?



Reactive and non-blocking generally do not make applications run faster.

WebFlux 并不能使接口的响应时间缩短，它仅仅能够提升吞吐量和伸缩性。

WebFlux 应用场景

PS: IO 密集型包括：磁盘IO密集型, 网络IO密集型，微服务网关就属于网络 IO 密集型，使用异步非阻塞式编程模型，能够显著地提升网关对下游服务转发的吞吐量。







选 WebFlux 还是 Spring MVC?

WebFlux 不是 Spring MVC 的替代方案！



首先是吞吐量

随着每个请求的被处理时间越长、并发请求的量级越大，WebFlux 相比 SpringMVC 的整体吞吐量高的越多，平均的请求响应时间越短。如下图所示



吞吐量大了，意味着单位时间内可以处理的请求数变多了，比如原来 1w 个请求 10 秒处理完，现在 10w 个请求也是 10 秒处理完，就代表吞吐上去了。注意，是吞吐上去了，不代表单次请求快了，单次请求的速度和原来一样。
