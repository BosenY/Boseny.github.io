---
title: webpack2学习(一)
date: 2017-01-22 10:00:00
tags:
- webpack 
- node
categories:
- webpack
---


# webpack2学习（一）

## 概念

是一个现代JavaScript应用模块打包器

## 四个核心概念

1. 入口(Entry)  

    webpack 将创建所有应用程序依赖关系图表(dependency graph)。图表的起点被称之为入口起点(entry point)。入口起点告诉 webpack 从哪里开始，并遵循着依赖关系图表知道打包什么。可以将您的应用入口起点认为是根上下文(contextual root)或 app 第一个启动文件。
    <br>
    在webpack当中使用entry属性来定义入口  

    webpack.config.js：
    ```javascript
    module.exports = {
        entry: './path/to/my/entry/file.js'
    };
    ```
<!--more-->
2. 出口(Output)

    webpack 的output属性描述了如何处理打包代码  
    webpack.config.js
    ```javascript
    var path = require('path');

    module.exports = {
        entry: './path/to/my/entry/file.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'my-first-webpack.bundle.js'
        }
    };
    ```
    这里的<em>__dirname</em>是指当前模块文件所在目录的完整绝对路径,path定义了打包后出口对应的就是当前目录下的dist文件夹,而打包出来的名字就是底下filename来控制的


3. 加载器(Loader)  

    webpack 的目标是，让项目中的所有资源都成为 webpack 的关注点，而浏览器不需要考虑这些（这并不意味着资源都必须打包在一起）。 webpack 把 每个文件(.css, .html, .scss, .jpg, etc.) 都作为模块 处理。然而 webpack 只了解 JavaScript。
    * webpack会自己识别出应该被特定的加载器转换的文件
    * 转换能够被添加到依赖图表的文件(并且最终打包) (use属性)

    webpack.config.js
    ```javascript
    var path = require('path');

    const config = {
    entry: './path/to/my/entry/file.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'my-first-webpack.bundle.js'
    },
    module: {
        rules: [
        {test: /\.(js|jsx)$/, use: 'babel-loader'}
        ]
    }
    };

    module.exports = config;

    ```
    module当中定义了<em>rules</em>属性,里面必须包含两个属性：test和use，test告诉了webpack编译器在模块被解析为js或者jsx路径时候，你需要把他们先使用babel-loader转换再去打包

    注意：在 webpack 配置中定义 loader 时，要定义在 module.rules 中，而不是 rules。在定义错时 webpack 会提出严重的警告。
    
4. 插件

    由于加载器仅基于单个文件执行转换，插件最常用(但不限于)在打包模块的编译和分块时执行操作和自定义功能。  

    插件的目的是为了解决loader无法实现的其他事情

    使用时，只需要require他们，并且把他们添加到plugins数组。由于会出现多次使用插件，因此要使用<em>new</em>来创建插件的实例，并且调用插件。

    webpack.config.js
    ```javascript
    const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
    const webpack = require('webpack'); //to access built-in plugins

    const config = {
    entry: './path/to/my/entry/file.js',
    output: {
        filename: 'my-first-webpack.bundle.js',
        path: './dist'
    },
    module: {
        rules: [
        {test: /\.(js|jsx)$/, use: 'babel-loader'}
        ]
    },
    plugins: [
        new webpack.optimize.UglifyJsPlugin(),
        new HtmlWebpackPlugin({template: './src/index.html'})
    ]
    };

    module.exports = config;
    ```