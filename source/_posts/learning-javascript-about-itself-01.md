title: js学习01 - Javascript的前世和实现
date: 2016-4-25  
tages:
- js
- 学习
- 前世
----

## 前言

我之前的学习计划是，直接学`AngularJS`框架的，学完了`Toturials`之后，发现思想差不多理解，但是具体到`code`之后还是没什么感觉。  

虽然，很久很久之前（5年前），写过`PHP`的东西，荒废太久之后，真是不得不服老啊……哈哈哈，简而言之，基础不好，装逼不牢……于是，我就额外花`2天`预习一下`Javascript`好了……

## 我的前端js水平

>- 达到`知道` 和 `使用过`的程度；
>- `Javascript`简称`js`, 是一种**浏览器客户端**的**脚本语言**，具体是由IE、Chrome、Firefox等浏览器解释执行；
>- 功能和目标是，实现动态改变HTML页面，实现动态效果，包括 `输入验证`、`Ajax异步调用`、`各种酷炫的页面效果`
>- 常见的类库，包括 前端效果类库`jQuery`、后台框架`node.js`和最近刚刚认识的`AngularJS`

## 知不足而学习，而后勇

### JS和它的前世   

早在1992年，一家名为 Nombas的公司发明了一种脚本语言 `ScriptEase`，目的是取代 `宏`命令。Nombas后来将 `ScriptEase`嵌入到 实验版本的浏览器中，用于处理网页，这便是 JS的萌芽……

1995年，Netscape 的 Brendan Eich 开发一个称之为 LiveScript 的脚本语言，当时的目的是在浏览器和服务器（本来要叫它 LiveWire）端使用它。Netscape 与 Sun 及时完成 LiveScript 实现。

> 就在 Netscape Navigator（NN） 2.0 即将正式发布前，Netscape 将其更名为 JavaScript，目的是为了利用 Java 这个因特网时髦词汇。Netscape 的赌注最终得到回报，JavaScript 从此变成了因特网的必备组件。

### 发展和标准化

Netscape 公司发布了 NN 3.0 , 此时，Microsoft 进入浏览器市场，并发布了 IE3.0 并搭载了 Javascript的复制版 JScript，（**为了避免版权纷争还自作聪明的改了名字，早期的微软为了生存也<font color="red">不择手段</font>啊！**）

后来，免不了三足鼎立，Microsoft的`JScript`、NN的`Javascript`和 Nombas的`ScriptEase`，我们呼唤和平呼唤爱、呼唤标准化。


于是，1997年，`JavaScript 1.1` 作为一个草案提交给欧洲计算机制造商协会（ECMA）
由来自 Netscape、Sun、微软、Borland 和其他一些对脚本编程感兴趣的公司的程序员组成的 TC39 锤炼出了 ECMA-262，该标准定义了名为 ECMAScript 的全新脚本语言。

---


## JS的实现

Javascript包括3块内容：
>- ECMAscript 的核心语法和预定义对象；
>- DOM：文档对象模型
>- BOM：浏览器对象模型

![](http://www.w3school.com.cn/i/ct_js_JavaScript_ECMAScript_DOM_BOM.gif)

---
### ECMAScript

ECMAScript 描述了以下内容：
>- 语法
>- 类型
>- 语句
>- 关键字
>- 保留字
>- 运算符
>- 对象

所以，我在学习js语言，我会关注以上的<font color="red">重点</font>，尤其是可以和其他语言对比着学习。  

>ECMAScript 仅仅是一个描述，定义了脚本语言的所有属性、方法和对象。其他语言可以实现 ECMAScript 来作为功能的基准，JavaScript 就是这样：
![](http://www.w3school.com.cn/i/ct_js_ECMAScript_JavaScript_ActionScript_ScriptEase.gif)  
>ECMAScript、JavaScript、ActionScript、ScriptEase
每个浏览器都有它自己的 ECMAScript 接口的实现，然后这个实现又被扩展，

----

### DOM

DOM（文档对象模型）是 HTML 和 XML 的应用程序接口（API）。
```
<html>
  <head>
    <title>Sample Page</title>
  </head>
  <body>
    <p>hello world!</p>
  </body>
</html>
```

![](http://www.w3school.com.cn/i/ct_js_domtree.gif)

DOM 通过创建树来表示文档，从而使开发者对文档的内容和结构具有空前的控制力。用 DOM API 可以轻松地删除、添加和替换节点。

### BOM 

BOM（浏览器对象模型），可以对浏览器窗口进行访问和操作。使用 BOM，开发者可以移动窗口、改变状态栏中的文本以及执行其他与页面内容不直接相关的动作。它只是 JavaScript 的一个部分，没有任何相关的标准。

>- 对浏览器的操作：
>>- 新建、弹出、关闭、和调整浏览器窗口的大小；
>>- 屏幕对象；
>- cookie的支持
>- IE 加入ActiveOBJ支持

浏览器，默认支持如下BOM对象：
>- [Window](http://www.w3school.com.cn/jsref/dom_obj_window.asp)
>>- [Navigator](http://www.w3school.com.cn/jsref/dom_obj_window.asp)
>>- [Screen](http://www.w3school.com.cn/jsref/dom_obj_screen.asp)
>>- [History](http://www.w3school.com.cn/jsref/dom_obj_history.asp)
>>- [Location](http://www.w3school.com.cn/jsref/dom_obj_location.asp)

----

## 小结

我的心得体会有：  

### 一切皆对象  

#### 什么意思？WHAT?  
JS虽然是解释型而不是编译型的脚本语言，但是它处处体现OOP的思想。  

> 什么是OOP（Object-Oriented-Programming）？  
> 万物皆对象，对象就是包含 数据（属性）和行为（方法）的实例（instance）。

#### JS怎么体现OOP？

比如 它会有一些全局的对象，用于描述` browser `和` server` 的通信。比如 窗口对象[`Window`](http://www.w3school.com.cn/jsref/dom_obj_window.asp)。语言本身包含的对象，如`String `对象，用于处理字符串。**JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...**

### DOM操作是精髓

Js存在的意义，就是能够实现动态页面。
而实现动态页面，可以有从2边实现，`Browser`端和 `Server`端；


从浏览器Broswer端实现动态效果，其大致过程如下：

![](http://7xsyqy.com2.z0.glb.clouddn.com/js-archi.png)
*图. B\S系统Broswer端实现动态页面示意图*


![](http://7xsyqy.com2.z0.glb.clouddn.com/bs-archi.png)  
*图. 一般B\S系统服务器端实现动态效果示意图*

JS 的对DOM操作，就是包含对HTML的DOM树的 修改和更新，也就改变原本静态的HTML 内容。但这些操作，都是由浏览器中的JS解释器，通过解释js程序，自动完成。

----


## Read more

[1][Js 简介](http://www.w3school.com.cn/js/js_intro.asp)    
[2][Js 实现](http://www.w3school.com.cn/js/pro_js_implement.asp)    
[3][Js 历史](http://www.w3school.com.cn/js/pro_js_history.asp) 