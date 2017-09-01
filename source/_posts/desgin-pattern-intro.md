title: 设计模式介绍、简单工厂模式、工厂方法模式
tags:
- Design Pattern
- 设计模式
- 工厂方法
-------

## 设计模式介绍

设计模式是前人软件开发过程中的最佳实践的总结，学习这些模式可以写出更健壮、更具扩展性的代码。具体介绍设计模式之前，先介绍一下面向对象编程的几个原则：
- 开闭原则：开发新功能不是在修改原有代码基础上，而是扩展，more open for extension
- 更多使用组合而不是继承：
- 李式替换原则：在使用父类的地方都可以使用子类对象替换
- 面向抽象接口编程而不是面向具体实现编程

上面OOP原则还有很多，详见这篇文章：

下面正式介绍设计模式。

## 设计模式分类

设计模式按照行为可以分为3类：
- 创建型：单例模式（singleton）、抽象工厂模式、工厂方法模式（Factory method）、创建者模式、原型模式
- 结构型：适配器模式、组合模式等等
- 行为型：模版方法模式、策略模式等等 

完整的列表如下：

<table border="1" width="800" cellspacing="1" cellpadding="1" align="center">
<tbody>
<tr>
<th scope="col"><span style="font-size:16px">范围/目的</span></th>
<th scope="col"><span style="font-size:16px">创建型模式</span></th>
<th scope="col"><span style="font-size:16px">结构型模式</span></th>
<th scope="col"><span style="font-size:16px">行为型模式</span></th>
</tr>
</tbody>
<tbody>
<tr align="center">
<td><span style="font-size:16px">类模式</span></td>
<td><span style="font-size:16px"><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7644635">工厂方法模式</a><br>
<br>
</span></td>
<td><span style="font-size:16px"><a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7653190">（类）适配器模式</a></span></td>
<td><span style="font-size:16px"><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7674756">解释器模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7661214">模板方法模式</a><br>
<br>
</span></td>
</tr>
<tr align="center">
<td><span style="font-size:16px">对象模式</span></td>
<td><span style="font-size:16px"><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7646587">抽象工厂模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7671209">创建者模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7678010">原型模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7646727">单例模式</a><br>
<br>
</span></td>
<td><span style="font-size:16px"><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7653190">（对象）适配器模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7670996">桥接模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7667796">组合模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7643395">装饰模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7657563">外观模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7674655">享元模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7670529">代理模式</a><br>
<br>
</span></td>
<td><span style="font-size:16px"><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7671594">职责链模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7650761">命令模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7665142">迭代器模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7677759">中介者模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7677867">备忘录模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7643058">观察者模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7669603">状态模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7638460">策略模式</a><br>
<a target="_blank" target="_blank" href="http://blog.csdn.net/yangzl2008/article/details/7681181">访问者模式</a><br>
<br>
</span></td>
</tr>
</tbody>
</table>

## 简单工厂模式和工厂方法模式

![简单工厂模式]()

![工厂方法模式]()



