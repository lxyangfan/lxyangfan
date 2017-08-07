title: ReactiveX 学习一：简介
date: 2017-8-5
tags:
- ReactiveX
- Rx
----

## 简介

ReactiveX 是为 Reactive Extentions的缩写，又简称为Rx。是由微软公司的架构师Erik Meijer领导的团队开发，在2012年11月开源。

Rx是一种编程模型，为了异步事件编程提供统一的接口（函数），目前已经支持很多流行的语言，如 RxJava和RxJs。

我因为在Angular开发中，接触了RxJs（使用Observable获取网络数据），所以需要学习Rx。

引用来自于Rx社区ReactiveX.io，对Rx的定义：
> Rx是一个使用**可观察数据流进行异步编程**的编程接口，ReactiveX结合了观察者模式、迭代器模式和函数式编程的精华。


## Rx 编程模式

- 观察者模式
    - 数据的生产者，事件或者数据流被视作 **可观察对象Observable**
    - 数据流的消费者，或者称作**监听对象Subscriber**，实现对数据的具体操作
    - 生产者可以向监听对象发送消息，如事件完成（completed）和异常（failed），监听者实现相应的处理逻辑
    - 使用Observable还有优势，可以在异步的数据流中嵌套异步操作。

实现Rx需要考虑如下问题：

>- 它能与调用者在同一线程同步执行吗？
>- 它能异步地在单独的线程执行吗？
>- 它会将工作分发到多个线程，返回数据的顺序是任意的吗？
>- 它使用Actor模式而不是线程池吗？
>- 它使用NIO和事件循环执行异步网络访问吗？
>- 它使用事件循环将工作线程从回调线程分离出来吗？

Rx 底层实现是透明无偏见的，对于使用者来说，无需关注底层实现。

## Observable 对象

<div style="width:60%;position:center;">
    <img src="https://mcxiaoke.gitbooks.io/rxdocs/content/images/legend.png" />
</div>

上图中，最上面的横线代表一个Observable的数据流的时间线，线上的一个个对象item表示由Observable发送的数据。最后的竖线表示Observable已经成功结束。

Observable到中间的方框，表示Observable数据项经历的变换，其中上图的变换是flip，表示翻转。因此经过此转换后的输出数据都是翻转后的item.

如果因为某些原因，Observable异常终止了，那么表示正常结束的竖线就会由'X'代替。

## 参考资料

[RxDocs](https://mcxiaoke.gitbooks.io/rxdocs/content/Intro.html)