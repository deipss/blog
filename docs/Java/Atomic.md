---
layout: default
title: Atomic
parent: Java
last_modified_date: 2025-05-25
---

# Atomic类

---

### 🛠 原句检查：

> Give me a guide of Atomic in Java incudeing implementation, using, inner control and so on.

### ✅ 修改建议：

> Please give me a guide to Atomic classes in Java, including their implementation, usage, internal control, and so on.

或者更自然一点：

> Could you provide a guide to Atomic classes in Java, covering their implementation, usage, internal mechanisms, etc.?

---

下面我给你详细讲解一下 Java 中的 **Atomic 类**，包括它们的实现原理、使用方式和内部控制机制。

---

# Atomic 类在 Java 中的全面指南

---

## 1. Atomic 类简介

Java 的 `java.util.concurrent.atomic` 包提供了一系列原子操作类，称为 **Atomic 类**。这些类支持在多线程环境下无锁（lock-free）的线程安全操作，常用于实现高性能的并发程序。

---

## 2. 常见的 Atomic 类

| 类名                          | 作用                  |
| --------------------------- | ------------------- |
| `AtomicInteger`             | 原子操作的整数变量           |
| `AtomicLong`                | 原子操作的长整数变量          |
| `AtomicBoolean`             | 原子操作的布尔变量           |
| `AtomicReference<V>`        | 原子操作的对象引用           |
| `AtomicStampedReference<V>` | 带版本戳的原子引用，解决 ABA 问题 |
| `AtomicIntegerArray`        | 原子操作的整数数组           |
| `AtomicLongArray`           | 原子操作的长整型数组          |
| `AtomicReferenceArray<E>`   | 原子操作的对象数组           |

---

## 3. 原理与实现

* **底层依赖**
  这些类底层通常依赖于 **CPU 的原子指令（CAS，Compare-And-Swap）**，通过 JVM 的 `Unsafe` 类调用操作系统提供的原子操作指令。

* **无锁设计**
  Atomic 类使用 CAS 操作不断尝试更新变量，直到成功，不需要使用传统的锁机制，因此性能较高且避免死锁。

---

## 4. 主要方法及用法

以 `AtomicInteger` 为例，常用方法：

| 方法名                                     | 作用                                |
| --------------------------------------- | --------------------------------- |
| `get()`                                 | 获取当前值                             |
| `set(int newValue)`                     | 设置新值                              |
| `lazySet(int newValue)`                 | 延迟设置新值，性能更优但不保证立即可见               |
| `compareAndSet(int expect, int update)` | CAS 操作，如果当前值等于 expect，则更新为 update |
| `getAndIncrement()`                     | 原子递增，返回递增前的值                      |
| `incrementAndGet()`                     | 原子递增，返回递增后的值                      |
| `getAndAdd(int delta)`                  | 原子增加指定值，返回增加前的值                   |

---

### 使用示例：

```java
AtomicInteger atomicInt = new AtomicInteger(0);

// 原子递增
int oldValue = atomicInt.getAndIncrement();
int newValue = atomicInt.incrementAndGet();

// CAS 操作
boolean updated = atomicInt.compareAndSet(1, 5);

System.out.println("oldValue: " + oldValue);
System.out.println("newValue: " + newValue);
System.out.println("updated: " + updated);
```

---

## 5. 内部控制机制

* **CAS（Compare-And-Swap）**
  是一种无锁的原子操作指令。
  大致流程是：

  1. 读取变量的当前值（V）
  2. 比较变量的值是否是预期值（expect）
  3. 如果是，则原子地将变量更新为新值（update）
  4. 如果不是，则重试

* **ABA 问题**
  CAS 有时会遇到 ABA 问题：变量从 A 变为 B，又变回 A，CAS 仍然认为变量未变。
  解决方案：使用 `AtomicStampedReference`，带版本号的原子引用。

* **内存可见性**
  `Atomic` 类的操作都保证了内存的 **可见性** 和 **有序性**，避免了普通变量多线程下的读写问题。

---

## 6. 使用场景

* 计数器（如并发计数、连接数）
* 状态标志（布尔值的原子切换）
* 实现无锁数据结构（栈、队列）
* 替代同步锁，减少性能开销

---

## 7. 注意事项

* Atomic 类不保证多个操作的原子性，只保证单个变量操作的原子性。复杂操作需要结合其他同步机制。
* 不适合用于需要对多个变量同时修改的场景。
* 虽然无锁，但在极端竞争情况下 CAS 可能失败重试，影响性能。

---

# CAS

好的！你这句话已经表达清楚了，我稍微帮你优化一下，使它更自然：

---

### 🛠 修改建议：

> I want to know the details of CAS in Java native code, and please give me an example of using Atomic classes.

---

下面我详细给你讲讲 **CAS（Compare-And-Swap）** 在 Java 本地代码中的实现细节，以及用 `AtomicInteger` 的简单示例。

---

# 1. CAS 在 Java 中的原理和本地代码实现

---

### CAS 是什么？

* **CAS**（比较并交换，Compare-And-Swap）是一种原子操作，用于实现无锁并发。
* 它包括三个操作数：

  * 内存地址（V）
  * 预期原值（A）
  * 新值（B）

操作步骤：

1. 比较内存地址 V 中的当前值是否等于 A（预期值）
2. 如果相等，则将 V 设置为 B（新值）
3. 如果不等，则不做修改，返回失败

这个过程是原子执行的。

---

### Java 中 CAS 的实现

Java 的 CAS 不是由 Java 语言直接实现的，而是通过 **JNI 调用本地操作系统或 CPU 指令** 来完成。

* Java 里调用的是 `sun.misc.Unsafe` 类中的 `compareAndSwapInt`、`compareAndSwapLong` 和 `compareAndSwapObject` 等方法。
* `Unsafe` 是 JVM 内部的类，可以直接访问底层内存和执行原子操作。
* 这些方法会调用 CPU 的 **原子指令**（如 x86 的 `cmpxchg` 指令）来完成 CAS。

---

### 以 x86 架构为例

* CAS 操作用的指令是 `LOCK CMPXCHG`，由 CPU 保证原子性。
* CPU 会在执行时锁住内存总线，防止其他线程访问该地址。
* 返回操作是否成功。

---

### 在 HotSpot JVM 中流程

1. Java 代码调用 `Unsafe.compareAndSwapInt`。
2. JVM 调用 JNI 层，将请求传递到底层操作系统。
3. 操作系统调用 CPU 原子指令执行 CAS。
4. 返回结果给 JVM，再返回给 Java 代码。

---

# 2. Atomic 类使用示例

下面用 `AtomicInteger` 举例，展示如何使用原子类实现线程安全的计数器。

```java
import java.util.concurrent.atomic.AtomicInteger;

public class AtomicExample {
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet(); // 原子递增
    }

    public int getCount() {
        return count.get();
    }

    public static void main(String[] args) throws InterruptedException {
        AtomicExample example = new AtomicExample();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                example.increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final count: " + example.getCount()); // 2000
    }
}
```

---

### 说明：

* `AtomicInteger` 保证了 `incrementAndGet()` 操作是原子的，多个线程并发调用不会导致数据竞争。
* 如果用普通的 `int` 变量，这种并发递增会导致结果不准确。


