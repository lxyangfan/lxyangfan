title: Spring In Action 3rd 读书笔记
date: 2016-5-26
tages:
- Spring
- MVC
- 读书笔记
-----
## Spring In Action 3rd 读书笔记

### 引子 —— 简单粗暴！什么是 Spring ？
关键词、短语：
- Spring是用来**简化** 企业级Java开发的！【既然是简化开发，那就爽啊，简单啊！】
- Spring的核心思想：**依赖注入 （Dependency Injection，DI）和 面向切面编程（Aspects-Oriented Programming, AOP）**【不知道不要紧，待会知道就行】
- 使用**POJO**简化开发；POJO = Plain-old Java Objects，就是我们上课随便写写的简单java类
- 使用 DI和AOP 创建 **低耦合**（loosely couple）的Java项目；

----

### 正题 —— 笔记组织

我一贯按照`3W1H`的简单粗暴的思考方式来认识世界，So is Spring!
接下来的笔记按照如下组织：
>- 分别详细介绍 Spring 的核心概念 `DI`和`AOP`
>- 怎样使用 `DI` 和 `AOP`

### Spring 核心概念之 依赖注入`DI`

#### 依赖注入`DI` 之名词解释

首先是`依赖`。此`依赖`，非你侬我侬的互相"依赖"，而是 OOP中的类和类之间的**依赖关系**。 So 在这里发一个传送门：[几种类间关系：继承、实现、依赖……](http://blog.csdn.net/sfdev/article/details/3906243)

> **依赖关系**
> 可以简单的理解，就是一个**类A使用到了另一个类B**，而这种使用关系是具有偶然性的、临时性的、非常弱的，但是B类的变化会影响到A；
> 比如某人要过河，需要借用一条船，此时人与船之间的关系就是依赖；
> 表现在代码层面，为**类B作为参数被类A在某个method方法**中使用；

`依赖`解释清楚了，感觉没什么`高大上`的，就是`使用`和`被使用`的意思呗。
`依赖注入`感觉就很`new bee`了，注入哎！我第一反应是`注水猪肉`…… Orz

下面，我将描述`注水猪肉`，哦不，`依赖注入`……

#### `依赖注入`和`冰与火之歌`

⊙﹏⊙b 怎么扯到 `冰与火之歌` ⊙﹏⊙b
因为原书作者就写了一个`骑士Knight`类来说明问题，这不怪我咯……

```
// demo code
// @author Frank Yang

package cn.frank.Knight;

// import the Knight interface
import com.game.of.thrones.Knight;
import com.game.of.thrones.ResequeBeautyQuest;

public class HandsomeKnight implements Knight{
  private ResequeBeautyQuest resequeQuest;
  public HandsomeKnight(){
    resequeQuest = new resequeQuest();
  }
  // implements the Gogogo interface from Knight
  public void Gogogo(){
    resequeQuest.beautyNeedHelp();
  }
}

```
每一个实现了`Knight`接口的人（或者Java类），都变成了骑士。  他们必须实现接口函数`Gogogo`来响应请求`Quest`。

以上的代码中，`HandsomeKnight`帅气骑士需要救助一个落难的美女，在这里，`resequeQuest`是救助美女的请求。所以，在`HandsomeKnight`的`Gogogo`函数中，实现了救助美女的全部过程，`resequeQuest.beautyNeedHelp();`。

这里，`resequeQuest`和`HandsomeKnight`就是 `聚合关系`，比`依赖关系`
还要强。也就是说，这2个类之间，耦合度太高。完全没有耦合是不现实的（否则`Knight`骑士无法救美人），弱耦合化，怎么破？

```
// BraveKnight
// @author Frank Yang

package cn.frank.Knight;

// import the Knight interface
import com.game.of.thrones.Knight;
import com.game.of.thrones.Quest;

public class BraveKnight implements Knight {
  public Quest quest;

  // constructor injection
  public BraveKnight (Quest quest) {
    this.quest = quest;
  }

  public void Gogogo( ) {
    quest.SomeHelp();
  }

  public void main( String[] args ){
    Quest resqueBeautyQuest = new ResequeBeautyQuest();
    Knight braveKnight = new BraveKnight( quest );

    // Resque The beauty!
    braveKnight.Gogogo();
  }

}
```

上面这段代码，`BraveKnight`的构造函数，包含了一个 实现了`Quest`接口的对象，也就是说，`BraveKnight`和`Quest`之间是`依赖关系`。他们之间的关系，要比第一段代码，弱化的多，耦合度也低。

**为什么？**

因为，`Quest`是接口，很多类可以实现这个接口，比如我们实现其他的类，如`SlayDragonQuest`这个屠龙的请求，照样可以传给`BraveKnight`。这样，`BraveKnight`可以去做很多事情，而不限制于救小美人或者屠龙了。

`依赖注入DI`的精髓就在这里：
> With DI, on the other hand, objects are given their dependencies at creation time by some third party that coordinates each object in the system.
>
> 在DI的帮助下，对象在创建的时候，由一些负责协调系统内对象的第三方给出这个对象的依赖关系。
>
> Objects aren’t expected to create or obtain their dependencies—dependencies are injected into the objects that need them.
>
> 换言之，对象不会**创建** 或者 得到他们**依赖对象**，这些**依赖**会在需要的时候**注入**到对象中。

这就是，DI 带来的好处—— 低耦合 ——依赖对象( Knight )无须知道 被依赖对象( Quest )的实现方式。

下一节，会简单介绍，如何实现`DI`……

----

### ReadMore

[Spring in Action 3rd](#)

