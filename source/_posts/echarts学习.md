---
title: echarts学习
date: 2017-03-09 14:16:06
type: "tags"
tags:
- JavaScript
- echarts
categories:
- JavaScript
---

# echarts api学习

因为暂时项目当中使用的是echarts-for-react插件，所以暂时先不考虑了解echarts原生对象的一些方法，
先从配置项开始学习。

首先是初始化一个echarts对象，然后这个对象去调用echarts的setOption方法，配置展示的信息。

setOption用来写echarts图表的配置信息

### title 
标题组件，包含主标题和副标题
```javascript
title: {
    show: //是否显示标题组件 默认是true
    text://主标题文本
    link: //主标题的超文本链接，也可以用在react的路由跳转
    target: //指定打开超链接的方式 默认是新窗口
    textStyle: {
        color: // 主标题颜色
        fontWeight: //主标题文字字体粗细
        fontFamily: // 主标题文字字体
        fontSize: //主标题文字字体大小

    }
    textAligin: //标题文本水平对齐方式
    textBaseline: //标题文本垂直对齐方式
    subtext: //副标题文本  副标题也有主标题同样的配置，这里就不记录了
    sublink: //富文本超链接
    
},

//api太多啦，也不记载这么多了，具体的自己去官网看吧，自己就记录一些第一层的配置信息

legend: //图例组件，展现了不同系列的标记(symbol)，颜色和名字。可以通过点击图例控制哪些系列不显示

grid: //直角坐标系内绘图网格，单个grid内最多可以放置上下两个x轴，左右两个y轴。可以在网格上绘制折线图、柱状图、散点图(气泡图)，在echarts3当中可以存在任意多个grid组件

xAxis: // 直角坐标系grid中的x轴，一般情况下grid组件最多只能放左右两个x轴，多于两个x轴需要通过配置offset防止同个位置多个x轴的重叠

yAxis: //直角坐标系 grid 中的 y 轴，一般情况下单个 grid 组件最多只能放左右两个 y 轴，多于两个 y 轴需要通过配置 offset 属性防止同个位置多个 Y 轴的重叠。

polar: // 极坐标系，可以用于散点图和折线图，每个极坐标拥有一个角度轴和一个半径轴

radiusAxis: //极坐标系的径向轴

angleAxis:  //极坐标系的角度轴

radar : // 雷达坐标系组件

dataZoom: // 用于区域缩放，从而能自由关注细节的数据信息，或者概览数据整体，或者去除离群点的影响

tooltip: //提示框组件

```