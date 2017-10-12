---
title: react-router学习(2)
date: 2017-02-27 14:42:12
tags:
- react
categories:
- react
---

# react router学习(2)

## 路由匹配原理

路由有三个属性来决定是否匹配一个url

1. 嵌套关系
2. 它的路径语法
3. 它的优先级

### 嵌套关系

React Router 使用路由嵌套的概念来让你定义 view 的嵌套集合，当一个给定的 `URL`
 被调用时，整个集合中（命中的部分）都会被渲染。嵌套路由被描述成一种树形结构。
 `React Router` 会深度优先遍历整个路由配置来寻找一个与给定的 `URL` 相匹配的路由。

### 它的路径语法
* :paramName 匹配一段位于`/`、`?`、`#`之后的url，命中的部分将被作为参数
* ()  在它内部的内容被认为是可选的
* * 匹配任意字符(非贪婪的)直到命中下一个字符或者整个url的末尾，并创建一个`splat`参数

### 它的优先级

路由算法会根据定义的顺序自顶向下匹配路由。因此，当你拥有两个兄弟路由节点配置时，你必须确认前一个路由不会匹配后一个路由中的路径。 例如，千万不要这么做：

```javascript
<Route path="/comments" ... />
<Redirect from="/comments" ... />
```



## History

History用来去监听浏览器地址栏的变化，并解析这个url转化为location对象，然后router使用它去匹配路由，然后渲染相应的组件

### History的模式

常用的有三种，当然你也可以去自定义

1. browserHistory
2. hashHistory
3. createMemoryHistory


用法：

你先从react-router当中引用他们

```javascript
import { browserHistory } from 'react-router'
```
然后将它们传递给`<Router>`
```javascript
render(
  <Router history={browserHistory} routes={routes} />,
  document.getElementById('app')
)
```


## browserHistory 
browserHistory是用的比较多的一种模式 它使用浏览器中的historyAPI用于处理URL，创建一个真实的url


看到这里正好还解决了我一个肯长时间百思不得其解的问题，就是我vue写的项目打包放到Nginx服务器上面后，路由匹配会报错，然后按照
这里给Nginx反向代理的方法重新配置了服务器，发现错误就解决了。

## hashHistory
hashHistory 使用url中的hash(#)部分去创建形如 example.com/#/some/path 的路由。
但由于有一个`#`号 所以看起来会比较丑，所以不建议线上使用

## createMemoryHistory

Memory History不会在地址栏被操作或读取。
 

它非常适合测试和其他的渲染环境(React Native)

和另外两种history的一点不同的是你必须创建它，这种方式便于测试

```javascript
const history = createMemoryHistory(location)
```


## Index Links


除了路由有默认的 link也有，如果你使用了`<Link to="/">Home</Link>`,它会一直处于激活状态，
因为所以的url的开头都是`/`。这个确实是个问题，因为我们仅仅希望在`home`被渲染后，激发并链接到它

如果需要在`home`路由被渲染后才激活 就用`<IndexLink to="/">Home</IndexLink>
`

就先记这么多，以后遇到坑在补