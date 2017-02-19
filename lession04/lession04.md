# javascript语法和标准库

## 1.基础语法
### 1.1语句
JavaScript的语法和Java类似，每个语句以;结束。但是，JavaScript并不强制要求在每个语句的结尾加;，JavaScript宿主引擎会自动在每个语句的结尾补上;。

```
var a = 1 + 3;
```

这条语句先用var命令，声明了变量a，然后将1 + 3的运算结果赋值给变量a


### 1.2变量
变量的声明和赋值，是分开的两个步骤，上面的代码将它们合在了一起，实际的步骤是下面这样。

```
var a;
a = 1;
```

如果只是声明变量而没有赋值，则该变量的值是undefined。undefined是一个JavaScript关键字，表示“无定义”。

```
var a;
a // undefined
```

JavaScirpt是一种动态类型语言，也就是说，变量的类型没有限制，可以赋予各种类型的值。

```
var a = 1;
a = 'hello';
```

> <b>变量提升</b>:
JavaScript引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

```
console.log(a);
var a = 1;
```

上面代码首先使用console.log方法，在控制台（console）显示变量a的值。这时变量a还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。

```
var a;
console.log(a);
a = 1;
```

变量提升只对var命令声明的变量有效，如果一个变量不是用var命令声明的，就不会发生变量提升。


```
console.log(b);
b = 1;
```

### 1.3 注释
和java一样，javascript的注释有单行和多行，分别是:

```
// 这是单行注释

/*
 这是
 多行
 注释
*/
```

### 1.4 区块
JavaScript使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

> 与大多数编程语言不一样，JavaScript的区块不构成单独的作用域（scope）。也就是说，区块中的变量与区块外的变量，属于同一个作用域。

```
{
  var a = 1;
}

a // 1
```

上面代码在区块内部，声明并赋值了变量a，然后在区块外部，变量a依然有效，这说明区块不构成单独的作用域，与不使用区块的情况没有任何区别。

注意，没有块作用域很容易污染全局变量：

```
if(false){
  var a = 1;
}
a//1
for(var i=0;i<3;i++){
}
i//3
```

## 2.数据类型

JavaScript的数据类型，共有六种。

- 数值（number）：整数和小数（比如1和3.14）
- 字符串（string）：字符组成的文本（比如”Hello World”）
- 布尔值（boolean）：true（真）和false（假）两个特定值
- undefined：表示“未定义”或不存在，即此处目前没有任何值
- null：表示空缺，即此处应该有一个值，但目前为空
- 对象（object）：各种值组成的集合



### 2.1 数值
JavaScript内部，所有数字都是以64位浮点数形式储存，整数和浮点数都用Number类型表示，所以1和1.0是相同的：

```
1 === 1.0//true
```

由于浮点数不是精确的值，所以涉及小数的比较和运算要特别小心。

```
0.1 + 0.2 === 0.3
// false

0.3 / 0.1
// 2.9999999999999996

(0.3 - 0.2) === (0.2 - 0.1)
// false
```

数值范围：2的-1023次方到2的1024次方

如果超出数值范围JavaScript会返回Infinity(表示无穷)，比如

```
1/0 //Infinity
```

JavaScript提供Number对象的MAX_VALUE和MIN_VALUE属性表示最大值和最小值


JavaScript使用NAN“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。

```
5 - 'x' // NaN
```

另外，一些数学函数的运算结果会出现NaN。

```
Math.acos(2) // NaN
Math.log(-1) // NaN
Math.sqrt(-1) // NaN
```

NaN不等于任何值，包括它本身。

```
NaN === NaN // false
```

NaN与任何数（包括它自己）的运算，得到的都是NaN。

```
NaN + 32 // NaN
NaN - 32 // NaN
NaN * 32 // NaN
NaN / 32 // NaN
```

isNaN方法可以用来判断一个值是否为NaN。

```
isNaN(NaN) // true
isNaN(123) // false
```

Number 相关详细资料和教程：
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number
- http://www.w3school.com.cn/jsref/jsref_obj_number.asp

### 2.2 字符串
字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。

```
'abc'
"abc"
```

如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。

```
var longString = "Long \
long \
long \
string";

longString
// "Long long long string"
```

字符串可以被视为字符数组，因此可以使用数组的方括号运算符

```
var s = 'hello';
s[0] // "h"
s[1] // "e"
s[4] // "o"

// 直接对字符串使用方括号运算符
'hello'[1] // "e"
```

需要特别注意的是，字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果：

```
var s = 'Test';
s[0] = 'X';
alert(s); // s仍然为'Test'
```

JavaScript为字符串提供了一些常用方法，注意，调用这些方法本身不会改变原有字符串的内容，而是返回一个新字符串。

- toUpperCase
- toLowerCase
- substring
- concat
- split
- 等等

