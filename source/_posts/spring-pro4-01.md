title: 【Spring Pro4】学习笔记 01
date: 2016-7-12
tages:
- Spring
- 笔记
- introduction
-----


## 【Spring Pro4】学习笔记

### Chapter 1 Introduction

#### 什么是Spring？

Spring 是一个轻量级的Java开发框架，这句话包括2层含义：
- *Java开发框架*，可以开发任何Java程序，包括 stand-alone, web, or Java Enterprise Edition (JEE) applications
- *轻量级* ， 是指使用上的轻量，原有的程序可以很轻松的加入Spring的支持。

#### 控制反转（IoC） or 依赖注入（DI）？

IoC 是一种技术，它将依赖关系的创建和管理外置化（externalized）。

举例来说，`class Foo` 如果需要使用`class Bar`的实例来完成某项工作，一般需要在`class Foo`中创建`class Bar`的实例。IoC技术，就是可以在 `runtime`（运行时）给 `Foo`提供`Bar`的实例。这种行为，运行时注入依赖关系的行为，又称为`Dependencies Injection, DI`。

所以，IoC 和 DI 是指一个概念，运行时注入依赖。

#### Spring 的DI又是怎么实现的呢？
Spring利用了2个Java 核心概念：JavaBean 和 Interface。

JavaBean我理解就是符合一定规范的POJO，必须包含 各种 getter、setter函数，必须是空的构造函数。
接口interface，那就是更好理解了，仅仅包含函数的声明，没有函数的定义，可以实现多态，一个类implements interface就必须给出具体的实现。

在这里spring 其实又可以看成是一种 container，里面包含了各种 JavaBean，通过XML\Annotation的方式，实现对各种JavaBean的DI。

再具体的实现方式，需要进一步阅读...

### Chapter 3， Spring中的DI和IoC

先放出一张我的理解，Spring本身就是 JavaBean的容器，使用XML和其他方式配置各个JavaBean之间的依赖关系。


![Alt text](http://7xsyqy.com2.z0.glb.clouddn.com/spring-idea.bmp)

第3章则详细介绍了如下内容：
- IoC详细概念：DI 和  Dependency Lookup
- Spring中的IOC，它们的具体实现（setter、getter）
- Spring中的DI，包括Spring实现的IOC容器container
- 配置Spring的ApplicationContext

#### IOC的分类

![](http://7xsyqy.com2.z0.glb.clouddn.com/spring-DI-types.bmp)
#### Dependency Injection

分为2类，构造函数注入和setter函数注入：

```
// Constructor Injection

class Foo {

    private Dependency dependency;

    Foor (Dependency dependency){
	    this.dependency = dependency;
	}

	@Override
	public String toString(){
		return dependency.toString();
	}
}


// Setter Injection

class Bar{

	private Dependency dependency;

	Bar(){
	}

	public void setDependency(Dependency dependency){
		this.dependency = dependency;
	}

	@Override
	public String toString(){
		return dependency.toString();
	}
}
```

- Setter Injection 会将注入的依赖暴露出来，setDependency 隐含着这个类依赖 `Dependency`(JavaBean的风格)。
- Constructor Injection 表示使用这个类，它所有的依赖关系都会首先被注入，首先被保证。尽管包括Spring在类的一些容器，已经有机制保证类在使用之前，所有的依赖都会满足。

这一小节讨论的是标准的IOC的概念，下面，说说Spring中的DI的实现，包括Constructor、setter、Method Injection 以及它们的配置方式。

#### DI in Spring

Spring的DI Container 核心就是 BeanFactory 接口，它负责管理所有的组件和对应依赖的生命周期。

![Alt text](http://7xsyqy.com2.z0.glb.clouddn.com/spring-DI-meachnism.png)

BeanFactory 和 Bean是什么意思呢？

Spring中的Bean是指由 Spring Container管理的JavaBean类。
BeanFactory 是一个接口，可以用于管理和创建这些Bean。因为本身是接口，没有实现，所以在使用之前必须用具体的类来实现。

除了BeanFactory之外，ApplicationContext 接口是对BeanFactory的一个扩展，他还提供了其他的服务，包括 事务、国际化等。

Spring中，推荐使用ApplicationContext，通过2种方式：
- 手动编码实例化ApplicationContext，加载配置文件
- Web容器通过 ContextLoadListener加载

#### Spring 配置选项

- properties or XML 文件
- annotation 注解的方式

> One common approach is to **define the application infrastructure** (for example, data source, transaction manager, JMS connection factory, or JMX) in an **XML file**, while defining the **DI configuration** (injectable beans and beans’ dependencies) in **annotations**.

TO BE CONTINUED...





