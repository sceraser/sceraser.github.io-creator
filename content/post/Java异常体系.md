---
title: "Java异常体系"
date: 2019-10-28T19:22:32+08:00
draft: false
---
# **Java异常体系**
异常发生的原因有很多，通常包含以下几大类：
- 用户输入了非法数据。
- 要打开的文件不存在。
- 网络通信时连接中断，或者JVM内存溢出。
<!--more-->
Java中有以下异常：
- **检查性异常(checked exception)**:最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的,此类异常在方法中throws之后，其他调用这个方法的方法也必须申明throws它。
- **非检查性异常(unchecked exception)**:在Java中为RuntimeException即**运行时异常**和它的子类，后续方法可以忽略它。
- **错误(error)**:错误不是异常，而是非常严重的问题，在代码中通常被忽略。
  
# **Exception的继承关系**

![](/image/img4.jpg)

- 所有的异常类是从 java.lang.Exception 类继承的子类。
- Exception 类是 Throwable 类的子类。除了Exception类外，Throwable还有一个子类Error 。
- 异常类有两个主要的子类：IOException 类和 RuntimeException 类。IOException通常代表“预期之内的异常”（除了Java外，其他跑在JVM的语言都抛弃了这个设计）。

# **异常处理方式**
使用try-catch来处理异常，try/catch代码块中的代码称为保护代码，使用 try/catch 的语法如下：

```
try
{
   // 程序代码
}catch(ExceptionName e1)
{
   //Catch 块
}
```
catch 语句包含要捕获异常类型的声明。当保护代码块中发生一个异常时，try 后面的 catch 块就会被检查。

如果发生的异常包含在 catch 块中，异常会被传递到该 catch 块，这和传递一个参数到方法是一样。

如果没有try，异常将直接击穿所有方法栈。

try之后可以不跟catch,可以只跟finally。

finally 只执行代码清洁工作，如把文件关闭，不要在finally里加上return，抓到了异常后一定要及时去处理。

假如try中没有发生异常，那就不会执行catch。

**try-with-resources** Java7之后，可以try(xxxx)  不用接finally，xxx是实现了AutoCloseable的类，实际上java会自动帮你接上finally，关闭xxxx对象
![](/image/img5.png)

# **多重捕获块**
一个 try 代码块后面跟随多个 catch 代码块的情况就叫多重捕获。

```
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}
```
可以在 try 语句后面添加任意数量的 catch 块。

如果保护代码中发生异常，异常被抛给第一个 catch 块。

如果抛出异常的数据类型与 ExceptionType1 匹配，它在这里就会被捕获。如果不匹配，它会被传递给第二个 catch 块。如此，直到异常被捕获或者通过所有的 catch 块。

所以异常的抛出要遵循从小到大的原则，先抛出子类的异常，再抛出父类的异常。

**Java7+** Java7中新增了语法糖，可以合并异常 ，IDE会自动提示你合并。

# **throw/throws**
- throws只是个声明，加在方法签名尾部，声明方法可能抛出一个异常，也可以实际不抛出。
- throw代表抛出一个异常，它可以是刚catch的，也可以是新实例化的。

# **异常抛出的原则**
- **能使用if-else的，不要使用try-catch**
异常创建要把栈轨迹填满，所以try-catch效率远低于if-else，且try-catch可能会意外抓住更深层的异常，导致程序出现难以发现的bug。

- **尽早抛出异常** 如果不能处理异常，应该把它抛出去。
- **异常要准确，带有详细信息**  不要用太宽泛的异常，尽肯能准确描述异常，如用FileNotFoundException而不是IOException。
- **抛出异常也比悄悄执行错误的逻辑强得多** 遇到异常不要不管不顾，最好抛出去。如图，假如result中发生了异常，catch之后只是将其打印出来，然后若无其事的return result，这种做法是错误的。
![](/image/img6.png)

# **异常的处理原则**
- **本方法是否有责任处理这个异常？**   不要处理不归自己管的异常
- **本方法是否有能力处理这个异常？**   如果自己无法处理，就抛出
- **如果不是万分必要，不要忽略异常！**     只有在特殊情况如UnsupportedEncodingException可以忽略，正常情况下获取了异常要么抛出要么处理，不要忽略异常