---
title: webpack2学习(四)
date: 2017-01-22 14:42:52
tags:
- webpack 
- node
categories:
- webpack
---

# 加载器(loaders)

loader 是对应用程序中资源文件进行转换。它们是(运行在node.js中的) 函数，可以将资源文件作为参数的来源，然后返回新的资源文件  
例如，你可以使用loader告诉webpack加载css文件，或者将TypeScript转化为JavaScript

## loader特性

* loader支持链式传递。能够对资源使用流水线(pipeline)。 loader链式按照时间先后顺序进行编译。  
  loader链中的第一个loader返回值给下一个loader，并且在最后一个loader，webpack按照预期的JavaScript返回
* loader可以是同步或者是异步函数。
* loader运行在node.js中，并且能够执行任何可能的操作。
* loader接受查询参数。用于loader间传递配置。
* loader也能够使用  `options`对象进行配置
* 除了使用package.json的main属性，还可以将普通的npm模块导出为loader，做法是在package.json里定义一个loader字段
* 插件可以给loader带来更多的功能
* loader能够产生额外的任意文件

loader通过(loader)预处理函数，为JavaScript生态系统提供了更多有利功能。用户现在可以更加灵活的引入细粒度逻辑，例如压缩、打包、语言翻译和其他
<!--more-->

## 解析loader

loader解析类似于模块，loader模块需要导出一个函数，并且使用兼容node.js的JavaScript编写。在通常情况下，你可以使用npm管理loader，但是你也可以在应用程序中将loader作为文件去使用


## 引用loader

loader通常被命名为xxx-loader ，xxx是上下文的名称  eg： json-loader

load的名称约定和优先搜索顺序，由webpack配置API中的resolveLoader、moduleTemplates定义
***
# 插件(plugins)

webpack本身也是构建于同样的插件系统
插件的目的在于解决loader无法实现的事情

## 解剖

webpack插件是一个具有apply属性的JavaScript对象。apply属性会被webpack解析器(compiler)调用，并且可在整个编译生命周期(compilation lifecycle)访问。

ConsoleLogOnBuildWebpackPlugin.js
```javascript
function ConsoleLogOnBuildWebpackPlugin() {

};

ConsoleLogOnBuildWebpackPlugin.prototype.apply = function(compiler) {
  compiler.plugin('run', function(compiler, callback) {
    console.log("The webpack build process is starting!!!");

    callback();
  });
};
```


