---
title: GCD基础
date: 2020-03-04 11:54:05
tags: GCD 多线程 iOS
---

## Dispatch
通过提交工作以分派系统管理的队列，在多核硬件上同时执行代码。

#### 队列和任务
[DispatchQueue](https://developer.apple.com/documentation/dispatch/dispatchqueue)：用于管理各线程上队列的对象。
- [main](https://developer.apple.com/documentation/dispatch/dispatchqueue/1781006-main)：主线程上的调度队列
```
DispatchQueue.main.async { 
    // 回到主线程
}
```
- [global(qos: DispatchQoS.QoSClass) -> DispatchQueue](https://developer.apple.com/documentation/dispatch/dispatchqueue/2300077-global)：返回具有指定优先级的全局系统队列。
```
let queue = DispatchQueue.global(qos: .default)
queue.async {
    // 异步执行（子线程）
}

queue.sync { 
    // 同步执行（主线程）
}
```
- [init(label: String, qos: DispatchQoS = .unspecified, attributes: DispatchQueue.Attributes = [], autoreleaseFrequency: DispatchQueue.AutoreleaseFrequency = .inherit, target: DispatchQueue? = nil)](https://developer.apple.com/documentation/dispatch/dispatchqueue/2300059-init)：创建一个新的调度队列
```
let queue = DispatchQueue(label: "cn.marbu.demo", qos: .unspecified, attributes: [], autoreleaseFrequency: .inherit, target: nil)
queue.async {
    // 异步执行（子线程）
}

queue.sync { 
    // 同步执行（主线程）
}
```

异步执行任务
- async
```
let queue = DispatchQueue(label: "cn.marbu.demo")
queue.async {
    // 异步执行
}
queue.asyncAfter(deadline: .now() + 1) {
    // 延迟1秒异步执行
}
```

同步执行任务
- sync
```
let queue = DispatchQueue(label: "cn.marbu.demo")
queue.sync { 
    // 同步执行	
}
let result = queue.sync {
    // 同步执行
    return "Result"
}
```

[DispatchWorkItem](https://developer.apple.com/documentation/dispatch/dispatchworkitem)：封装想要执行的工作，可以附加完成句柄或执行依赖项。
- 初始化和应用
```
let workItem = DispatchWorkItem {
    // Work
}
queue.async(execute: workItem)

let workItem1 = DispatchWorkItem(qos: .default, flags: []) {
    // Work
}
queue1.async(execute: workItem1)
```

[DispatchGroup](https://developer.apple.com/documentation/dispatch/dispatchgroup)：作为一个单元，监视一组任务。当所有工作项完成执行时，将执行其完成处理程序。也可以同步等待组中的所有任务完成执行。
- notify（一组任务完成时处理程序）
```
let group = DispatchGroup()
let queue = DispatchQueue(label: "cn.marbu.demo")

group.enter()
queue.async {
    // Work1...

    // Work1结束
    group.leave()
 }
        
group.enter()
queue.async {
    // Work2...

    // Work2结束
    group.leave()
}
        
group.notify(queue: queue) {
    // Work1和Work2已全部结束
}
```

#### 优先级
[DispatchQoS](https://developer.apple.com/documentation/dispatch/dispatchqos)：指定任务优先级，高优先级的工作会比低优先级的工作执行的更快。
- [userInteractive](https://developer.apple.com/documentation/dispatch/dispatchqos/1780708-userinteractive)：用户交互任务（例如动画，事件处理或更新应用程序的用户界面）类，与主线程优先级一致，优先级最高。
- [userInitiated](https://developer.apple.com/documentation/dispatch/dispatchqos/1780759-userinitiated)：用户积极使用您的应用的任务类，优先级第二。
- [default](https://developer.apple.com/documentation/dispatch/dispatchqos/2016062-default)：默认类，优先级第三。
- [utility](https://developer.apple.com/documentation/dispatch/dispatchqos/1780791-utility)：用户未主动跟踪的任务类，优先级第四。
- [background](https://developer.apple.com/documentation/dispatch/dispatchqos/1780981-background)：维护或清除任务类，优先级第五。
- [unspecified](https://developer.apple.com/documentation/dispatch/dispatchqos/1780703-unspecified)：没有质量类，优先级最低。
```
let queue = DispatchQueue(label: "cn.marbu.demo", qos: .default)
...
```

#### 系统事件监控
[DispatchSource](https://developer.apple.com/documentation/dispatch/dispatchsource)：协调特定低级系统事件（例如文件系统事件，计时器和UNIX信号）的处理的对象。
[DispatchIO](https://developer.apple.com/documentation/dispatch/dispatchio)：使用基于流或随机访问的语义管理文件描述符上的操作的对象。
[DispatchData](https://developer.apple.com/documentation/dispatch/dispatchdata)：一个对象，该对象管理基于内存的数据缓冲区，并将其公开为连续的内存块。
[DispatchDataIterator](https://developer.apple.com/documentation/dispatch/dispatchdataiterator)：调度数据对象内容上的逐字节迭代器。
#### 任务同步
[DispatchSemaphore](https://developer.apple.com/documentation/dispatch/dispatchsemaphore)：通过使用传统的计数信号量来控制跨多个执行上下文对资源的访问的对象。
#### 时间构造
[DispatchTime](https://developer.apple.com/documentation/dispatch/dispatchtime)：相对于默认时钟的时间点，具有纳秒精度。
[DispatchWallTime](https://developer.apple.com/documentation/dispatch/dispatchwalltime)：根据壁钟的绝对时间点，以微秒为单位。
[DispatchTimeInterval](https://developer.apple.com/documentation/dispatch/dispatchtimeinterval)：数秒，毫秒，微秒或纳秒。
[DispatchTimeoutResult](https://developer.apple.com/documentation/dispatch/dispatchtimeoutresult)：结果值，指示调度操作是否在指定时间之前完成。
[dispatch_time_t](https://developer.apple.com/documentation/dispatch/dispatch_time_t)：时间别名。
[DISPATCH_WALLTIME_NOW](https://developer.apple.com/documentation/dispatch/dispatch_walltime_now)：当前时间。
#### 调度对象
[DispatchObject](https://developer.apple.com/documentation/dispatch/dispatchobject)：大多数调度类型的基类。
[DispatchPredicate](https://developer.apple.com/documentation/dispatch/dispatchpredicate)：在给定执行上下文中进行评估的逻辑条件。
[dispatchPrecondition(condition: () -> DispatchPredicate)](https://developer.apple.com/documentation/dispatch/1780605-dispatchprecondition)：检查进一步执行所需的调度条件。