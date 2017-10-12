---
title: react-router学习(1)
date: 2017-02-27 10:42:12
tags:
- react
categories:
- react
---


# react-router学习

关于配置什么的 请自行移至百度，下面就记录一下如何使用react-router

有关react-router的内容都是从这里学习和摘抄的：   [react中文文档](http://www.uprogrammer.cn) 

先写一个简单的例子来解释一下如何编写路由配置:
<!--more-->
```javascript
import React from 'react';
import { Router, Route, Link } from 'react-router'
const App = React.createClass({
  render() {
    return (
      <div>
        <h1>App</h1>
        <ul>
          <li><Link to="/about">About</Link></li>
          <li><Link to="/inbox">Inbox</Link></li>
        </ul>
        {this.props.children}
      </div>
    )
  }
})

const About = React.createClass({
  render() {
    return <h3>About</h3>
  }
})

const Inbox = React.createClass({
  render() {
    return (
      <div>
        <h2>Inbox</h2>
        {this.props.children || "Welcome to your Inbox"}
      </div>
    )
  }
})

const Message = React.createClass({
  render() {
    return <h3>Message {this.props.params.id}</h3>
  }
})

React.render((
  <Router>
    <Route path="/" component={App}>
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)

```

这里，最下面的render就是路由配置的一个具体的格式，其中主路由 `'/'` 是匹配的 `App`这个组件  
紧接着 `about` 和 `inbox` 是 `App` 的子组件 他们显示的位置就是 `this.props.children`的位置  
他们会在路由匹配成功后显示在对应的位置上面
然后是`inbox`里面的又一个子路由，这个路由还待了一个参数id，会跟着路由传过来，就是说 我们匹配到`/inbox/messages/xxx` 的时候 message这个组件就会被渲染出来，而且对应的`this.props.params.id`
也就是`xxx`

## 添加首页

仅仅这样写是不够的，比方说我没有给出子路由的时候`this.props.children`就是undefined 
这个时候我们就应该加入一个默认的路由去渲染，我们可以使用`IndexRouter` 来设置默认的页面

```javascript
import { IndexRoute } from 'react-router'

const Dashboard = React.createClass({
  render() {
    return <div>Welcome to the app!</div>
  }
})

React.render((
  <Router>
    <Route path="/" component={App}>
      {/* 当 url 为/时渲染 Dashboard */}
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

这样的话 当我们的url是`/`时，我们渲染的子路由 `this.props.children`的位置就是`Dashboard` 这个路由


如果我们想要将 `/inbox` 从 `/inbox/messages/:id`中去除，并且还能够让 `Message` 嵌套在 `App -> Inbox` 中渲染，那会非常赞。绝对路径可以让我们做到这一点。


```javascript
React.render((
  <Router>
    <Route path="/" component={App}>
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        {/* 使用 /messages/:id 替换 messages/:id */}
        <Route path="/messages/:id" component={Message} />
      </Route>
    </Route>
  </Router>
), document.body)
```

这样，我们的绝对路径就写好了，匹配`/messages/:id` 会依次渲染 `App -> Inbox -> Message`

但是，这时候又有了新的问题,当我们访问`/inbox/messages/5`的时候 我们就会看到错误，
这个的解决办法就是路由的重定向，我们使用`<Redirect> `来使这个url重新工作

```javascript
import { Redirect } from 'react-router'

React.render((
  <Router>
    <Route path="/" component={App}>
      <IndexRoute component={Dashboard} />
      <Route path="about" component={About} />
      <Route path="inbox" component={Inbox}>
        <Route path="/messages/:id" component={Message} />

        {/* 跳转 /inbox/messages/:id 到 /messages/:id */}
        <Redirect from="messages/:id" to="/messages/:id" />
      </Route>
    </Route>
  </Router>
), document.body)
```

这样的话，无论任何人点击`/inbox/messages/5`这个链接，它最终都会被重定向到`/messages/5`这个url上面  

## 进入和离开的钩子

`Router` 可以定义 `onEnter` 和 `onLeave` 两个钩子 ，这两个钩子会在页面跳转时触发，在验证权限的时候特别有用
，在路由跳转过程当中，`onLeav` 钩子会在所有将离开的路由中触发，从最下层的子路由开始直到最外层父路由结束。然后`onEnter` 钩子会从最外层的父路由开始直到最下层子路由结束


继续我们上面的例子，如果一个用户点击链接，从 /messages/5 跳转到 /about，下面是这些 hook 的执行顺序：

* /messages/:id 的 onLeave
* /inbox 的 onLeave
* /about 的 onEnter