# javascript面向对象与函数式

前面我们说到JavaScript的“编程风格”是函数式编程和面向对象编程的一种混合体。再说函数式和面向对象之前，可以先探讨一下编程风格也就是编程范式：<a href='http://blog.fruitsandwich.cc/pardigm-oop-functional/'>编程范式与设计模式</a>


## 1.javascript面向对象

“面向对象编程”（Object Oriented Programming，缩写为OOP）是目前主流的编程范式。它的核心思想是将真实世界中各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。

### 1.1构造函数与new
面向对象编程”的第一步，就是要生成“对象”。

“对象”是单个实物的抽象，通常需要一个模板，表示某一类实物的共同特征，然后“对象”根据这个模板生成。

典型的面向对象编程语言（比如 C++ 和 Java），存在“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。

JavaScript语言使用构造函数（constructor）作为对象的模板。所谓“构造函数”，就是专门用来生成“对象”的函数。它提供模板，描述对象的基本结构。一个构造函数，可以生成多个对象，这些对象都有相同的结构。

构造函数的写法就是一个普通的函数，但是有自己的特征和用法。

```
var Vehicle = function () {
  this.price = 1000;
};
```

> 函数体内部使用了this关键字，代表了所要生成的对象实例。

>生成对象的时候，必需用new命令，调用Vehicle函数。

```
var v = new Vehicle();
v.price // 1000
```

使用new命令时，根据需要，构造函数也可以接受参数。

```
var Vehicle = function (p) {
  this.price = p;
};

var v = new Vehicle(500);
```

如果忘了使用new命令，直接调用构造函数，构造函数就变成了普通函数，并不会生成实例对象。而且由于后面会说到的原因，this这时代表全局对象，将造成一些意想不到的结果。

```
var Vehicle = function (){
  this.price = 1000;
};

var v = Vehicle();
v.price
// Uncaught TypeError: Cannot read property 'price' of undefined

price
// 1000
```

### 1.2this关键字
this关键字是一个非常重要的语法点。毫不夸张地说，不理解它的含义，大部分开发任务都无法完成。

首先，this总是返回一个对象，简单说，就是返回属性或方法“当前”所在的对象。

```
this.property
```
上面代码中，this就代表property属性当前所在的对象。

下面是一个实际的例子。

```
var person = {
  name: '张三',
  describe: function () {
    return '姓名：'+ this.name;
  }
};

person.describe()
// "姓名：张三"
```

上面代码中，this.name表示describe方法所在的当前对象的name属性。调用person.describe方法时，describe方法所在的当前对象是person，所以就是调用person.name。

由于对象的属性可以赋给另一个对象，所以属性所在的当前对象是可变的，即this的指向是可变的。

```
var A = {
  name: '张三',
  describe: function () {
    return '姓名：'+ this.name;
  }
};

var B = {
  name: '李四'
};

B.describe = A.describe;
B.describe()
// "姓名：李四"
```
上面代码中，A.describe属性被赋给B，于是B.describe就表示describe方法所在的当前对象是B，所以this.name就指向B.name。

稍稍重构这个例子，this的动态指向就能看得更清楚。

```
function f() {
  return '姓名：'+ this.name;
}

var A = {
  name: '张三',
  describe: f
};

var B = {
  name: '李四',
  describe: f
};

A.describe() // "姓名：张三"
B.describe() // "姓名：李四"
```

再看一个网页编程的例子。

```
<input type="text" name="age" size=3 onChange="validate(this, 18, 99);">

<script>
function validate(obj, lowval, hival){
  if ((obj.value < lowval) || (obj.value > hival))
    console.log('Invalid Value!');
}
</script>
```
上面代码是一个文本输入框，每当用户输入一个值，就会调用onChange回调函数，验证这个值是否在指定范围。回调函数传入this，就代表传入当前对象（即文本框），然后就可以从this.value上面读到用户的输入值。


如果一个函数在全局环境中运行，那么this就是指顶层对象（浏览器中为window对象）

```
function f() {
  return this;
}

f() === window // true
```
