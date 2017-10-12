---
title: redux学习(1)
date: 2017-02-27 20:22:04
tags:
- react
- redux
categories:
- react
- redux
---


# Redux学习

因为我最先掌握的是vuex，反过头来去看学习成本相对较高的redux，可能效果会好一点。

redux是JavaScript状态容器，提供了可预测化的状态管理

redux由flux演变而来，但受elm的启发，避开了flux的复杂性

## 核心

应用当中的所有`state`都是以一个对象树的形式存储在一个一个单一的`store`当中，唯一改变`state`的办法就是触发`action`，一个描述发生什么的对象，为了描述`action`如何改变`state`树，你需要去编写`reducers`
<!--more-->


## 三大原则

redux可以用这三个基本原则来描述：

### 1.单一数据源

整个应用的state被存储在一棵 object tree中，并且这个object tree只存在于唯一一个store中。

### 2.state是只读的

唯一改变state的方法就是触发action，action是一个用于描述已发生事件的普通对象

### 3.使用纯函数来执行修改

为了描述action如何改变state tree ，你需要编写reducers。

reducer只是一些纯函数，它接收先前的state和action，并返回新的state。刚开始你可以只有一个reducer，随着应用的变大，你可以把它拆成多个小的
reducers，分别独立操作state tree的不同部分



### redux的一般写法

层次:
* 首先一般的redux要分为component和reducer两部分
* component当中只负责ui的设计，里面所有的方法和数据全部写成props，暴露给上层去调用
* reducer负责接收state和action两个参数，然后根据action的type属性进行不同的操作，返回不同的state
* 最终使用redux当中的一个叫做`createStore`方法来生成store，参数就是上面的reducer
* 然后在给子component传props的时候，调用store当中的dispatch方法来改变state，参数需要传action(因为state的初始值已经给出，不需要传)



但是这种普通的redux写法只能运用于特别简单的应用当中，如果要用到一个大型的react项目当中配合react-router一起使用，就要用到`react-redux`了