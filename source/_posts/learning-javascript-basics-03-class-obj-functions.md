title: js学习04 - Javascript的基本语法03 - 类、对象 与 函数 初探
date: 2016-4-28  
tages:
- js
- 学习
- 语法
- 基础
- 变量
- 函数
- 数据类型

----
# Javascript的基本语法03 -  类、对象 与 函数 初探  

## 前言

上一頁博客討論了`JS`語言中的 `原始类型`，本节介绍高端一点点的`引用类型`。  
其实，本节更适合没有接触过`C++/C`的读者，因为`JS`中，使用`引用`这个术语，反而让有经验的人感觉很迷惑，废话不多说，上代码！

## 对象 Fr4nk

```
  <script type="text/javascript">
      var oFr4nk;
      oFr4nk.sName = "Frank YANG";
      oFr4nk.iAge = 18;           // 18 flower boy, oh shit....
      oFr4nk.sId = "1113332220";
      oFr4nk.sAddr = "PuDong Shanghai China";

      oFr4nk.fnShowHimself = function (){
        console.log("His name is "+ oFr4nk.sName + ".\n" + "And His Id is "+oFr4nk.sId+"\n.");
      }
  </script>
```
<font color="red">**上面这段代码，很不幸，报错了！**</font>

BUt WHy?

`Chrome or Firefox`的控制台告诉我们，`TypeError: oFr4nk is undefined`。
因为，代码中，我们是这样`var　oFrank;`，还记得上一篇博客，如果这样声明变量，则它的类型是未定义的。修改起来也很简单，直接改为`var oFr4nk = new Object;`

![firefox控制台调试js| center ](http://7xsyqy.com2.z0.glb.clouddn.com/console.JPG)

> **TIPS**
> Firefox 和 chrome 均有调试控制台，点击键盘顶端`F12`开启

----

## 函数 `function`

函数其实很简单，可以把它想象成 一个 冰箱，它包括2个要素 ：
>- 【上面冷冻，下面冷藏】: 功能，也就是可以重复使用的代码块；
>-  【厢门】：参数，可以打开 接收输入，也会有返回值！

```
    // 函数定义
    // 该函数还包含 参数，参数无需指定类型
    // 本函数包含返回值，返回一个字符串
    function fridge(iPower, sMilk, sWater, sSugar) {
      return "By using " + iPower + " and elements as " +
        sMilk + " ," + sWater + "," + sSugar + ". Get ice cream!!\n";
    }

    var icecream = "";
    var iPower = "220V Power";
    var sMilk = " Australia cow sMilk";
    var sWater = "water from Tibet";
    var sSugar = "sugar from Guangdong";
    icecream = fridge(iPower, sMilk, sWater, sSugar);

    console.log(icecream + '\n\n\n');

```

<font color="red">**Some key points:**</font>
>- 在函数内部，使用`var`声明的为 局部变量；
>- 函数外部声明的变量，为全局变量，网页的任何位置都能访问；
>- 您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明，如 `carname = 'Volvo'`;
>- 只能在变量声明之后开始访问【生存周期】，局部变量在函数执行完毕后就删除了，而全局变量是在页面关闭之后。

----


## 介绍：什么是『引用类型』

>- 引用类型通常叫做 *类（class）*，也就是说，遇到引用值，所处理的就是对象。
>- 注意：在 `ECMA-262` 中根本没有出现“类”这个词。ECMAScript 定义了“对象定义”，逻辑上等价于其他程序设计语言中的类。

OK， 也就是说 `JS`中，不存在 '类' 这个概念，反而 使用了 “对象定义”，也就是 逻辑上的 `类`。不理解，还是看代码。

对象是由 `new `运算符加上要实例化的 `对象的名字` 创建的。例如，下面的代码创建 `Object 对象`的实例：
```
var o = new Object();
```

----


## 总结：

>- 写的有点无厘头，因为思路被很多知识中断了：比如我在跟着 W3school 教程学习，看到了 `类与对象`，我就想把js中的概念与`CPP/JAVA`的对比学习，深入学习，又会被打断。
>- 如果是按照学习语言的思路，我觉得按照w3school的教程一步一步就可以了，那我这个blog岂不是东施效颦？所以，接下来我决定转换思路，以项目的思维写下面的教程；
>- 虚拟一个很常见的`快递单号CRUD`应用，实现增删改查的功能；

----

## Read more

[1][ Script 对象应用. http://www.w3school.com.cn/js/pro_js_object_working_with.asp](http://www.w3school.com.cn/js/pro_js_object_working_with.asp)
[2][ Script 引用类型. http://www.w3school.com.cn/js/pro_js_referencetypes.asp ](http://www.w3school.com.cn/js/pro_js_referencetypes.asp)
