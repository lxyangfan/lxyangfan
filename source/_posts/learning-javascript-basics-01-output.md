title: js学习02 - Javascript的基本语法01 - 输出  
date: 2016-4-25  
tages:
- js
- 学习
- 语法
----

## 前言

>- 学习本教程前提是，有其他编程语言的基础，或者说编程思想的。我不会赘述类似于`if..else`和`when\while`等基础思想。
>- 我会尽量手把手教学；

---

## 环境准备


### 软件系统

>- 本教程可能包含其他工具的使用：必选[`git`](https://git-scm.com/downloads/guis)和任何一款文本编辑器(我使用[`sublime text 3`](https://www.sublimetext.com/3))
>- `git`环境搭建和安装,请自行`Google`,使用搜索引擎,也是历练的一部分;
>- 如果没有**科学上网**的条件,例如`Google`被墙,我可以提供我自己掏钱买的`VPN`，微信联系我或者评论；

### 心里系统

>- 默念n遍,我可以的\我可以的.....无限循环

---


## 正式开始

### 导入项目

>- 我在`C:\`新建一个文件夹目录`C:\Dev\my_js_toturial`
>- 打开`Git bash`中，使用`cd`切换到该目录下；  
`cd C:\Dev\my_js_toturial`  
>- 导入我托管到github上的开源项目：  
`git clone https://github.com/lxyangfan/js-learn.git`
![](http://7xsyqy.com2.z0.glb.clouddn.com/js-learn-2-01.png)
>- 切换到子目录`js-learn`下，加载代码文件
`git checkout step-01`
![](http://7xsyqy.com2.z0.glb.clouddn.com/js-learn-2-02.png)
>- 可以看到，静态html文件就下载完毕，项目文件导入完成
![](http://7xsyqy.com2.z0.glb.clouddn.com/js-learn-2-03.png)

### 运行

切换到下图，直接双击`index.html`,在默认浏览器查看效果，我的默认浏览器是`Firefox`,`Chrome`也推荐，建议舍弃`IE`.
![](http://7xsyqy.com2.z0.glb.clouddn.com/js-learn-2-03.png)

运行结果：  

![](http://7xsyqy.com2.z0.glb.clouddn.com/js-learn-2-04.png)

----

### 开始实践

`index.html`的全部代码，如下，草鸡简单！

```
<!DOCTYPE html>
  <head>

  </head>
  <body>

    <p id="p1">Hello </p>
    <input type="button" id="btn1" value="click me!"></input>

  </body>
</html>
```

#### 目标：hello world!

##### 法一

```
<!DOCTYPE html>

  <head>


  <script type="text/javascript">

  /**
    func name:    changeString
    params:       null,
    return:       null,
    intro:        change the 'p1' string
  */
    function changeString(){
      window.document.getElementById('p1').innerHTML =  "Hello world";
    }


  </script>

  </head>

  <body>

    <p id="p1">Hello </p>
    <input type="button" id="btn1" value="click me!" onclick="changeString()" ></input>

  </body>

</html>

```
#### 作业：

实现，点击按钮,切换 页面显示的文字。

代码在`ans.html`中，请自己思考，再看答案！

---

## Read more

[1][W3School 官方教程](http://www.w3school.com.cn/js/js_whereto.asp)









