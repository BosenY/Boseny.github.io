---
title: redux学习(3)
date: 2017-03-04 15:07:56
tags:
- react
- redux
categories:
- react
- redux
---


# redux学习(三)

基本快把react-redux都看完了，还差最后的几部。

## `<Provider>`组件

connect方法生成容器组件后，需要让容器组件拿到state对象，才能生成ui组件的参数

一种解决方法就是将state对象作为参数，传入容器组件。但是，这样做比较麻烦，尤其是容器组件可能在很深的层级，一级
级将state传下去就很麻烦

使用了provider组件后，可以让容器组件拿到state
<!--more-->
```javascript
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import todoApp from './reducers'
import App from './components/App'

let store = createStore(todoApp);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

上面的例子当中，使用`provider`组件在根组件外面包了一层，这样一来，app的所有组件就默认可以拿到state了