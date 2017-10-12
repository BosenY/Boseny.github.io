---
title: ng过滤器
date: 2017-09-14 14:40:04
tags:
- JavaScript
- AngularJS
categories:
- AngularJS
---

# ng过滤器

所有的例子会写在这里：<a src="http://jsbin.com/vigiciresi/edit?html,js,output">例子</a>

首先学习一下ng1的过滤器的一个基本写法：

一个过滤器，不带参数的情况
```js
{{expression | filter}}
```
一个过滤器，带参数的情况
```js
{{expression | filter:arguments}}
```
一个过滤器，带多个参数的情况
```js
{{expression | filter: arg1: arg2: ...}}
```
多个过滤器，不带参数的情况
```js
{{expression | filter1 | filter2 | ...}}
```

先学习自定义的，现找出来10个：

## 1. currency
顾名思义，用于将数字转换为货币的
默认的话，是将数字转化成了当前使用语言环境的符号
当然也可以设置自定义符号，格式：
```js
{{ currency_expression | currency : symbol : fractionSize}}
```
其中symbol代表你要自定义的货币符号，fractionSize代表小数位的取舍量

## 2. date

根据要求将时间转换成字符串，开发当中经常用到，
格式化的字符串可以由以下原件组成：
* 'yyyy': 年份用4位数字表示(e.g. AD 1 => 0001, AD 2010 => 2010)
* 'yy': 年份用2位数字表示, 补全0 (00-99). (e.g. AD 2001 => 01, AD 2010 => 10)
* 'y': 年份用最少位数字表示, e.g. (AD 1 => 1, AD 199 => 199)
* 'MMMM': 月份 (January-December)
* 'MMM': 月份 (Jan-Dec)
* 'MM': 月份, 补全0 (01-12)
* 'M': 月份 (1-12)
* 'dd': 日期, 补全0 (01-31)
* 'd': 日期 (1-31)
* 'EEEE': 星期,(Sunday-Saturday)
* 'EEE': 星期, (Sun-Sat)
* 'HH': 小时, 补全0 (00-23)
* 'H': 补全0 (0-23)
* 'hh': AM/PM 表示的小时, 补全0 (01-12)
* 'h': AM/PM 表示的小时, (1-12)
* 'mm': 分钟, 补全0 (00-59)
* 'm': 分钟 (0-59)
* 'ss': 秒, 补全0 (00-59)
* 's': 秒 (0-59)
* 'sss': 毫秒, 补全0 (000-999)
* 'a': AM/PM 标记
* 'Z': 用4位表示时区的偏移 (-1200-+1200)
* 'ww': 周数, 补全0 (00-53). 01周是每年的包含第一个周四的周
* 'w': Week of year (0-53). 01周是每年的包含第一个周四的周
* 'G', 'GG', 'GGG': 时代的简写字符串 (e.g. 'AD')
* 'GGGG': 时代的完整字符串 (e.g. 'Anno Domini')

格式字符串还可以是下列预定义的本地化的格式之一:
* 'medium': en_US 地区的形式，等同于 'MMM d, y h:mm:ss a' (e.g. Sep 3, 2010 12:05:08 PM)
* 'short': en_US 地区的形式，等同于 'M/d/yy h:mm a' (e.g. 9/3/10 12:05 PM)
* 'fullDate': en_US 地区的形式，等同于 'EEEE, MMMM d, y' (e.g. Friday, September 3, 2010)
* 'longDate': en_US 地区的形式，等同于 'MMMM d, y' (e.g. September 3, 2010)
* 'mediumDate': en_US 地区的形式，等同于 'MMM d, y' (e.g. Sep 3, 2010)
* 'shortDate': en_US 地区的形式，等同于 'M/d/yy' (e.g. 9/3/10)
* 'mediumTime': en_US 地区的形式，等同于 'h:mm:ss a' (e.g. 12:05:08 PM)
* 'shortTime': en_US 地区的形式，等同于 'h:mm a' (e.g. 12:05 PM)

格式字符串可以包含文字。但是需要使用 ' 包裹进行转义 (e.g. "h 'in the morning'").
如果想使用单引号,则需要转义 - 举个例子, 在一行里有两个单引号 (e.g. "h 'o''clock'").




