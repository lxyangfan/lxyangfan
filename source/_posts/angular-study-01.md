title: AngularJS 学习之路 01
date: 2016-4-12
tages:
- angular
- 简介
- introduction
-----

## AngularJS 简介

AngularJS 是一个搭建动态WEB APP的程序框架。
HTML语言本身是静态的，导致如今搭建动态WEB APP程序变成了一种任务：究竟我该做哪些事情，才能 *耍*

一般来说，trick的方式有2种：
>* brary : 库lib 是指将常用的功能或者函数functions封装，在你想使用的时候，调用它们。如 `jQuery`
>* frameworks : 框架 是指WEB程序的一种特定的实现，举例子就是 毛坯房，没有装修，你可以具体实现细节部分的装修，毛坯房 = frameworks ；一类框架只适合特定一类应用，你想要 海景别墅，你就不可能去沙漠中选毛坯房。

Angular 采用了其他的方案，它通过指导浏览器理解一些特定的*原语*来构建HTML。例如：
>* 数据动态绑定，如`{\{}\}`
>* DOM控制结构来重复/隐藏DOM片段
>* 附加新的的行为到DOM元素上，如 DOM 事件处理
>* 将HTML组合成可重用的部分



--------

##  一个完全客户端解决方案

在构建Web Application的难题中，Angular 能解决的方面不是一小块。他可以处理所有你曾经手写过的有关DOM和AJAX的和稀泥代码（glue code），并将它们以一种完整定义的方式组合在一起。这使得Angular在构建 增删改查（GRUD）应用方面有一些规矩/固有套路(opinionated)。尽管看起来有些*固执*，但是它仍然易改。一些开箱即用的特点：
>* 一些构建CRUD应用的功能组合，包括 **数据绑定，基本的模板原语，表格验证，路由，深链接，可重用组件，依赖注入**；
>* 可测试性：单元测试/端到端测试/Mocks/test harnesses；
>* 使用目录视图seed应用，测试脚本作为起始点 ；

--------

## Angular 的爽点（Sweet spot）

Angular 通过提出一种更高层次的抽象来简化开发。简化和抽象的代价就是牺牲程序灵活性。
Angular 就是为CRUD应用而生，换句话说，可能其他的应用就不适合使用Angular，如 GUI和游戏。他们可能需要更底层的库，如`jQuery`

------

###  Angular之禅

Angular 框架认为，描述性原语比命令式（过程式）代码在*构建UI和将软件模块组织起来*等方面有优势，后者在表达业务逻辑上更占优势。

>* 将DOM处理从app逻辑层解耦，碉堡了，提高软件代码可测试性！
>* 代码测试和代码编写一样重要，测试的复杂度受代码构建方式影响严重！
>* 将客户端代码从服务器端解耦出来，这是一个 吊爆了 的想法，可以并行开发，2端都可以重用！
>* 带小弟，完整的过一遍框架的使用，这是非常有帮助的！
>* 日常工作无脑化，复杂工作简单化（make common tasks trivial and difficult tasks possible）；

Angular 有如下吊爆了的特性：

>* 注册回调函数；
>* 通过原语操作DOM，更爽；
>* 操作数据流动，更爽，WEB应用的数据交换，无非是从页面拿数据，在页面展示返回的数据，Angular让这部分代码更简洁；
>* 兵马未动，粮草先行：启动程序开始前，N多代码就已经加载；使用Angular,我们启动app更爽，很多依赖会自动加载，注入dependency-injection；

## Reference

[1].[AngularJS 1.X 参考文献](https://docs.angularjs.org/guide/introduction)
