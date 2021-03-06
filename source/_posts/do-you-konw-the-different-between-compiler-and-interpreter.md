---
title: 你知道「编译」与「解释」的区别吗？
date: 2016-11-20 00:03:00
tags:
- 编译
- 解释
category: 搬砖码农
---

最近在看一些编译过程的知识点，看的比较多的是英文文献。
在这之间经常遇到的两个单词让我着实迷惑：Compiler, Interpreter
中文翻译分别是：编译器，解释器。

如果有人问我们「你知道什么是编译器么？」，
我们很有可能首先蔑视一下这个人，然后说：「知道啊，不就编译编程语言的程序嘛！」
要是别人再追问一句「那你知道解释器么？」，
这时候很有可能也会说「知道啊。」，但是很难再带有蔑视的语气了。
要是再问一句「那么编译器和解释器的区别是什么啊？」，
「呃......」

那么到底什么是「编译器」，什么是「解释器」？
虽然对于两个词，我们很「耳熟」，但是「能详」么？
似乎我们并没有认真对待这两个词汇。

# 什么是编译器
摘自 [Wiki Compiler](https://www.wikiwand.com/en/Compiler) 一段
>A compiler is a computer program (or a set of programs) that transforms source code written in a programming language (the source language) into another computer language (the target language), with the latter often having a binary form known as object code. The most common reason for converting source code is to create an executable program.

大概意思：
> 编译器是一种计算机程序，负责把一种编程语言编写的源码转换成另外一种计算机代码，后者往往是以二进制的形式被称为目标代码(object code)。这个转换的过程通常的目的是生成可执行的程序。

编译器的产出是「另外一种代码」，然后这些代码等着被别人拿来执行，如果还不能直接被执行，那么还需要再编译或解释一遍，再交由计算机硬件执行。
编译器，往往是在「执行」之前完成，产出是一种可执行或需要再编译或者解释的「代码」。

# 什么是解释器
摘自 [Wiki Interpreter](#) 一段
> In computer science, an interpreter is a computer program that directly executes, i.e. performs, instructions written in a programming or scripting language, without previously compiling them into a machine language program. An interpreter generally uses one of the following strategies for program execution:
1. parse the source code and perform its behavior directly.
2. translate source code into some efficient intermediate representation and immediately execute this.
3. explicitly execute stored precompiled code made by a compiler which is part of the interpreter system.

大概意思：
> 在计算机科学中，解释器是一种计算机程序，它直接执行由编程语言或脚本语言编写的代码，并不会把源代码**预编译**成机器码。一个解释器，通常会用以下的姿势来执行程序代码：
1. 分析源代码，并且直接执行。
2. 把源代码翻译成相对更加高效率的中间码，然后立即执行它。
3. 执行由解释器内部的编译器预编译后保存的代码

可以把解释器看成一个黑盒子，我们输入源码，它就会实时返回结果。
不同类型的解释器，黑盒子里面的构造不一样，有些还会集成编译器，缓存编译结果，用来提高执行效率（例如 Chrome V8 也是这么做的）。
解释器通常是工作在「运行时」，并且对于我们输入的源码，是一行一行的解释然后执行，然后返回结果。

# 分两个维度比较一下

## 表现 Behavior 
* **编译器**把源代码转换成其他的更低级的代码(例如二进制码、机器码)，但是不会执行它。
* **解释器**会读取源代码，并且直接生成指令让计算机硬件执行，不会输出另外一种代码。
  
## 性能 Performance
* **编译器**会事先用比较多的时间把整个程序的源代码编译成另外一种代码，后者往往较前者更加接近机器码，所以执行的效率会更加高。时间是消耗在预编译的过程中。
* **解释器**会一行一行的读取源代码，解释，然后立即执行。这中间往往使用相对简单的词法分析、语法分析，压缩解释的时间，最后生成机器码，交由硬件执行。解释器适合比较低级的语言。但是相对于预编译好的代码，效率往往会更低。如何减少解释的次数和复杂性，是提高解释器效率的难题。

# 关于代码，需要知道的几个概念

在看了不少不多关于「编译和解释」的文章之后，我发现下面的词汇是大量出现的。
知道这些词汇代表的意思，以及对应的层次，能够更好地看懂别人所要表达的意思。

## 高级语言代码 High-Level Code
高级语言代码，自然是指由高级编程语言编写代码，对计算机的细节有更高层次的抽象。
相对于低级编程语言（low-level programming language）更接近自然语言（人类的语言）。
集成一系列的自动工具（垃圾回收，内存管理等），会让程序员延长寿命，更快乐的编写出更简洁，更易读的程序代码。

## 低级语言代码 Low-Level Code 
低级语言代码，指由低级编程语言编写的代码，相对高级语言，少了更多的抽象概念，更加接近于汇编或者机器指令。
但是这也意味着代码的可移植性很差。

在我看来，高与低，只是一组相对词而已。
越高级的语言，性能、自由度越不及低级语言。
但是在抽象、可读可写性、可移植性越比低级语言优秀。
在以前的年代，C/C++语言相对汇编语言，机器指令来说，肯定是高级语言。
而到了今天，我们更多人对C语言偏向认知为「低级语言」。
或许未来世界的开发者，看我们现在所熟悉的Java、PHP、Python、ECMAScript等等，都是「low」到爆的语言。

## 汇编语言 Assembly Language
汇编语言作为一门低级语言，对应于计算机或者其他可编程的硬件。
它和计算机的体系结构以及机器指令是强关联的。
换句话说，就是不同的汇编语言代码对应特定的硬件，所以不用谈可移植性了。
相对于需要编译和解释的高级语言代码来说，汇编代码只需要翻译成机器码就可以执行了。
所以汇编语言也往往被称作象征性机器码(symbolic machine code)

## 字节码 Byte Code 
字节码严格来说不算是编程语言，而是高级编程语言为了种种需求（可移植性、可传输性、预编译等）而产生的中间码（Intermediate Code）。
它是由一堆指令集组成的代码，例如在`javac`编译过后的java源码产生的就是字节码。
源码在编译的过程中，是需要进行「词法分析 → 语法分析 → 生成目标代码」等过程的，在预编译的过程中，就完成这部分工作，生成字节码。
然后在后面交由解释器（这里通常指编程语言的虚拟机）解释执行，省去前面预编译的开销。

## 机器码 Machine Code
机器码是一组可以直接被CPU执行的指令集，
每一条指令都代表一个特定的任务，或者是加载，或者是跳转，亦或是计算操作等等。
所有可以直接被CPU执行的程序，都是由这么一系列的指令组成的。
机器码可是看作是编译过程中，最低级的代码，因外再往下就是交由硬件来执行了。
当然机器码也是可以被编辑的，但是以人类难以看懂的姿势存在，可读性非常差。

# 从熟悉的编程语言的角度来看看

![从熟悉的编程语言的角度来看](/image/blog/do-you-konw-the-different-between-compiler-and-interpreter/5698B76C4AAAE21598E7AB1A381B4AF9.gif)

从左往右看，
1. 以 Java 为例，我们在文本编译器写好了 Java 代码，交由「编译器」编译成 Java Bytecode。然后 Bytecode 交由 JVM 来执行，这时候 JVM 充当了「解释器」的角色，在解释 Bytecode 成 Machine Code 的同时执行它，返回结果。
2. 以 [BASIC](https://www.wikiwand.com/zh/BASIC) 语言（早期的可以由计算机直译的语言） 为例，通过文本编译器编写好，不用经历「编译」的过程，就可以直接交由操作系统内部来进行「解释」然后执行。
3. 以 C 语言为例，我们在文本编译器编写好源代码，然后运行 `gcc hello.c` 编译出 `hello.out` 文件，该文件由一系列的机器指令组成的机器码，可以直接交由硬件来执行。

# 抽象看本质：人与计算机之间的鸿沟
无论是最近在看《暗时间》的作者刘未鹏，还是前一段时间听《以产品思维写文章》讲座的阿禅，还是其他的很多聪明的人。
他们都强调「抽象看本质」的能力，能从事物本身抽象出共通属性，看待本质。
这也是很多人所说的「跳出这个框框再看」的思维方式。

无论是「编译 Compile」还是「解释 Interpret」。
本质还是**「人与计算机的交流形式」**，人的语言最终转换成机器语言。
一句 「Hello World」，经过一些列的「编译」和「解释」，最终转换成一系列包含机器指令的那些0和1，机器傻傻执行完之后，告诉你结果。

就这么一个过程，我们就需要很多的翻译官。
有些翻译官可以做到同声传译（解释），有些翻译官却只能把我们的意图记下来再全部翻译（编译）给计算机。
而往往一个翻译官能力有限，也只能把你的语言，翻译成另外一种低级点的语言，再由另外懂这个语言的翻译官来翻译更接近计算机能读得懂的语言。

![人类和计算机的鸿沟.png](/image/blog/do-you-konw-the-different-between-compiler-and-interpreter//B531CE953267440FAA32A1DA644BFD68.png)

# 一句话描述「编译」与「解释」？
不如这张图来得直接：

![一句话描述编译与解释](/image/blog/do-you-konw-the-different-between-compiler-and-interpreter//B415AA74BF5438CCEB2FEAEDD002B1BD.jpg)

**编译 Compile**：把整个程序源代码翻译成另外一种代码，然后等待被执行，发生在运行之前，产物是「另一份代码」。
**解释 Interpret**：把程序源代码一行一行的读懂然后执行，发生在运行时，产物是「运行结果」。

# 参考
http://stackoverflow.com/questions/2377273/how-does-an-interpreter-compiler-work
https://www.wikiwand.com/en/Interpreter_(computing)
https://www.wikiwand.com/en/Compiler
https://www.wikiwand.com/en/Machine_code
https://www.wikiwand.com/en/High-level_programming_language
https://www.wikiwand.com/en/Low-level_programming_language
https://www.wikiwand.com/en/Bytecode

