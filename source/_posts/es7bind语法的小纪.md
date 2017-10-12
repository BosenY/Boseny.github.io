---
title: 关于es7bind语法的小纪
date: 2017-04-21 10:11:04
tags:
- JavaScript
- Ecmascript7
categories:
- JavaScript
---

# 有关es7 function bind syntax的东西

因为群里有大佬以前提到过，但是因为自己太菜了根本无法理解，所以就去学习了一下。。

## 概念

所谓的function bind syntax ，其实就是一个绑定的语法糖，就和箭头函数是类似的（箭头函数是声明函数时绑定this的语法糖，这里就有个坑，用箭头函数声明的方法就不能再使用::去绑定了，不会起作用。。）


## 作用

简单来说<strong>::</strong>有两种作用：

1. 当::出现在一个对象名的签名，且对象名后面紧跟着一个它的方法名的时候，作用就是把这个对象绑定为这个方法的this

```javascript
let obj = {
    method() {
        console.log(this)
    }
}
::obj.method
//等同于
obj.method.bind(obj)
```


2. 当::出现在对象和方法名之间的时候，将这个对象绑定为这个方法的this,当然，因为这个绑定后还是一个函数，所以也可以直接调用

```javascript
let obj = {
    foo: 'bar'
}
function method() {
    console.log(this.foo)
}
obj::method()
//等同于
method.call(obj)()



obj::method
//等同于
method.bind(obj)
```