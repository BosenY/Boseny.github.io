---
title: redux学习2
date: 2017-03-03 08:52:52
tags:
- react
- redux
categories:
- react
- redux
---


# react-redux学习

react-redux是一个专门用于在react项目中使用redux的一个库，
而且还有一定的规范和写法的推荐。还有额外的api需要去学习。

## 组件规范

### ui组件
首先react-redux将所有的组件分成了两大类：ui组件和容器组件

* UI组件只负责样式和ui
* 所有数据都由props来传递
* 不使用任何的redux

### 容器组件

* 管理所有的
* 使用redux
<!--more-->
### connect()


react-redux提供了一个connect方法 ，用来从ui组件生成一个容器组件

但是，如果只是简单的进行了对UI组件的包装的，并没有太多的作用，为了定义业务逻辑，需要给出下面两方面的信息。
1. 输入逻辑: 外部的数据(即state对象)如何转换为UI组件的参数
2. 输出逻辑: 用户发出的动作如何变为Action对象，从UI组件传出去

完整的API如下：

```javascript
import { connect } from 'react-redux'

const VisibleTodoList = connect(
  mapStateToProps,
  mapDispatchToProps
)(TodoList)
```

上面两个参数就是对应了输入逻辑和输出逻辑

前者负责输入逻辑，即将state映射到ui组件的参数(props)  
后者负责输出逻辑，将用户对ui组件的操作映射成action

### mapStateToProps()

`mapStateToProps` 是一个函数。它的作用就是像它的名字那样，建立一个从(外部的)`state`对象到 (UI组件的) `props`对象的映射关系

看一个count的例子:

```javascript
const mapStateToProps = (state) => {
  return {
    counter: state.counter
  }
}
```
这里的`mapStateToProps` 是一个fun ，它接收一个`state`作为参数，并且返回了一个obj，这个obj有一个counter属性，代表了ui组件当中的同名参数，然后这里也可以自己自定义一个fun去计算返回一个obj

`mapStateToProps`会订阅`store`，每当你的`state`更新的时候，就会自动执行，重新计算ui组件的参数，从而触发ui组件的重新渲染。而不需要使用`subscribe`这个方法了

除了可以传一个参数state以外，还可以使用第二个参数，代表容器组件的props对象
然后容器组件的参数发生变化，也会引发UI组件的重新渲染

### mapDispatchToProps()

`mapDispatchToProps`是connect的第二个参数，用来建立UI组件的参数到`store.dispatch`方法的映射，
定义了ui组件发出action的方法

如果`mapDispatchToProps`是一个对象，它的每个键名也就是对应ui组件的同名参数，数值应该是一个函数，会被当做Action creator，返回的Action 会由redux自动发出，eg:

```javascript
const mapDispatchToProps = {
  onClick: (filter) => {
    type: 'SET_VISIBILITY_FILTER',
    filter: filter
  };
}
```

上面的就是一个例子，上面的`mapDispatchToProps`这个对象当中的onClick这个键值其实就是一个UI组件的props