---
title: js实现一个发布订阅
date: 2020-05-28 19:14:44
tags: JS JS基础 面试题 进阶
---

## js设计模式之发布-订阅模式

发布-订阅模式又叫观察者模式，它用来定义一种一对多的依赖关系。当某个对象发生改变的时候，所有依赖于它的对象都将得到通知。在js中，通常用事件模型来代替传统的发布订阅模式（因为js没有类，可以直接传递函数）。



## 发布订阅模式的作用

  **第一点**广泛用于异步编程中，这是一种代替传统回调函数的手段。比如我们监听异步请求的success和error事件。当事件来临 的时候，发布一个状态，那么对此感兴趣的订阅者就会收到这个状态并执行相关操作。
  
  **第二点**在程序方面带来的好处是可以改变对象之间的硬编码的通知机制。一个对象不再显式地去调用另外一个对象的某个接口。发布订阅模式将两个对象松耦合地联系在一起，虽然不清除彼此细节，但并不影响彼此通信。无论发布者还是订阅者发生了变化，只要它们之间的约定没有变，就没有关系。
  

## 常见的订阅发布模式--DOM事件

window.addEventListener就是一个典型的例子。
```
  document.body.addEventListener('click', fn1);
  document.body.addEventListener('click', fn2);
  document.body.addEventListener('click', fn3);
```

用户可能会点击页面，但不知道什么时候点击。所以我们订阅body的click事件，当body被点击的时候，body节点便会向订阅者发布这个消息。

当然我们还可以随意移除订阅者，通过removeEventListener事件。

## 实现一个简单的发布订阅模式

除了内置的DOM事件，我们还会经常实现一些自定义的事件，这种依靠自定义事件完成的发布-订阅模式可以用于任何js的代码中。现在来实现一个简单的发布订阅模式。

- 首先需要一个发布者对象
- 发布者需要维护一个缓存队列，用于存放订阅对象的订阅回调
- 订阅者可以向事件列表中添加一个事件 表示订阅
- 发布消息时 遍历事件列表 去执行所有事件

```
  class CustomEvent {
    private clientList = [] // 回调列表

    constructor() {
      
    }

    // 订阅通知
    listen(fn: () => void) {
      this.clientList.push(fn)
    }

    // 发送通知
    trigger(...args) {
      this.clientList.forEach(fn => fn(args))
    }
  }
```

但是，上面的代码有一个问题，没有区分订阅的事件类型,并且没有取消订阅的功能

## 发布订阅的通用实现


```
  class CustomEvent {
    private clientList = {}

    constructor() {

    }

    // 订阅通知
    addListener(type: string, fn: (...args: any) => void) {
      if (!this.clientList[type]) {
        this.clientList[type] = []
      }
      this.clientList[type].push(fn)
    }

    // 取消订阅
    removeListener(type) {
      if(!type){
        this.clientList = {}
      }
      this.clientList[type] = []
    }

    // 发送通知
    trigger(type, ...args) {
      const fns = this.clientList[type]
      if (!fns || fns.length <= 0) {
        return
      }
      fns.forEach(fn => {
        fn.apply(this, args)
      });
    }
  }
```

## 小结

发布订阅者模式在实际开发中非常有用。

发布订阅的优点非常明显，一是时间上的解耦，而是对象间的解耦。

- 时间上的解耦: 在异步编程中，由于无法确定异步加载的时间，有可能订阅事件的模块还没有初始化完毕而异步加载就完成了，发布者就已经发布事件了。通过发布订阅模式，可以将发布者的事件提前保存起来，等到发布者加载完毕再执行。
- 对象间的解耦：发布订阅模式中，发布者和订阅者可以不必知道对方的存在，而是通过中介对象来通信。

发布订阅模式还可以用来帮助实现一些别的设计模式，比如中介者模式。从架构上看，无论是MVC还是MVVM，都少不了发布订阅模式的参与，而且js语言本身也是一门基于事件驱动的语言。

当然，发布订阅模式也不是没有缺点。

- 创建订阅者本身需要一定的时间和内存，而当你订阅一个消息后，也许此消息最后都未发生，但这个订阅者会始终存在于内存中。
- 另外，发布订阅模式将对象间完全解耦，如果过度使用的话，对象和对象之间的必要联系就会被掩盖，会导致程序难以追踪和理解。

## 参考文章

[js设计模式之发布-订阅模式](https://juejin.im/post/5c44236be51d4511dc72db58)