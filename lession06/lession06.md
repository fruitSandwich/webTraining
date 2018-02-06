# 前端框架及其实现

## 1.何为框架
框架（Framework）是一个框子——指其约束性，也是一个架子——指其支撑性。

IT语境中的框架，特指为解决一个开放性问题而设计的具有一定约束性的支撑结构。在此结构上可以根据具体问题扩展、安插更多的组成部分，从而更迅速和方便地构建完整的解决问题的方案。

框架是为解决开放性问题而设计的一套约束性支持结构。

## 2.常见的前端框架


前端都有哪些开放性问题？
- 实现页面设计
- 操作交互控制

对应的框架就有

- HTML/CSS框架，比如BootStrap,Material Design
- javascript框架，比如jquery，以及The big three(react,Angular,Vue)

用javascript在浏览器中操作页面元素(HTML DOM)经历了几个阶段：

1. 原生操作
```
var dom = document.getElementById('name');
dom.innerHTML = 'Homer';
dom.style.color = 'red';
```
2. jQuery（API精简，解决兼容性）
```
$('#name').text('Homer').css('color', 'red');
```
3. MVVM（变量和UI绑定，同步变化）
```
var person = {name: 'Bart',age: 12};
```

现在的前端框架大部分指的是JavaScript MVVM框架，其中以React、Angular、Vue为代表被称为前端三大框架。

## 3.todolist的实现
我们用jquery和Vue来实现一个简单的web程序：TODO List

主要功能：
- 将用户输入添加至待办项
- 可以对todolist进行分类，用户勾选即将待办项分入已完成组
- todolist的每一项可删除和编辑
- 将用户输入数据写入localStorage本地缓存，实现对输入数据的保存
- 可以清楚域名下本地缓存，并清空所有todolist项

### 3.1 jquery实现
```

```

### 3.2 vue实现
```

```
