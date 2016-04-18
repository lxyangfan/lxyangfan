title: Angular 学习02 之 路由+拦截器
date: 2016-4-14
tags:
- angularjs
- js
- route
---

## 闲话少叙，上代码

代码结构，如下：

![directory](http://7xsyqy.com2.z0.glb.clouddn.com/image/jpg/160414-01.PNG)


代码主体包括 `controller.js`和`app.js`，其中`app.js`是程序入口文件。他们都加载到`index.html`中。

```html
<!doctype html>
<html lang="en" ng-app="phonecatApp">
<head>
  <meta charset="utf-8">
  <title>Google Phone Gallery</title>
  <link rel="stylesheet" href="bower_components/bootstrap/dist/css/bootstrap.css">
  <link rel="stylesheet" href="css/app.css">
  <script src="bower_components/angular/angular.js"></script>
  <script src="bower_components/angular-route/angular-route.js"></script>
  <script src="js/app.js"></script>
  <script src="js/controllers.js"></script>
</head>
<body>

  <div ng-view></div>

</body>
</html>
```
上面是 `index.html`可以看出，这个首页文件沦落为 模板文件`template file`。


```javascript
/**
 * controller.js 页面控制器js
**/

'use strict'; //什么语法？

/* Controllers */

// controller变量名 和 Module的第一个参数必须一致
var ControllersName = angular.module('ControllersName', []);

// 向ControllersName实例化各个小的controller；
// 负责接收数据的 PhoneListCtrl_1
// 负责 网址路由的 PhoneDetailCtrl_2

ControllersName.controller('PhoneListCtrl_1', ['$scope', '$http',
  function($scope, $http) {
    $http.get('phones/phones.json').success(function(data) {
      $scope.phones = data;
    });

    $scope.orderProp = 'age';
  }]);

// 其中phoneId是在 其他html模板文件中出现的
// 具体在 phone-list.html文件中

ControllersName.controller('PhoneDetailCtrl_2', ['$scope', '$routeParams',
  function($scope, $routeParams) {
    $scope.phoneId = $routeParams.phoneId;
  }]);


```

**小结一下：**
>- controller变量名 和 Module的第一个参数必须一致；
>- `$`开头的变量`$scope`,`$http`和`$routeParams`都是有**身份**的，AngularJS预定义的，所以我们自己不能随便定义`$`开头的变量；

下面介绍入口文件`app.js`，说它是入口，类似于`C++/C`中的`main`函数一样，加载点。


```javascript
/*
   app.js 程序入口js
*/
'use strict';

/* App Module */

// 定义了一个变量 app， 其中加载了 ngRoute 和我们自定义的 Controllers 模块
var phonecatApp = angular.module('phonecatApp', [
  'ngRoute',
  'ControllersName'
]);

// app需要配置一下 ngRoute，其中 路由的功能是由 routeProvider 提供

phonecatApp.config(['$routeProvider',
  function($routeProvider) {
    $routeProvider.
      when('/phones', {
        templateUrl: 'partials/phone-list.html', // 在这里连接了模板html文件
        controller: 'PhoneListCtrl_1'			 // 因此 phone_ctrl1 就能 bi-bind双向绑定
      }).
      when('/phones/:phoneId', {
        templateUrl: 'partials/phone-detail.html',
        controller: 'PhoneDetailCtrl_2'
      }).
      otherwise({
        redirectTo: '/phones'					// 默认跳转到 /phones
      });
  }]);


```
**小结:**

>- `$routeProvider` 来声明 路由，是服务提供者。可以让我们使用浏览器的历史(*回退或者前进导航*)和*书签*。

----

## 关于 依赖注入 和 服务提供者（Providers）

### Something about （Dependency Injection, DI）

>- 依赖注入是AngularJS的核心特性；
>- 当应用引导时，AngularJS会创建一个注入器，我们应用后面所有依赖注入的服务都会需要它；
>- 注入器 为了载入特定服务模块，如`$http`和 `$route`服务，在这些模块中注册所有定义的服务提供者，并且当需要时给一个指定的函数注入依赖（服务）；
>- 这些依赖通过它们的提供者“懒惰式”（需要时才加载）实例化；


### Let's talk about `Provider`

提供者是提供（创建）服务实例并且对外提供API接口的对象，它可以被用来控制一个服务的创建和运行时行为。对于`$route`服务来说，`$routeProvider`对外提供了API接口，通过API接口允许你为你的应用定义路由规则。


## 依赖注入DI - 未完待续


>- What is DI?
>- Why we need DI?
>- When to use DI?
>- How to use DI in Angular JS?
