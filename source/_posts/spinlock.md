---
title:  java 自旋锁 SpinLock
date: 2023-02-25 12:17:26
tags: [并发编程,多线程]
categories: 技术
---
## 含义
线程等待加锁时，**不会阻塞**，**不会进入等待状态**，**而是保持运行状态**。大致的思路是：让当前线程不停地的在循环体内执行，当循环的条件被其他线程改变时才能进入临界区。

## 优势
- 避免死锁
自旋锁不会让线程阻塞或等待，也就不需要唤醒，所以可以避免产生死锁；
- 提高性能
 减少上下文切换次数,提高效率.

 ## 缺点

- 在等待锁时进入循环会占用CPU，若等待的线程很多，对CPU的消耗会比较大；

- 不适合需要长时间等待的任务或线程；
- 不适合大量线程等待的场景。

## 适用场景
- 等待时间比较短的任务中；
- 线程数量不太多的应用中；
- 当等待时间长或线程数量很大时，可以使用其他锁（比如：可重入锁）。

## java 实现

```
public class SpinkLock {
    
    // 是否占用的标志
    private AtomicBoolean occupied = new AtomicBoolean(false);

    public void lock() {
        // 使用自旋锁
        while (occupied.getAndSet(true)) {
        }
    }

    public void unlock() {
        occupied.set(false);
    }
}
```