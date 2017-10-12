---
title: ng-router
date: 2017-09-15 16:16:28
tags:
- JavaScript
- AngularJS
categories:
- AngularJS
---

# ng-router

ng-router可以把angular1变成一个spa应用，在页面上的原理就是渲染了不同的controller来实现不同的路由，具体实例代码如下：
```js
<html>
    <head>
        <meta charset="utf-8">
        <title>AngularJS 路由实例 - 菜鸟教程</title>
    </head>
    <body ng-app='routingDemoApp'>

        <h2>AngularJS 路由应用</h2>
        <ul>
            <li><a href="#/">首页</a></li>
            <li><a href="#/computers">电脑</a></li>
            <li><a href="#/printers">打印机</a></li>
            <li><a href="#/blabla">其他</a></li>
        </ul>

        <div ng-view></div>
        <script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script>
        <script src="http://apps.bdimg.com/libs/angular-route/1.3.13/angular-route.js"></script>
        <script>
            angular.module('routingDemoApp',['ngRoute'])
            .config(['$routeProvider', function($routeProvider){
                $routeProvider
                .when('/',{template:'这是首页页面'})
                .when('/computers',{template:'这是电脑分类页面'})
                .when('/printers',{template:'这是打印机页面'})
                .otherwise({redirectTo:'/'});
            }]);
        </script>


    </body>
</html>
```

首先，载入了实现路由的js文件：angular-route.js； 然后，包含了ngRoute模块作为主应用模块的依赖模块。
```js
angular.module('routingDemoApp',['ngRoute'])
```
使用ngView指令
```js
<div ng-view></div>
```
该div内html会根据路由的变化来变化。

然后配置$routeProvider, 用于定义我们的路由规则

```js
module.config(['$routeProvider', function($routeProvider){
    $routeProvider
        .when('/',{template:'这是首页页面'})
        .when('/computers',{template:'这是电脑分类页面'})
        .when('/printers',{template:'这是打印机页面'})
        .otherwise({redirectTo:'/'});
}]);
```

