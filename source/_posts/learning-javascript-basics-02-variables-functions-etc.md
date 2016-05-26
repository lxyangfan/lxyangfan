title: js学习03 - Javascript的基本语法02 - 变量/数据类型
date: 2016-4-26
tages:
- js
- 学习
- 语法
- 基础
- 变量
- 函数
- 数据类型

----
#  Javascript的基本语法02 - 变量/数据类型

## 前言

因为这些是基础中的基础，而我有一些基础，所以基础就简单讲讲。哈哈

我会更侧重与，其他高级语言`C/C++/Java`等不同的地方。 SO game start！

## Js 变量

### 事前问题

Q1: `变量`怎么理解？
`变量`可以比喻成 - 水桶，只不过，`变量`装的是 数据，而不是水。
所以，变量的内容是存放在 内存中的数据。

Q2: js 中的变量是如何存放到内存中的？『很有**深度**的问题』

<font color="gray">
js是一种解释型的语言，所以它的内存分配机制和 浏览器的解释器有很大的关系，这涉及到 js解释器的实现，这属于『高阶』话题。应该是采用数据结构的 『栈内存』，没听说过 js还可以动态申请和分配『堆』内存。这些有待考证和学习！</font>

-- TBD --

----


### 变量的声明和特殊点

----


#### 变量的声明

在`JavaScript`中创建变量通常称为“声明”变量。 我们使用`var`关键词来声明变量：

`var carname;`

变量声明之后，该变量是空的（它没有值）。如需向变量赋值，请使用等号：

`carname = "Volvo";`

不过，您也可以在声明变量时对其赋值：

`var carname="Volvo";`

----


在计算机程序中，经常会声明无值的变量。未使用值来声明的变量，其值实际上是 `undefined`。

`var carname;`

`carname = undefined`

---

重新声明`JavaScript`变量，该变量的值不会丢失：
在以下两条语句执行后，变量`carname`的值依然是`Volvo`：

```
var carname="Volvo";
var carname;
```
---


#### 变量的命名规则


`Pascal`标记法

首字母是大写的，接下来的字母都以大写字符开头。例如：

`var MyTestValue = 0, MySecondValue = "hi";`


有3种命名规则，我以后会遵循`匈牙利类型标记法`：

在以 Pascal 标记法命名的变量前附加一个小写字母（或小写字母序列），说明该变量的类型。例如，i 表示整数，s 表示字符串，如下所示
```
var iMyTestValue = 0, sMySecondValue = "hi";
```

|	类型	|	前缀	|	示例	|
|-----------|-----------|-----------|
|	数组	|	a		|	aValues	|
|	布尔型	|	b		|	bFound	|
|	浮点型	|	f		|	fValue	|
|	函数	|	fn		|	fnChange|
|	整数数	|	i		|	iAge	|
|	对象	|	o		|	oPerson	|
|	字符串	|	s		|	sName	|
|	变型	|	v		|	vValue	|



---

#### 其他

变量的声明不是必须的，`Javascript`是一种弱类型的语言。

```
var sTest = "hello ";
sTest2 = sTest + "world";
alert(sTest2);
```

`sTest2`虽然使用之前没有声明和赋初始值，但是它被运算后的值是字符串`Hello world`.