String 相关详细资料和教程：
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String
- http://www.w3school.com.cn/jsref/jsref_obj_string.asp

### 2.3 对象

对象（object）是JavaScript的核心概念，也是最重要的数据类型。JavaScript的所有数据都可以被视为对象。

简单说，所谓对象，就是一种无序的数据集合，由若干个“键值对”（key-value）构成。

```
var o = {
  p: 'Hello World'
};
```

对象的生成方法，通常有三种方法。除了像上面那样直接使用大括号生成（{}），还可以用new命令生成一个Object对象的实例，或者使用Object.create方法生成。

```
var o1 = {};
var o2 = new Object();
var o3 = Object.create(Object.prototype);
```

上面三行语句是等价的。一般来说，第一种采用大括号的写法比较简洁，第二种采用构造函数的写法清晰地表示了意图，第三种写法一般用在需要对象继承的场合。

对象的所有键名都是字符串，所以加不加引号都可以：

```
var a = {'p':'hello'}
var b = {p:'world'}
a.p//"hello"
b.p//"world"
```

对象的每一个“键名”又称为“属性”（property），它的“键值”可以是任何数据类型。如果一个属性的值为函数，通常把这个属性称为“方法”，它可以像函数那样调用。

```
var o = {
  p: function (x) {
    return 2 * x;
  }
};

o.p(1)
// 2
```

如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址。修改其中一个变量，会影响到其他所有变量。

```
var o1 = {};
var o2 = o1;

o1.a = 1;
o2.a // 1

o2.b = 2;
o1.b // 2
```

读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。

```
var o = {
  p: 'Hello World'
};

o.p // "Hello World"
o['p'] // "Hello World"
```

>注意，如果使用方括号运算符，键名必须放在引号里面，否则会被当作变量处理。

方括号运算符内部可以使用表达式

```
o['hello' + ' world']
o[3 + 3]
```

in 运算符：

in运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回true，否则返回false。

```
var o = { p: 1 };
'p' in o // true
```

在JavaScript语言中，所有全局变量都是顶层对象（浏览器的顶层对象就是window对象）的属性，因此可以用in运算符判断，一个全局变量是否存在。
```
'x' in window
```

for ... in循环：

for...in循环用来遍历一个对象的全部属性。

```
var o = {a: 1, b: 2, c: 3};

for (var i in o) {
  console.log(o[i]);
}
// 1
// 2
// 3
```


### 2.4.数组

JavaScript的Array可以包含任意数据类型，并通过索引来访问每个元素。

要取得Array的长度，直接访问length属性：

```
var arr = [1, 2, 3.14, 'Hello', null, true];
arr.length; // 6
```

> 注意，直接给Array的length赋一个新的值会导致Array大小的变化：

```
var arr = [1, 2, 3];
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```

Array可以通过索引把对应的元素修改为新的值，因此，对Array的索引进行赋值会直接修改这个Array：

```
var arr = ['A', 'B', 'C'];
arr[1] = 99;
arr; // arr现在变为['A', 99, 'C']
```

>注意，如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化：

```
var arr = [1, 2, 3];
arr[5] = 'x';
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

大多数其他编程语言不允许直接改变数组的大小，越界访问索引会报错。然而，JavaScript的Array却不会有任何错误。在编写代码时，不建议直接修改Array的大小，访问索引时要确保索引不会越界。

数组的遍历:

```
var colors = ['red', 'green', 'blue'];
colors.forEach(function (item, index, array) {
  console.log(item,index);
});
//或
for(var i = 0;i<colors.length;i++){
	console.log(colors[i]);
}
//因为Array是一种特殊的对象，一种键名为数字的对象，所以也可以用for...in来遍历数组
for (var i in colors) {
  console.log(colors[i]);
}
但for...in不仅会遍历数组所有的数字键，还会遍历非数字键
colors.a = 123
for (var i in colors) {
  console.log(colors[i]);
}
//red
//green
//blue
//123
```


数组对象方法有两类，一类调用后会改变自身的值，一类调用后不改变自身返回一个新的数组。

会改变自身的方法：

Array.prototype.fill(value,start,end):将一个数组的所有元素从开始索引填充到具有静态值的结束索引。返回值：改变后的数组

Array.prototype.push(element1, ..., elementN):将一个或多个元素添加到数组的末尾。返回值：数组的新长度。

Array.prototype.pop():从数组中删除最后一个元素，并返回该元素的值。此方法更改数组的长度。返回值：从数组中删除的元素; undefined 如果数组为空。

Array.prototype.reverse():颠倒数组中元素的位置

Array.prototype.splice(start, deleteCount, item1, item2, ...):通过删除现有元素和/或添加新元素来更改数组的内容。

```
var arr = [1,2,3,4,5,7,8]
arr.splice(2,1)//[3]
arr//[1, 2, 4, 5, 7, 8]
arr.splice(2,2,'one','two')//[4, 5]
arr//[1, 2, "one", "two", 7, 8]
```

Array.prototype.sort(compareFunction):对数组的元素进行排序，并返回数组

```
var arr = [{value:3,text:'hello'},{value:1,text:'world'},{value:2,text:'!'}]
arr.forEach(function(item){
	console.log(item)
})
//Object {value: 3, text: "hello"}
//Object {value: 1, text: "world"}
//Object {value: 2, text: "!"}
arr.sort(function(a,b){
	return a.value - b.value
})
//Object {value: 1, text: "world"}
//Object {value: 2, text: "!"}
//Object {value: 3, text: "hello"}
```


不会改变自身的方法:

Array.prototype.concat():返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组。

```
var arr1 = ["a", "b", "c"];
var arr2 = ["d", "e", "f"];

