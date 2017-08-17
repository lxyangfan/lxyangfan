title: webpack 打包神器的使用
date: 2017-8-17
tags:
- webpack
- 前端
-----

## webpack 前端打包“神器”

最近使用了AMD的方式组织前端代码，也就是 `RequireJs` 管理前端 js 代码之间的依赖。在发布的时候，的确也可以将源代码 js 按照项目目录发布，这样不足的地方：
- 浏览器会发起多次 web 请求不同的js文件；
- 直接给出了源码，可能会被人直接乱改，破坏了代码的完整性；

因此需要类似于后端发布包，需要给出一个前端的发布包，包括版本信息。

简单的搜索了一下，前端的打包工具有很多，如`gulp`,`grunt`...，相比之下`webpack` 是目前主流的打包神器，`Angular\React` 都选择它作为默认的打包工具，学习使用它完全不需要理由。下面正式介绍 webpack。

## webpack 安装和使用

webpack 是基于 nodejs 平台的，先把 nodejs 和 npm 装了才能使用 webpack 。

```
npm install --save-dev webpack

```

webpack 有几个基本概念：
- `entry`: 简单理解就是输入，基本的 js 单元
- `output`: 输入的文件，最终的 bundle 文件
- `plugin`: 可以对 bundle 操作的插件，比如 uglifyPlugin
- `loader`: webpack 把所有的文件都看成模块，如 png，css，js 等，但是 webpack 直接认识的只有 js 文件，其他格式的文件需要 loader 工具处理

### webpack 配置文件

webpack 工具需要配置，指定打包过程、输入、输出。下面给出一个配置文件 `webpack.conf.js`：

```
const path = require('path');

module.exports = {
    //context: path.resolve(__dirname, 'src'),
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, 'dist/assets'),
        filename: 'bundle.js',
    },
    resolve: {
        alias: {
            jquery: path.resolve(__dirname, 'node_modules/jquery/dist/jquery.min')
        },
        modules: ['node_modules']
    }
}

```
如下是我的工程目录树（`tree . -I node_modules`, 不列出符合正则表达式的目录）。

```
.
├── README.md
├── dist
│   ├── assets
│   │   └── bundle.js
│   └── index.html
├── doc
│   ├── requirejs.md
│   └── routes.md
├── index.html
├── package-lock.json
├── package.json
├── src
│   ├── asset
│   │   └── api.js
│   ├── libs
│   │   └── json3.min.js
│   ├── main.js
│   ├── service
│   │   └── excel.js
│   └── utils
│       └── network.js
└── webpack.conf.js
```
下面我会一一介绍`webpack.conf.js`文件配置选项的含义。

`entry` 配置的就是输入，可以理解为程序的入口。如果是单页面应用就只有一个，多页面应用可能会有多个。我这个项目很简单，就包含了一个入口文件。
`output` 配置了最终打包输出的文件名和位置。
`resolve` 配置了怎么去解析诸如 `import $ from 'jquery';`的依赖，类似于`RequireJs`的设置。

## 其他

webpack 自带了对 es2015 的导入和导出的 API ，因此我在代码中直接写：
```
import $ from 'jquery';
function XXX() {}
export {
    XXX
};
```
这种是直接被 webpack 处理的，es2015 其他高级特性，需要再 webpack 中引入 Babel 插件才能使用。（果断抛弃requireJs的AMD写法了 keke）

`webpack --display-error-details`: 可以打印出报错详情，推荐初学者加上。

## 参考

[webpack2 官方概念介绍](https://webpack.js.org/concepts/)
[webpack2 官方指导](https://webpack.js.org/guides/)
[webpack2 官方配置说明](https://webpack.js.org/configuration/)
[基于webpack打包的实例项目](https://github.com/lxyangfan/vue-downloader/tree/jq-webpack)
