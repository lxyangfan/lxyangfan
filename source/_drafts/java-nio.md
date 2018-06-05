title: Java NIO 学习
date: 2018-06-04
tages:
- NIO
- Java
-----


### 前言

Java NIO (New IO) 是基于事件模型， 事件驱动型。当有IO准备好的事件发生时，切换回调函数，效率会高。以上是我最粗浅的理解。

它主要的概念包括：Channel、Buffer、Selector。Channel 和 Buffer 类似于数据流的思想，但是跟数据流有如下区别：
- Channel 可以代表 文件、UDP报文、TCP报文（SocketChannel\ServerSocketChannel）；
- Buffer可以写入Channel或者从Channel读取，而流打开时候需要确认是输入还是输出流；
- Channel支持异步读取或者写入Buffer

### NIO 基础

#### Buffer

Buffer 从字面上就可以理解是一个内存缓冲区，可以接受从Channel读入操作和写内容到Channel操作。

Buffer 有3个重要的参数：
- capacity： 表示已分配的内存容量；
- position
- limit

其中position和limit参数，在读操作和写操作上是有不同的含义：
- 读操作：limit表示Buffer能从Channel读的最大的下标，值为 capacity-1, position表示当前读的下标；
- 写操作：limit表示当前Buffer能写到Channel的最大下标，position表示正在写出的下标初始化为0；

<img src="http://tutorials.jenkov.com/images/java-nio/buffers-modes.png"  style="width:60%;display: block;margin-left: auto;margin-right: auto" />



### Ref

[图片居中](https://www.w3.org/Style/Examples/007/center.en.html)
