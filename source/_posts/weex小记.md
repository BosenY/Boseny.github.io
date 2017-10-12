---
title: weex小记
date: 2017-02-23 14:19:24
tags:
- vue 
- weex
categories:
- vue
---

# weex学习(一)

上个学期学校实验周要求做一个项目，就考虑做个native端的，当时weex还不怎么稳定，看了半天网上的资料还是研究不出到底如何从构建到编译、打包，
于是用了React Native，但是由于react本身学习成本的问题，做的并不精致，好多东西都没用进去。 在公司实习的这段时间，公司的新项目都使用vue，在这个3个多月的时间当中，基本
学会了vue的整个概念和它的一些生态库，比方说vue-router和vuex，然后自己也了解了webpack打包编译的机制
，还将nodejs后端的koa自己写到了一个个人的小项目里面： [vue2-koa2的小demo](https://github.com/BosenY/koa2-vue2)  
感觉使用vue要比react清爽多了(关键还是学习成本低，上限还高)，现在看weex官方已经支持了vue语法编译，所以就学一下，准备毕设就拿这个开题。  
    
关于weex和vue： Vue.js 是 Evan You 开发的渐进式 JavaScript 框架，在易用性、灵活性和性能等方面都非常优秀。开发者能够通过撰写 *.vue 文件，基于 &lt;template&gt;, &lt;style&gt;, &lt;script&gt;   快速构建组件化的 web 应用。  
Vue.js 在 2016 年 10 月正式发布了 2.0 版本，该版本加入了 Virtual-DOM 和预编译器的设计，使得该框架在运行时能够脱离 HTML 和 CSS 解析，只依赖 JavaScript；同时 Virtual-DOM 也使得 Vue 2.x 渲染成原生 UI 成为了可能。
 <!--more--> 
weex就相对于react 和react native ，它就是vue的native版本，同时更加强大的是，它可以同时编译渲染web、android、ios三端。    

目前 Weex 与 Vue 正在展开官方合作，并将 Vue 2.x 作为内置的前端框架，Vue 也因此具备了开发原生应用的能力。



## 关于起步

由于我也是刚起步，不太能说明白，我是看的饿了么前端的一个妹子大神的教程才跟着一步一步配置出来的，链接在此:  

 * [快速开始weex之旅](https://zhuanlan.zhihu.com/p/25177344) 
 * [Weex 入坑指南：手把手编译 Playground](https://zhuanlan.zhihu.com/p/25227030) 


我是直接把weex团队的weex-hacknews改了一下，就可以成为自己开发时候的一个基础架子了。
然后可以自己去配置一下router、vuex等等的东西，然后编译调试打包。。。

