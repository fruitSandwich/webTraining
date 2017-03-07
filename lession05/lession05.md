# javascript面向对象与函数式

前面我们说到JavaScript的“编程风格”是函数式编程和面向对象编程的一种混合体。再说函数式和面向对象之前，我们先来探讨一下编程风格是怎么回事，以及都有哪些常见的“编程风格”

## 1.编程范式

范式（paradigm）的概念和理论是美国著名科学哲学家托马斯·库恩(Thomas,Kuhn) 提出并在《科学革命的结构》(The Structure of Scientific Revolutions)（1962）中系统阐述的，它指的是一个共同体成员所共享的信仰、价值、技术等等的集合。指常规科学所赖以运作的理论基础和实践规范，是从事某一科学的研究者群体所共同遵从的世界观和行为方式。

本节节选总结自<a href='http://www.cnblogs.com/xyz98/archive/2009/03/20/1417919.html'>冒号课堂--编程范式与OOP思想</a>

## 1.1编程语言的世界观与方法论

编程范式是计算机编程中的基本风格和典范模式，是编程者在其所创造的虚拟世界中自觉不自觉采用的世界观和方法论。每种范式都引导人们带着其特有的倾向和思路去分析和解决问题。面向对象(OOP)就是一种编程范式。

如果把一门编程语言比作武功，它的语法、工具和技巧等是招法，它采用的编程范式则是心法。

抽象的编程范式需要通过具体的编程语言来体现。范式的世界观体现在语言的核心概念之中，范式的方法论体现在语言的表达机制中。一种语言的语法和风格与其所支持的编程范式密切相关。

## 1.2编程范式与设计模式的区别
设计模式（Design pattern）是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。设计模式是遵循设计原则的一些具体技巧，以保证代码的灵活性、扩展性和可重用性为目的。它重在设计，对编程语言一般没有要求。

编程范式则不同，对编程语言往往有专门的要求。通常所说的某某范式的语言，即指该语言对该范式在语法上有明确充分的支持，不需要借助其他的范式或工具。事实上，语言本来就是围绕其所倡导的核心范式来设计的。

设计模式好比几种功夫的巧妙组合（比如开闭原则、接口隔离、依赖倒转等等），能在一些特定场合下克敌制胜。编程范式则好比武功门派，博大精深且自成体系(范式互相之间天壤之别)。


## 2.几种常见的编程范式

### 2.1命令式/过程式
- 核心概念：命令/过程
- 关键突破：突破单一主程序和非结构化程序的限制
- 主要目的：模拟机器思维，实现自顶向下的模块设计
- 代表语言：Fortran/Pascal/C
- 运行机制：命令执行
- 实现原理：引入逻辑控制和子程序
- 常见应用：交互式、事件驱动型系统；数值计算等

### 2.2函数式/应用式
- 核心概念：函数
- 关键突破：突破机器思维的限制
- 主要目的：模拟数学思维，简化代码，减少副作用
- 代表语言：Scheme/Haskell
- 运行机制：表达式计算
- 实现原理：引入高阶函数，将函数作为数据处理
- 常见应用：微积分计算；数学逻辑；博弈等

### 2.3逻辑式
- 核心概念：断言
- 关键突破：突破逻辑与控制粘合的限制
- 主要目的：专注逻辑分析，减少控制代码
- 代表语言：Prolog/Mercury
- 运行机制：逻辑推理
- 实现原理：利用推理引擎在已知的事实和规则的基础上进行逻辑推断
- 常见应用：机器证明；专家系统；自然语言处理；语义网（semantic web）；决策分析；业务规则管理等

### 2.4对象式
- 核心概念：对象
- 关键突破：突破数据与代码分离的限制
- 主要目的：迎合人类认知模式，提高软件的易用性、重用性和可维护性
- 代表语言：Smalltalk/Java
- 运行机制：对象间信息交换
- 实现原理：引入封装、继承和多态机制
- 常见应用：大型复杂交互式系统等

### 2.5并发式/并行式
- 核心概念：进程/线程
- 关键突破：突破串行的限制
- 主要目的：充分利用资源、提高运行效率、提高软件的响应能力、保证公平竞争
- 代表语言：Erlang/Oz
- 运行机制：进程/线程间通讯与同步
- 实现原理：引入并行的线程模块以及模块间的通讯与同步机制
- 常见应用：图形用户界面；I/O处理；多任务系统如操作系统、网络服务器等；实时系统；嵌入式系统；计算密集型系统如科学计算、人工智能等

### 2.6泛型式
- 核心概念：算法
- 关键突破：突破静态类型语言的限制
- 主要目的：提高算法的普适性
- 代表语言：Ada/Eiffel/C++
- 运行机制：算法实例化
- 实现原理：利用模板推迟类型指定
- 常见应用：普适性算法如排序、搜索等；集合类容器等

