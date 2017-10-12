---
title: webpack2学习(三)
date: 2017-01-22 13:42:52
tags:
- webpack 
- node
categories:
- webpack
---

# 输出output

output选项控制webpack如何向硬盘写入编译文件。注意，即使可以存在多个入口起点，但只指定一个输出配置

## 用法

设置`output`属性，只需要在你的webpack配置简单的设置输出值：

webpack.config.js
```javascript
const config = {
  output: 'bundle.js'
};

module.exports = config;
```
<!--more-->
下面是一些output的属性：
### output.filename  

    指定硬盘每个输出文件的名称。在这里你不能指定绝对路径！ `output.path`选项规定了文件被写入硬盘的位置。 filename 仅用于命名每个文件。

单个入口
```javascript
{
  entry: './src/app.js',
  output: {
    filename: 'bundle.js',
    path: __dirname + '/build'
  }
}

// 写入到硬盘：./build/bundle.js
```

多个入口

如果你的配置创建了多个`chunk`(例如使用多个入口点或使用类似CommonsChunkPlugin的插件)，
你应该使用以下的替换方式来确保每个文件名都不重复。

* [naem] 被chunk 的name 替换
* [hash] 被编译(compilation) 的hash替换
* [chunkhash] 被chunk 的hash 替换
```javascript
{
  entry: {
    app: './src/app.js',
    search: './src/search.js'
  },
  output: {
    filename: '[name].js',
    path: __dirname + '/build'
  }
}

// 写入到硬盘：./build/app.js, ./build/search.js
```

### output.hotUpdateChunkFilename

热更新块(Hot Update Chunk)的文件名。 他们在`output.path` 目录中
* [id] 被chunk的id替换
* [hash] 被编译(compilation)的hash替换。 (最后一个hash存储在记录中)

        默认值： "[id].[hash].hot-update.js"

### output.hotUpdateFunction

webpack 用于异步加载(async loading)热更新块(hot update chunk)的 JSONP 函数。

....还有好多就不详细记录了，具体去官网看吧，下面记录一个重点的：

### output.path

以绝对路径作为导出目录(必选项)

[hash] 被编译(compilation)的 hash 替换。

config.js
```javascript
output: {
    path: "/home/proj/public/assets",
    publicPath: "/assets/"
}
```

index.html
```html
<head>
  <link href="/assets/spinner.gif"/>
</head>
```
接下来是一个更复杂的例子，来说明对资源使用 CDN 和 hash。

config.js
```javascript
output: {
    path: "/home/proj/cdn/assets/[hash]",
    publicPath: "http://cdn.example.com/assets/[hash]/"
}
```


### output.sourceMapFilename

javascript文件SourceMap的文件名。 它们在output.path目录中。

* [file] 被JavaScript文件的文件名替换
* [id] 被chunk的id替换
* [hash] 被编译的(compilation)的hash替换

        默认值："[file].map"