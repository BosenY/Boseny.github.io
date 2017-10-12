---
title: webpack2学习(五)
date: 2017-01-22 16:52:52
tags:
- webpack 
- node
categories:
- webpack
---

# 模块热替换(Hot Module Replacement)

模块热替换功能会在应用程序运行过程中替换、添加或删除模块，而无需重新加载页面。这使得你可以在独立模块变更后，
无需刷新整个页面，就可以更新这些模块，极大地加速了开发时间。

* 站在app角度
 1. app代码要求HMR runtime检查更新
 2. HMR runtime(异步) 下载更新，然后通知app代码更新可用
 3. app代码要求HMR runtime 应用更新
