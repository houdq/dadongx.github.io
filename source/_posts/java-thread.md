---
title: java如何创建多线程?
date: 2023-03-14 16:35:40
tags: 多线程
categories: 技术
toc: ture

---
## 继承 Thread,重新 run

```java
    /**
     * 继承 Thread 类
     */
    class MyThread extends Thread {
        @Override
        public void run() {
            System.out.println("线程名" + Thread.currentThread().getName() + ",开始运行");
        }
    }

```
## 实现 Runable+重写 run

```java
  /**
     * 实现  Runnable 接口
     */
    class MyRunnable implements Runnable {
        @Override
        public void run() {
            System.out.println("线程名" + Thread.currentThread().getName() + ",开始运行");
        }
    }
```
## 实现 Callable 接口重写 call 方法
获取返回值
```java
    /**
     * 实现 Callable 接口 获取返回值
     */
    class MyCallable implements Callable {
        @Override
        public Object call() throws Exception {
            System.out.println("线程名" + Thread.currentThread().getName() + ",开始运行");
            return Thread.currentThread().getName();
        }
    }
```
	
## new Thread+lamda 表达式
```java
        /**
         * 创建 Thread 对象 lambda 表达式
         */
        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("线程名" + Thread.currentThread().getName() + ",开始运行");
            }
        });

```
## 线程池

```java
   /**
     * 基于线程池创建线程
     */
    class MyThreadFactory implements ThreadFactory {
        @Override
        public Thread newThread(Runnable r) {
            return null;
        }
    }
```