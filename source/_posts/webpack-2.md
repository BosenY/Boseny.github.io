---
title: webpack2学习(二)
date: 2017-01-22 11:06:00
tags:
- webpack 
- node
categories:
- webpack
---

# entry入口起点

## 单入口写法

用法： <strong>entry： string|Array(string)</strong>

webpack.config.js  
```javascript
const config = {
  entry: './path/to/my/entry/file.js'
};

module.exports = config;
```

entry 属性的单入口语法：

webpack.config.js  
```javascript
const config = {
  entry:{
      main:'./path/to/my/entry/file.js'
  } 
};

module.exports = config;
```
<!--more-->
## 对象语法

用法：entry: {[entryChunkName: string]: string|Array(string)}

webpack.config.js

```javascript
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```

这是应用程序中定义入口的最可扩展的方式

webpack的可扩展配置是可重用的，并且可以与其他配置组合使用，这是一种流行的技术，用于将关注点从环境、构建目标、运行时中分离，
然后使用专门的工具把它们合并在一起

## 常见场景

### 入口分离 应用(app) 和 公共库(vendor)

webpack.config.js

```javascript
const config = {
  entry: {
    app: './src/app.js',
    vendors: './src/vendors.js'
  }
};
```
这告诉了我们webpack从app.js和vendors.js开始创建依赖图表。这些图表是完全分离的、互相独立的。在只有一个入口起点(不包括公共库)的单页面应用(spa)当中比较常见

此设置允许你使用CommonsChunkPlugin并从 app 包 提取 公共引用(vendor reference) 到 vendor 包，并把公共引用的部分替换为 <strong>__webpack_require__()</strong>调用。如果应用包中了没有公共代码，那么你可以在 webpack 中实现被称为 长效缓存的通用模式。  

### 多页应用

webpack.config.js

```javascript
const config = {
  entry: {
    pageOne: './src/pageOne/index.js',
    pageTwo: './src/pageTwo/index.js',
    pageThree: './src/pageThree/index.js'
  }
};
```

这里webpack 需要3个独立分离的依赖图表

在多页面应用中，服务器将为您获取一个新的html文档，页面重新加载新文档，并且资源被重新下载。然而，这给了我们独特的机会去做很多事：
* 使用 CommonsChunkPlugin 为每个页面间的应用共享代码创建 bundle。由于入口起点增多，多页应用能够在入口起点重用大量代码/模块，这样可以极大的从这些新技术受益。
* 根据经验：每个 HTML 文档只使用一个入口起点。