var arr3 = arr1.concat(arr2);
```

Array.prototype.includes(searchElement, fromIndex):用来判断当前数组是否包含某指定的值，如果是，则返回 true，否则返回 false。

Array.prototype.join(separator):将数组（或一个类数组对象）的所有元素连接到一个字符串中。

```
var a = ['Wind', 'Rain', 'Fire'];

a.join();
// 默认为 ","
// 'Wind,Rain,Fire'
```

Array.prototype.slice(begin,end):将数组的一部分浅拷贝, 返回到从开始到结束（不包括结束）选择的新数组对象。

```
var arr = [1,2,3,4,5]
var sliced = arr.slice(1,3)
arr//[1, 2, 3, 4, 5]
sliced//[2, 3]
```

Array.prototype.indexOf():返回在数组中可以找到给定元素的第一个索引，如果不存在，则返回-1。




## 3.函数
### 3.1 声明和使用
JavaScript有三种方法，可以声明一个函数。

#### function命令

function命令声明的代码区块，就是一个函数。function命令后面是函数名，函数名后面是一对圆括号，里面是传入函数的参数。函数体放在大括号里面。

```
function print(s) {
  console.log(s);
}
print('hello')
```

#### 函数表达式

```
var print = function(s) {
  console.log(s);
};
```
这种写法将一个匿名函数赋值给变量。这时，这个匿名函数又称函数表达式（Function Expression），因为赋值语句的等号右侧只能放表达式。

#### Function构造函数
```
var add = new Function(
  'x',
  'y',
  'return x + y'
);

// 等同于

function add(x, y) {
  return x + y;
}
```
可以传递任意数量的参数给Function构造函数，只有最后一个参数会被当做函数体，如果只有一个参数，该参数就是函数体。

#### 重复声明
如果同一个函数被多次声明，后面的声明就会覆盖前面的声明。

```
function f() {
  console.log(1);
}
f() // 2

function f() {
  console.log(2);
}
f() // 2
```
后一次的函数声明覆盖了前面一次。而且，由于函数名的提升，前一次声明在任何时候都是无效的，这一点要特别注意。

>很多时候如果在html中引用了多个script，而script中含有同名函数，那么前面的函数效果就会被覆盖而导致不可预测的效果，所以html中script引用的顺序非常重要。但尽可能的要避免使用全局变量。

### 3.2 函数名提升

JavaScript引擎将函数名视同变量名，所以采用function命令声明函数时，整个函数会像变量声明一样，被提升到代码头部。所以，下面的代码不会报错。
```
f();

function f() {}
```

但是，如果采用赋值语句定义函数，JavaScript就会报错。

```
f();
var f = function (){};
// TypeError: undefined is not a function
```

上面的代码等同于下面的形式。

```
var f;
f();
f = function () {};
```

如果同时采用function命令和赋值语句声明同一个函数，最后总是采用赋值语句的定义。

```
var f = function() {
  console.log('1');
}

function f() {
  console.log('2');
}

f() // 1
```

### 3.3第一等公民
JavaScript语言将函数看作一种值，与其它值（数值、字符串、布尔值等等）地位相同。凡是可以使用值的地方，就能使用函数。比如，可以把函数赋值给变量和对象的属性，也可以当作参数传入其他函数，或者作为函数的结果返回。函数只是一个可以执行的值，此外并无特殊之处。

由于函数与其他数据类型地位平等，所以在JavaScript语言中又称函数为第一等公民。

```
function add(x, y) {
  return x + y;
}

// 将函数赋值给一个变量
var operator = add;

// 将函数作为参数和返回值
function a(op){
  return op;
}
a(add)(1, 1)
// 2
```

### 3.4作用域
作用域（scope）指的是变量存在的范围。Javascript只有两种作用域：一种是全局作用域，变量在整个程序中一直存在，所有地方都可以读取；另一种是函数作用域，变量只在函数内部存在。

在函数外部声明的变量就是全局变量（global variable），它可以在函数内部读取。

```
var v = 1;

