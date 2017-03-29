# javascript面向对象与函数式

“面向对象编程”（Object Oriented Programming，缩写为OOP）是目前主流的编程范式。它的核心思想是将真实世界中各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。

## 1.javascript对象的生成
面向对象编程”的第一步，就是要生成“对象”。

“对象”是单个实物的抽象，通常需要一个模板，表示某一类实物的共同特征，然后“对象”根据这个模板生成。

典型的面向对象编程语言（比如 C++ 和 Java），存在“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。

JavaScript的原型链和Java的Class区别就在，它没有“Class”的概念，所有对象都是实例，所谓继承关系不过是把一个对象的原型指向另一个对象而已。

比如：

```
var bird = {
    fly: function () {
        console.log(this.name + ' is flying...');
    }
};
var owl = {
  name:'owl'
}

owl.__proto__ = bird;
owl.fly()//owl is flying...
```


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

## 2.this与prototype

### 2.1this关键字的涵义
this关键字是一个非常重要的语法点。不理解它的含义，大部分开发任务都无法完成。

this总是返回一个对象，简单说，就是返回属性或方法“当前”所在的对象。

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

上面代码中，函数f在全局环境运行，它内部的this就指向顶层对象window。

可以近似地认为，this是所有函数运行时的一个隐藏参数，指向函数的运行环境。

### 2.2this的使用场合

1. 全局环境
  在全局环境使用this，它指的就是顶层对象window。

  ```
  this === window // true

  function f() {
    console.log(this === window); // true
  }
  ```

  上面代码说明，不管是不是在函数内部，只要是在全局环境下运行，this就是指顶层对象window。

2. 构造函数

  构造函数中的this，指的是实例对象。

  ```
  var Obj = function (p) {
    this.p = p;
  };

  Obj.prototype.m = function() {
    return this.p;
  };
  ```

  上面代码定义了一个构造函数Obj。由于this指向实例对象，所以在构造函数内部定义this.p，就相当于定义实例对象有一个p属性；然后m方法可以返回这个p属性。

  ```
  var o = new Obj('Hello World!');

  o.p // "Hello World!"
  o.m() // "Hello World!"
  ```
3. 对象的方法
  当A对象的方法被赋予B对象，该方法中的this就从指向A对象变成了指向B对象。所以要特别小心，将某个对象的方法赋值给另一个对象，会改变this的指向。

  ```
  var a = {
    b: {
      m: function() {
        console.log(this.p);
      },
      p: 'Hello'
    }
  };

  var hello = a.b.m;
  hello() // undefined
  ```

  上面代码中，m是多层对象内部的一个方法。为求简便，将其赋值给hello变量，结果调用时，this指向了顶层对象。为了避免这个问题，可以只将m所在的对象赋值给hello，这样调用时，this的指向就不会变。

  ```
  var hello = a.b;
  hello.m() // Hello
  ```

### 2.3prototype 对象

JavaScript的每个对象都继承另一个对象，后者称为“原型”（prototype）对象。只有null除外，它没有自己的原型对象。

原型对象上的所有属性和方法，都能被派生对象共享。这就是JavaScript继承机制的基本设计。

通过构造函数生成实例对象时，会自动为实例对象分配原型对象。<b>每一个构造函数都有一个prototype属性</b>，这个属性就是实例对象的原型对象。

```
function Animal (name) {
  this.name = name;
}

Animal.prototype.color = 'black';

var bear1 = new Animal('熊大');
var bear2 = new Animal('熊二');

bear1.color // 'black'
bear2.color // 'black'
```

上面代码中，构造函数Animal的prototype对象，就是实例对象bear1和bear2的原型对象。在原型对象上添加一个color属性。结果，实例对象都能读取该属性。

原型对象的属性不是实例对象自身的属性。只要修改原型对象，变动就立刻会体现在所有实例对象上。

```
Animal.prototype.color = 'yellow';

bear1.color // "yellow"
bear2.color // "yellow"
```

上面代码中，原型对象的color属性的值变为yellow，两个实例对象的color属性立刻跟着变了。这是因为实例对象其实没有color属性，都是读取原型对象的color属性。也就是说，当实例对象本身没有某个属性或方法的时候，它会到构造函数的prototype属性指向的对象，去寻找该属性或方法。这就是原型对象的特殊之处。

如果实例对象自身就有某个属性或方法，它就不会再去原型对象寻找这个属性或方法。

```
bear1.color = 'black';

bear2.color // 'yellow'
Animal.prototype.color // "yellow";
```

上面代码中，实例对象bear1添加color属性为black，就使得它不再去原型对象读取color属性，后者的值依然为yellow。

## 3.es6/es2015 中的Class
JavaScript语言的传统方法是通过构造函数，定义并生成新对象。下面是一个例子。

```
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```

上面这种写法跟传统的面向对象语言（比如C++和Java）差异很大，很容易让新学习这门语言的程序员感到困惑。

ES6提供了更接近传统语言的写法，引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看作只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用ES6的“类”改写，就是下面这样。

```
//定义类
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

更多关于es2015中的Class相关:<a href='http://es6.ruanyifeng.com/#docs/class'>ECMAScript 6 入门</a>

## 4.编程范式与设计模式

前面我们说到JavaScript的“编程风格”是函数式编程和面向对象编程的一种混合体。

函数式和面向对象是两种不同的编程范式，而不同的编程范式有着不同的世界观，在编程过程中会引导人民带着特有的倾向和思路去分析和解决问题。
<a href='http://blog.fruitsandwich.cc/pardigm-oop-functional/'>编程范式与设计模式</a>
