title: Java面向对象基础之OOP基础
date: 2017-8-2
tags:
- java
- oop
- 继承
----

## 介绍

Java是一门面向对象编程的语言。OOP具有如下几个特性：
- 封装：将对象的属性和行为，封装在类声明中。通过方法来改变对象的状态；
- 继承：父类可以派生出子类，子类可以继承父类的属性和方法。从而达到复用代码的效果；
- 多态：Java中有接口的概念，当接口被赋值为不同实现类的实例的引用时，调用同样的方法会有不同的效果。

## 封装

```
class Base {

	private String baseValue;

	public Base() {}

	public void setValue(String val) {
		this.baseValue = val;
	}

	public String getValue() {
		return this.baseValue;
	}

	public static void main(String[] args) {
		Base base = new Base();
		base.setValue("一个字符串");
	}
}

```

上面定义了一个简单的Java类，其中包含一个私有的数据属性`baseValue`，2个操作该属性的方法getter和setter。


## 继承

继承包括如下概念：
- 子类使用extends 关键字继承父类；
- 

