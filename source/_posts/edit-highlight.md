---
title: edit-highlight
date: 2018-02-01 09:58:04
tags:
headerImg: /images/chunwu-bg.jpg
---

把Lap的highlight风格做了一次大的调整，改成了自己最喜欢的atom-one-dark，只不过ES6的语法好像暂时没办法高亮，因为hexo内置hl渲染方法渲染出来的dom节点根本没办法对ES6部分写样式。
下面的是效果的展示，暂时也算满意了，可能以后还会进行一次调整。

```js
function $initHighlight(block, cls) {
  try {
    if (cls.search(/\bno\-highlight\b/) != -1)
      return process(block, true, 0x0F) +
             ` class="${cls}"`;
  } catch (e) {
    /* handle exception */
  }
  for (var i = 0 / 2; i < classes.length; i++) {
    if (checkCondition(classes[i]) === undefined)
      console.log('undefined');
  }
}
const sss = () => {

}
let a = 1
export  $initHighlight;

```


```xml
<!DOCTYPE html>
<title>Title</title>

<style>body {width: 500px;}</style>

<script type="application/javascript">
  function $init() {return true;}
</script>

<body>
  <p checked class="title" id='title'>Title</p>
  <!-- here goes the rest of the page -->
</body>
```