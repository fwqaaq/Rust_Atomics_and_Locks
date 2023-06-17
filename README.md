# Rust Atomics and Locks

## [第一章：Rust 并发基础](./1_Basic_of_Rust_Concurrency.md)

* [Rust 中的线程](./1_Basic_of_Rust_Concurrency.md#rust-中的线程)
* [线程作用域](./1_Basic_of_Rust_Concurrency.md#线程作用域)
* [共享所有权以及引用计数](./1_Basic_of_Rust_Concurrency.md#共享所有权以及引用计数)
  * [Static](./1_Basic_of_Rust_Concurrency.md#static)
  * [泄漏（Leak）](./1_Basic_of_Rust_Concurrency.md#泄漏leak)
  * [引用计数](./1_Basic_of_Rust_Concurrency.md#引用计数)
* [借用和数据竞争](./1_Basic_of_Rust_Concurrency.md#借用和数据竞争)
* [内部可变性（Cell、RefCell、Mutex 以及 RwLock、Atomics、UnsafeCell）](./1_Basic_of_Rust_Concurrency.md#内部可变性)
* [线程安全：Send 和 Sync](./1_Basic_of_Rust_Concurrency.md#线程安全send-和-sync)
* [锁：Mutex 和 RwLock](./1_Basic_of_Rust_Concurrency.md#锁mutex-和-rwlock)
  * [Rust 的 Mutex](./1_Basic_of_Rust_Concurrency.md#rust-的-mutex)
  * [锁毒化](./1_Basic_of_Rust_Concurrency.md#锁毒化)
  * [Reader-Writer Lock](./1_Basic_of_Rust_Concurrency.md#reader-writer-lock)
* [等待：Parking 和条件变量](./1_Basic_of_Rust_Concurrency.md#等待-parking-和条件变量)
  * [Thread Parking](./1_Basic_of_Rust_Concurrency.md#thread-parking)
  * [条件变量](./1_Basic_of_Rust_Concurrency.md#条件变量)
* [总结](./1_Basic_of_Rust_Concurrency.md#总结)

## [第二章：Atomic](./2_Atomics.md)

* [Atomic 的加载和存储操作](./2_Atomics.md#atomic-的加载和存储操作)
  * [示例：停止标识](./2_Atomics.md#示例停止标识)
  * [示例：进度报道](./2_Atomics.md#示例进度报道)
    * [同步](./2_Atomics.md#同步)
  * [示例：惰性初始化](./2_Atomics.md#示例惰性初始化)
* [获取和修改操作](./2_Atomics.md#获取和修改操作)
  * [示例：来自多线程的进度报道](./2_Atomics.md#示例来自多线程的进度报道)
  * [示例：统计数据](./2_Atomics.md#示例统计数据)
  * [示例：ID 分配](./2_Atomics.md#示例id-分配)
* [compare-and-exchange 操作](./2_Atomics.md#compare-and-exchange-操作)
  * [示例：没有溢出的 ID 分配](./2_Atomics.md#示例没有溢出的-id-分配)
  * [示例：惰性一次性初始化](./2_Atomics.md#示例惰性一次性初始化)
* [总结](./2_Atomics.md#总结)

## [第三章：内存排序](./3_Memory_Ordering.md)

* [重排和优化](./3_Memory_Ordering.md#重排和优化)
* [内存模型](./3_Memory_Ordering.md#内存模型)
* [Happens-Before 关系](./3_Memory_Ordering.md#happens-before-关系)
  * [产生和加入](./3_Memory_Ordering.md#产生和加入)
* [Relaxed 排序](./3_Memory_Ordering.md#relaxed-排序)
* [Release 和 Acquire 排序](./3_Memory_Ordering.md#release-和-acquire-排序)
  * [示例：「锁」](./3_Memory_Ordering.md#示例锁)
  * [示例：使用间接的方式惰性初始化](./3_Memory_Ordering.md#示例使用间接的方式惰性初始化)
* [消费排序](./3_Memory_Ordering.md#消费排序)
* [顺序一致性排序](./3_Memory_Ordering.md#顺序一致性排序)
* [屏障（Fence）](./3_Memory_Ordering.md#屏障fence2)
* [常见的误解](./3_Memory_Ordering.md#常见的误解)
* [总结](./3_Memory_Ordering.md#总结)

## [第四章：构建我们自己的自旋锁](./4_Building_Our_Own_Spin_Lock.md)

* [一个最小实现](./4_Building_Our_Own_Spin_Lock.md#一个最小实现)
* [一个不安全的自旋锁](./4_Building_Our_Own_Spin_Lock.md#一个不安全的自旋锁)
* [使用锁守卫的安全接口](./4_Building_Our_Own_Spin_Lock.md#使用锁守卫的安全接口)
* [总结](./4_Building_Our_Own_Spin_Lock.md#总结)

## [第五章：构建我们自己的 Channel](./5_Building_Our_Own_Channels.md)

* [一个简单的以 mutex 为基础的 Channel](./5_Building_Our_Own_Channels.md#一个简单的以-mutex-为基础的-channel)
* [一个不安全的一次性 Channel](./5_Building_Our_Own_Channels.md#一个不安全的一次性-channel)
* [通过运行时检查来达到安全](./5_Building_Our_Own_Channels.md#通过运行时检查来达到安全)
* [通过类型来达到安全](./5_Building_Our_Own_Channels.md#通过类型来达到安全)
* [借用以避免分配](./5_Building_Our_Own_Channels.md#借用以避免分配)
* [阻塞](./5_Building_Our_Own_Channels.md#阻塞)
* [总结](./5_Building_Our_Own_Channels.md#总结)

## [第六章：构建我们自己的“Arc”](./6_Building_Our_Own_Arc.md)

* [基础的引用计数](./6_Building_Our_Own_Arc.md#基础的引用计数)
  * [测试它](./6_Building_Our_Own_Arc.md#测试它)
  * [可变性](./6_Building_Our_Own_Arc.md#可变性)
* [Weak 指针](./6_Building_Our_Own_Arc.md#weak-指针)
  * [测试它](./6_Building_Our_Own_Arc.md#测试它2)
  * [优化](./6_Building_Our_Own_Arc.md#优化)
* [总结](./6_Building_Our_Own_Arc.md#总结)

## [第七章：理解处理器](./7_Understanding_the_Processor.md)

* [处理器指令](./7_Understanding_the_Processor.md#处理器指令)
  * [加载和存储操作](./7_Understanding_the_Processor.md#加载和存储操作)
  * [读、修改、写操作](./7_Understanding_the_Processor.md#读修改写操作)
    * [x86 锁前缀](./7_Understanding_the_Processor.md#x86-锁前缀)
    * [x86 比较和交换指令](./7_Understanding_the_Processor.md#x86-比较和交换指令)
* [缓存](./7_Understanding_the_Processor.md#缓存)
  * [缓存一致性](./7_Understanding_the_Processor.md#缓存一致性)
    * [写入协议](./7_Understanding_the_Processor.md#写入协议)
    * [MESI 协议](./7_Understanding_the_Processor.md#mesi-协议)
  * [对性能的影响](./7_Understanding_the_Processor.md#对性能的影响)
* [重排](./7_Understanding_the_Processor.md#重排)
* [内存排序](./7_Understanding_the_Processor.md#内存排序)
  * [x86-64：强排序](./7_Understanding_the_Processor.md#x86-64强排序)
  * [ARM64：弱排序](./7_Understanding_the_Processor.md#arm64弱排序)
  * [一个实验](./7_Understanding_the_Processor.md#一个实验)
  * [内存屏障](./7_Understanding_the_Processor.md#内存屏障)
* [总结](./7_Understanding_the_Processor.md#总结)

## [第八章：操作系统原语](./8_Operating_System_Primitives.md)

* [使用内核接口](./8_Operating_System_Primitives.md#使用内核接口)
* [POSIX](./8_Operating_System_Primitives.md#posix)
  * [在 Rust 中包裹](./8_Operating_System_Primitives.md#在-rust-中包裹)
* [Linux](./8_Operating_System_Primitives.md#linux)
  * [Futex](./8_Operating_System_Primitives.md#futex)
  * [Futex 操作](./8_Operating_System_Primitives.md#futex-操作)
  * [优先继承 Futex 操作](./8_Operating_System_Primitives.md#优先继承-futex-操作)
* [macOS](./8_Operating_System_Primitives.md#macos)
  * [os_unfair_lock](./8_Operating_System_Primitives.md#os_unfair_lock)
* [Windows](./8_Operating_System_Primitives.md#windows)
  * [重量级内核对象](./8_Operating_System_Primitives.md#重量级内核对象)
  * [轻量级对象](./8_Operating_System_Primitives.md#轻量级对象)
    * [一个轻巧的读写锁](./8_Operating_System_Primitives.md#一个轻巧的读写锁)
  * [基于地址的等待](./8_Operating_System_Primitives.md#基于地址的等待)
* [总结](./8_Operating_System_Primitives.md#总结)

## [第九章：构建我们自己的「锁」](./9_Building_Our_Own_Locks.md)

* [Mutex](./9_Building_Our_Own_Locks.md#mutex)
  * [避免系统调用](./9_Building_Our_Own_Locks.md#避免系统调用)
  * [进一步优化](./9_Building_Our_Own_Locks.md#进一步优化)
  * [基准测试](./9_Building_Our_Own_Locks.md#基准测试)
* [条件变量](./9_Building_Our_Own_Locks.md#条件变量)
  * [避免系统调用2](./9_Building_Our_Own_Locks.md#避免系统调用2)
  * [避免虚假唤醒](./9_Building_Our_Own_Locks.md#避免虚假唤醒)
* [读写锁](./9_Building_Our_Own_Locks.md#读写锁)
  * [避免 writer 忙碌循环](./9_Building_Our_Own_Locks.md#避免-writer-忙碌循环)
  * [避免 writer 陷入饥饿](./9_Building_Our_Own_Locks.md#避免-writer-陷入饥饿)
* [总结](./9_Building_Our_Own_Locks.md#总结)

## [第十章：主意和灵感](./10_Ideas_and_Inspiration.md)

* [信号量](./10_Ideas_and_Inspiration.md#信号)
* [RCU](./10_Ideas_and_Inspiration.md#rcu)
* [无锁链表](./10_Ideas_and_Inspiration.md#无锁链表)
* [基于队列的锁](./10_Ideas_and_Inspiration.md#基于队列的锁)
* [基于 Parking 的锁](./10_Ideas_and_Inspiration.md#基于-parking-的锁)
* [顺序锁](./10_Ideas_and_Inspiration.md#顺序锁spinlock)
* [教学材料](./10_Ideas_and_Inspiration.md#教学材料)

注明：本文译自 <https://marabos.nl/atomics/inspiration.html#lock-free-linked-list>，若其它平台引用此翻译，也请注明出处。

翻译进行中...