function f(){
  console.log(v);
}

f()
// 1
```

上面的代码表明，函数f内部可以读取全局变量v。

在函数内部定义的变量，外部无法读取，称为“局部变量”（local variable）。

```
function f(){
  var v = 1;
}

v // ReferenceError: v is not defined
```


与全局作用域一样，函数作用域内部也会产生“变量提升”现象。var命令声明的变量，不管在什么位置，变量声明都会被提升到函数体的头部。

```
function foo(x) {
  if (x > 100) {
    var tmp = x - 100;
  }
}
```

等同于

```
function foo(x) {
  var tmp;
  if (x > 100) {
    tmp = x - 100;
  };
}
```

函数本身也是一个值，也有自己的作用域。它的作用域与变量一样，就是其<b>声明时</b>所在的作用域，与其运行时所在的作用域无关。

```
var a = 1;
var x = function () {
  console.log(a);
};

function f() {
  var a = 2;
  x();
}

f() // 1
```
上面代码中，函数x是在函数f的外部声明的，所以它的作用域绑定外层，内部变量a不会到函数f体内取值，所以输出1，而不是2。

> 总之，函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。

很容易犯错的一点是，如果函数A调用函数B，却没考虑到函数B不会引用函数A的内部变量。

```
var x = function () {
  console.log(a);
};

function y(f) {
  var a = 2;
  f();
}

y(x)
// ReferenceError: a is not defined
```
上面代码将函数x作为参数，传入函数y。但是，函数x是在函数y体外声明的，作用域绑定外层，因此找不到函数y的内部变量a，导致报错。

同样的，函数体内部声明的函数，作用域绑定函数体内部。

```
function foo() {
  var x = 1;
  function bar() {
    console.log(x);
  }
  return bar;
}

var x = 2;
var f = foo();
f() // 1
```

上面代码中，函数foo内部声明了一个函数bar，bar的作用域绑定foo。当我们在foo外部取出bar执行时，变量x指向的是foo内部的x，而不是foo外部的x。正是这种机制，构成了“闭包”现象。

#### 3.5闭包
所谓“闭包”，指的是一个拥有许多变量和绑定了这些变量的环境的表达式（通常是一个函数）。

```
function f1() {
  var n = 999;
  function f2() {
    console.log(n);
  }
  return f2;
}

var result = f1();
result(); // 999
```
上面代码中，函数f1的返回值就是函数f2，由于f2可以读取f1的内部变量，所以可以在外部获得f1的内部变量了。

闭包就是函数f2，即能够读取其他函数内部变量的函数。

闭包最大的特点，就是它可以“记住”诞生的环境，比如f2记住了它诞生的环境f1，所以从f2可以得到f1的内部变量。在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

闭包的最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在。

```
function createIncrementor(start) {
  return function () {
    return start++;
  };
}

var inc = createIncrementor(5);

inc() // 5
inc() // 6
inc() // 7
```

上面代码中，start是函数createIncrementor的内部变量。通过闭包，start的状态被保留了，每一次调用都是在上一次调用的基础上进行计算。从中可以看到，闭包inc使得函数createIncrementor的内部环境，一直存在。


闭包的另一个用处，是封装对象的私有属性和私有方法。

```
function Person(name) {
  var _age;
  function setAge(n) {
    _age = n;
  }
  function getAge() {
    return _age;
  }

  return {
    name: name,
    getAge: getAge,
    setAge: setAge
  };
}

var p1 = Person('张三');
p1.setAge(25);
p1.getAge() // 25
```

上面代码中，函数Person的内部变量_age，通过闭包getAge和setAge，变成了返回对象p1的私有变量。

#### 3.5立即调用的函数表达式（IIFE）

javascript提供了一种“创建一个匿名函数并立刻执行”的语法

```
(function(){ /* code */ }());
// 或者
(function(){ /* code */ })();
```

它的目的有两个：一是不必为函数命名，避免了污染全局变量；二是IIFE内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量。

使用IIFE常见的场景：

```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];
```

在上面的例子中，每次循环，都创建了一个新的函数，然后，把创建的3个函数都添加到一个Array中返回了。

你可能认为调用f1()，f2()和f3()结果应该是1，4，9，但实际结果是：
```
f1(); // 16
f2(); // 16
f3(); // 16
```
全部都是16！原因就在于返回的闭包引用了变量i，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量i已经变成了4，因此最终结果为16。

返回闭包时牢记的一点就是：返回函数不要引用任何循环变量，或者后续会发生变化的变量。

如果一定要引用循环变量怎么办？那就是使用立即执行匿名函数
```
(function (x) {
    return x * x;
})(3); // 9
```
更改后达到效果
```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push((function (n) {
            return function () {
                return n * n;
            }
        })(i));
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];

f1(); // 1
f2(); // 4
f3(); // 9
```