### 2.7元编程
- 核心概念：元程序
- 关键突破：突破语言的常规语法限制
- 主要目的：减少手工编码，提升语言级别
- 代表语言：Lisp/Ruby/JavaScript
- 运行机制：动态生成代码或自动修改执行指令
- 实现原理：利用代码生成或语言内建的反射（reflection）、动态等机制，将程序语言作为数据来处理
- 常见应用：自动代码生成；定义结构化配置文件；IDE；编译器；解释器；人工智能；模型驱动架构（MDA）；领域特定语言（DSL）等

### 2.8切面式
- 核心概念：切面
- 关键突破：突破横切关注点无法模块化的限制
- 主要目的：实现横切关注点分离
- 代表语言：AspectJ/AspectC++
- 运行机制：在接入点处执行建议
- 实现原理：通过编织（weaving）将附加行为嵌入主体程序
- 常见应用：日志输出；代码跟踪；性能监控；异常处理；安全检查；事务管理等

### 2.9事件驱动
- 核心概念：事件
- 关键突破：突破顺序、同步的流程限制
- 主要目的：调用者与被调用者在代码和时间上双重解耦
- 代表语言：C#/VB.NET
- 运行机制：监听器收到事件通知后做出响应
- 实现原理：引入控制反转和异步机制
- 常见应用：图形用户界面；网络应用；服务器；操作系统；IoC框架；异步输入；DOM等

## 3.设计模式中的面向对象与函数式

> 某些设计模式是一种涉及到的是函数和对象的转换，这种转换往往不是有必要的，仅仅是把一些函数式编程的概念强行转换成面向对象风格。所以这就带来更多的代码，更低的可读性而且维护起来更困难。实际上，这不仅仅是用对象把函数包装起来那么简单，你还必须得把这些松散的对象“粘起来”。相同的结果，如果用函数式编程实现更加简单。——https://www.voxxed.com/blog/2016/04/gang-four-patterns-functional-light-part-1/

### 3.1策略（Strategy）模式
有一个场景，一个处理文本的过程：输入，筛选，最后把结果转换并输出。换句话说需要两个行为：过滤文本，转换格式。如果过滤文本和转换格式的算法需要独立于客户的变化又可以互相替换，那么可以用策略模式。

>策略模式：定义一系列的算法,把每一个算法封装起来, 并且使它们可相互替换。本模式使得算法可独立于使用它的客户而变化。

使用面向对象范式：
1. 定义一个接口，定义两个行为过滤文本和转换格式

  ```
  interface TextFormatter {
     boolean filter(String text);
     String format(String text);
  }
  ```

2. 封装场景，封装用户怎样过滤和格式化文本

  ```
  public class TextEditor {
      private final TextFormatter textFormatter;
      public TextEditor(TextFormatter textFormatter) {
          this.textFormatter = textFormatter;
      }
      public void publishText(String text) {
          if (textFormatter.filter( text )) {
             System.out.println( textFormatter.format( text ) );
          }
      }
  }
  ```

3. 新增接口实现

  ```
  //实现一，接受任何文本，原样输出
  public class PlainTextFormatter implements TextFormatter {
      @Override
      public boolean filter( String text ) {
         return true;
      }    
      @Override
      public String format( String text ) {        
         return text;
      }
  }

  //实现二，处理日志中的"ERROR"，如果发现”ERROR”就把文本转换成大写
  public class ErrorTextFormatter implements TextFormatter {    @Override
      public boolean filter( String text ) {        
         return text.startsWith( "ERROR" );
      }
      @Override
      public String format( String text ) {        
         return text.toUpperCase();
      }
  }

  //实现三，小于20个字符的文本变成小写
  public class ShortTextFormatter implements TextFormatter {
      @Override
      public boolean filter( String text ) {       
         return text.length() < 20;
      }    
      @Override
      public String format( String text ) {       
         return text.toLowerCase();
      }
  }
  ```

4. 使用整套模式
  ```
  TextEditor textEditor = new TextEditor( new PlainTextFormatter() );
  textEditor.publishText( "ERROR - something bad happened" );
  textEditor.publishText( "DEBUG - I'm here" );

  TextEditor errorEditor = new TextEditor( new ErrorTextFormatter() );
  errorEditor.publishText( "ERROR - something bad happened" );
  errorEditor.publishText( "DEBUG - I'm here" );
  ```

策略模式将策略或算法封装到类通过传递不同类的实例达到动态调用不同算法的目的。使用函数式范式直接传递实现算法的函数会更加简洁：

1. 定义使用场景

  ```
  function publishText(text, filter, format) {
    if (filter(text)) {
      console.log(format(text))
    }
  }
  ```
2. 封装过滤文本和转换函数

  ```
  const textUtil = {
    acceptAll: s => true,
    noFormatting: s => s,
    acceptError: s => s.startsWith('ERROR'),
    formatError: s => s.toUpperCase()
  }
  ```

3. 使用模式

  ```
  publishText("DEBUG - I'm here", textUtil.acceptAll, textUtil.noFormatting);

  publishText("ERROR - something bad happened", textUtil.acceptError, textUtil.formatError);
  ```