更多内容详见：
[1][ ECMAScript 变量 . http://www.w3school.com.cn/js/pro_js_variables.asp](http://www.w3school.com.cn/js/pro_js_variables.asp)
[2][ ECMAScript 语法 . http://www.w3school.com.cn/js/pro_js_syntax.asp](http://www.w3school.com.cn/js/pro_js_syntax.asp)

----

## Js 数据类型

### Js具有动态类型

这意味着**相同的变量**可用作不同的类型：
```
var x                // x 为 undefined
var x = 6;           // x 为数字
var x = "Bill";      // x 为字符串
```


### Js 的数组

多种定义方式：
```
var aCars = new Array();
aCars[0] = "Audi";
aCars[1] = "BMW";
aCars[2] = "Volvo";
```
或者

```
var aCars = new Array("Audi", "BMW", "Volvo");
```

或者

```
var aCars = [ "Audi", "BMW", "Volvo" ];
```

显然，第三种方式，更简单，好写，方便；


### Js 的对象

在JS中，所有的变量都是对象，和其他语言不同，JS不需要实例化 和 定义类，就可以生成对象：

```

// 定义了，fr4nk，这个对象，以及它的属性和方法
var oFr4nk = {

	sName : "Frank YANG" ,
	sBirthday : "1993-01",
	iGender : 1,	// 男性
	bMarried : false,	// 未婚
	bGf : true 		// 有女朋友


};
    // 显示他的个人信息
    function fnGetHisInfo(oPerson){
        return 'His name is '+ oPerson.sName +  '. And His birthday is '+ oPerson.sBirthday;
    }


// sInfo 存放了 对象的个人信息
var sInfo = fnGetHisInfo(oFr4nk);
// 对话框弹出消息
alert( sInfo );



```

### 声明变量类型

Js变量当然也可以声明对象的类型：
```
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;
```

----

## 一丢丢的<font color="red">高阶知识</font>

### 变量的原始类型 primitive type

5种原始类型（primitive type），即 `Undefined、Null、Boolean、Number 和 String`。

`typeof` 运算符有一个参数，即要检查的*变量或值*。例如：
```
var sTemp = "test string";
alert (typeof sTemp);    //输出 "string"
alert (typeof 86);    //参数是 值，输出 "number"
```
对变量或值调用 `typeof` 运算符将返回下列值之一：
>- undefined - 如果变量是 Undefined 类型的
>- boolean - 如果变量是 Boolean 类型的
>- number - 如果变量是 Number 类型的
>- string - 如果变量是 String 类型的
>- object - 如果变量是一种**引用类型或 Null** 类型的

---

### `undefined` 类型

前面说过，如果对对象没有初始化，默认值就是`undefined`.
```
  var vSome;  // 该变量vSome将被赋予值 undefined

  console.log(typeof vSome);

  // 因为 vSome 是未定义的变量，而不是 字符串'undefined', 所以是false
  console.log( vSome == 'undefined');

  // vSome 开始被赋值 undefined, 所以是 true, undefined不是 字符串'undefined'!!
  console.log( vSome == undefined);
```

同理，`JS` 可以不声明就使用变量，默认值也是`undefined`.

```
  console.log( typeof vSome2 );

  // 因为 vSome 是未声明的变量，而不是 字符串'undefined', 所以是false
  console.log( vSome == 'undefined');

  // vSome 开始被赋值 undefined, undefined 不是 字符串'undefined'!!
  console.log( vSome == undefined);
```
`ECMAscript`规范提到，未声明的变量不能使用除了`typeof` 之外的其他运算符，否则会报错。但是，我在`chrome\firefox`中测试上面代码，并没有提示报错！也是醉了。

当函数无明确返回值时，返回的也是值 `undefined`，如下所示：

```
  // 无返回值的 函数 fnTest(), 返回值也是 undefined
  function fnTest(){

  }
  console.log( typeof fnTest() );
```

---

### `Null`值

>- `undefined `是声明了变量但未对其初始化时赋予该变量的值，
>- `null` 则用于表示`尚未存在的对象`。如果函数或方法要返回的是`对象`，那么找不到该`对象`时，返回的通常是` null`。

我的理解是，`null`类似于`C`语言中的空指针一样，这样说可能不规范，但是方便理解，具体的例子可以以后补上。

`undefined`表示对象：
>- 声明了，但是没有赋初始值， `var vValue;` ;
>- 没有声明，直接使用的变量！

`null`就是表示该对象不存在！

---

### `Number`类型

这种类型既可以表示 32 位的`整数`，还可以表示 64 位的`浮点数`。
直接输入的（而不是从另一个变量访问的）任何数字都被看做 `Number` 类型的字面量。
#### 8进制和16进制
```
var iNum = 070;  //070 等于十进制的 56
var iNum = 0x1f;  //0x1f 等于十进制的 31
var iNum = 0xAB;  //0xAB 等于十进制的 171
```
尽管所有整数都可以表示为八进制或十六进制的字面量，但所有数学运算返回的都是十进制结果。

#### 浮点数
```
var fNum = 1.0;
```
对于浮点字面量的有趣之处在于，用它进行计算前，**真正存储的是字符串**。

#### 无穷、`NaN`

前两个是 	`Number.MAX_VALUE` 和 `Number.MIN_VALUE`，它们定义了 `Number `值集合的外边界。

`Number.POSITIVE_INFINITY` 的值为 `Infinity`。
`Number.NEGATIVE_INFINITY` 的值为 `-Infinity`。

`NaN`，表示非数（Not a Number）。`NaN `是个奇怪的特殊值。一般说来，这种情况发生在类型（String、Boolean 等）转换失败时。

`NaN` 的另一个奇特之处在于，它与自身不相等。

```
isFinite( Number.POSITIVE_INFINITY  ) // 测试无穷大
isNaN("blue")						// 测试NaN
```

----

## Read more


[1][ ECMAScript 变量 . http://www.w3school.com.cn/js/pro_js_variables.asp](http://www.w3school.com.cn/js/pro_js_variables.asp)
[2][ ECMAScript 语法 . http://www.w3school.com.cn/js/pro_js_syntax.asp](http://www.w3school.com.cn/js/pro_js_syntax.asp)
