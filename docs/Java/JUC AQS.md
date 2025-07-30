---
layout: default
title: JUC AQS
parent: Java
last_modified_date: 2025-07-13
---

### 🇨🇳 中文回答：

**AQS** 是 **AbstractQueuedSynchronizer** 的缩写，是 Java `java.util.concurrent` 包中的一个非常核心的同步框架基础类，简称 AQS。

---

# AQS 详解

---

## 1. AQS 的作用

* AQS 是一个用于构建锁和同步器的基础框架，简化了并发同步工具的开发。
* 它通过一个先进先出（FIFO）的等待队列来管理线程的阻塞和唤醒。
* Java 中很多同步器都是基于 AQS 实现的，比如：`ReentrantLock`、`Semaphore`、`CountDownLatch`、`ReentrantReadWriteLock` 等。

---

## 2. AQS 的核心结构

* **状态（state）变量**：表示同步状态，一般用 `int` 类型。具体含义由子类定义，比如锁的占用次数。
* **等待队列（CLH 队列）**：内部维护一个 FIFO 队列，管理所有等待线程。
* **独占模式和共享模式**：

  * **独占模式**（exclusive）：只有一个线程能占用资源（如 `ReentrantLock`）。
  * **共享模式**（shared）：多个线程可以共享资源（如 `Semaphore`、`CountDownLatch`）。

---

## 3. AQS 的工作原理

* 当线程请求资源时，尝试通过 `tryAcquire` 或 `tryAcquireShared` 方法获取资源。
```java
protected final boolean tryAcquire(int acquires) {
            final Thread current = Thread.currentThread();
            int c = getState();
            if (c == 0) {
                if (!hasQueuedPredecessors() &&
                    compareAndSetState(0, acquires)) {
                    setExclusiveOwnerThread(current);
                    return true;
                }
            }
            else if (current == getExclusiveOwnerThread()) {
                int nextc = c + acquires;
                if (nextc < 0)
                    throw new Error("Maximum lock count exceeded");
                setState(nextc);
                return true;
            }
            return false;
        } 
```
* 获取失败时，将当前线程包装成节点加入等待队列，线程阻塞等待。
* 释放资源时，调用 `release` 或 `releaseShared` 方法唤醒等待队列中的线程。

```java
protected final boolean tryRelease(int releases) {
            int c = getState() - releases;
            if (Thread.currentThread() != getExclusiveOwnerThread())
                throw new IllegalMonitorStateException();
            boolean free = false;
            if (c == 0) {
                free = true;
                setExclusiveOwnerThread(null);
            }
            setState(c);
            return free;
        }
```
* AQS 通过 **CAS 操作** 修改 `state` 状态，保证线程安全。

---

## 4. AQS 的重要方法

| 方法名                     | 说明               |
| ----------------------- | ---------------- |
| `tryAcquire(int arg)`   | 独占模式下尝试获取资源，子类实现 |
| `tryRelease(int arg)`   | 独占模式下释放资源，子类实现   |
| `tryAcquireShared(int)` | 共享模式下尝试获取资源，子类实现 |
| `tryReleaseShared(int)` | 共享模式下释放资源，子类实现   |
| `acquire(int)`          | 独占模式下获取资源，含阻塞等待  |
| `release(int)`          | 独占模式下释放资源，唤醒等待线程 |
| `acquireShared(int)`    | 共享模式下获取资源        |
| `releaseShared(int)`    | 共享模式下释放资源        |

---

## 5. 简单示意图

```
线程请求资源
     │
     ├─> 尝试获取资源（tryAcquire/tryAcquireShared）
     │      │
     │      ├─> 成功：直接执行
     │      └─> 失败：加入等待队列，阻塞线程
     │
线程释放资源（release/releaseShared）
     │
     └─> 唤醒等待队列中的线程
```

---

## 6. 应用示例

* **ReentrantLock** 使用 AQS 的独占模式管理锁的获取和释放。
* **Semaphore** 使用共享模式管理许可数量。
* **CountDownLatch** 使用共享模式管理计数器。

---

