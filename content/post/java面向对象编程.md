---
title: Java面向对象编程
date: 2018-10-01 
tags:
---
### Java面向对象编程
#### 前言
Java语言提供类、接口和继承等面向对象的特性，为了简单起见，只支持类之间的单继承，但支持接口之间的多继承，并支持类与接口之间的实现机制（关键字为implements）。Java语言全面支持动态绑定，而C++语言只对虚函数使用动态绑定。总之，Java语言是一个纯的面向对象程序设计语言。
<!--more-->
#### 继承
继承是java面向对象的基石,它允许创建不同级别的类继承就是子类继承父类的行为和特征,使得子类拥有父类的构造方法
- 子类和父类符合is-a的关系,子类是一个父类,只是它的行为更丰富了
![](https://i.loli.net/2019/05/01/5cc961face310.jpg)
- 子类可以拥有父类非private的属性和方法
- 子类可以拥有自己的属性和方法,即子类可以对父类进行拓展
- ***子类构造方法必须且只能实现父类一个构造方法,当父类存在没有参数的构造方法时,可以不写来代表用super()调用了它,当父类不存在没有参数的构造方法时,必须super(参数)一个父类构造方法且必须放在子类构造方法语句开头***
- this 和 super 不能同时出现在一个构造函数里面，因为this必然会调用其它的构造函数，其它的构造函数必然也会有 super 语句的存在，所以在同一个构造函数里面有相同的语句，就失去了语句的意义，编译器也不会通过。
- 子类可以用自己的方式实现父类的方法(override)
- 在申明子类的时候,通过关键词"extends"表达继承
```
class 父类{
}
class 子类 extends 父类 {
}
```
- java不支持多继承.但支持多重继承
![](https://i.loli.net/2019/05/01/5cc95fbaa6985.png)
- 修饰符final
  - final<类> ->防止类被继承
  - final<方法> ->防止方法被重载(override)
  - final<变量> ->防止变量被修改引用到另一个对象,可称为"常量"
#### 封装
在面向对象程式设计方法中，封装（英语：Encapsulation）是指一种将抽象性函式接口的实现细节部份包装、隐藏起来的方法。
- 封装--类和外部的关系
继承--类和下一级类的关系
- 封装把代码分成两部分：接口和实现。接口应该保持稳定，例如：API和库。对外暴露的越少越
- 封装通过类来实现，所以为什么成员变量要用private去修饰，因为这样就不会被跨类调用对类内部状态的访问进行控制，只提供该提供的信息。
```
public class Person {
    private String name;
    private int age;
    
    public int getAge(){
      return age;
    }
    
    public String getName(){
      return name;
    }
    
    public void setAge(int age){
      this.age = age;
    }
    
    public void setName(String name0{
      this.name = name;
    }
}
```
#### 多态
多态是同一个行为具有多个不同表现形式或形态的能力。多态就是同一个接口，使用不同的实例而执行不同操作，如图所示：
![](https://i.loli.net/2019/05/01/5cc99fb179674.png)
- 多态基本只在静态语言中出现
- **多态的优点**
  - 1. 消除类型之间的耦合关系
  - 2. 可替换性
  - 3. 可扩充性
  - 4. 接口性
  - 5. 灵活性
  - 6. 简化性
- **多态存在必须的条件**
  - 继承
  - 重写
  - 父类引用指向子类对象(java转型)
比如:
```
Father f = new Son();  //Son extends Father
```
当使用多态调用方法时,首先检查父类是否有该方法,没有就编译错误;如果有,就调用子类同名的方法。
```
public class Test {
    public static void main(String[] args) {
        show(new Cat());  // 以 Cat 对象调用 show 方法
        show(new Dog());  // 以 Dog 对象调用 show 方法

        Animal a = new Cat();  // 向上转型  
        a.eat();               // 调用的是 Cat 的 eat
        Cat c = (Cat)a;        // 向下转型  
        c.work();        // 调用的是 Cat 的 work
    }

    public static void show(Animal a)  {
        a.eat();
        // 类型判断
        if (a instanceof Cat)  {  // 猫做的事情 
            Cat c = (Cat)a;
            c.work();
        } else if (a instanceof Dog) { // 狗做的事情 
            Dog c = (Dog)a;
            c.work();
        }
    }
}

abstract class Animal {
    abstract void eat();
}

class Cat extends Animal {
    public void eat() {
        System.out.println("吃鱼");
    }
    public void work() {
        System.out.println("抓老鼠");
    }
}

class Dog extends Animal {
    public void eat() {
        System.out.println("吃骨头");
    }
    public void work() {
        System.out.println("看家");
    }
}
```
执行以上程序，输出结果为：
```
吃鱼
抓老鼠
吃骨头
看家
吃鱼
抓老鼠
```
- 抽象类和接口的区别
  -  抽象类中的方法可以有方法体，就是能实现方法的具体功能，但是接口中的方法不行。
  -  抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是 public static final 类型的。
  -  接口中不能含有静态代码块以及静态方法(用 static 修饰的方法)，而抽象类是可以有静态代码块和静态方法。
  -  一个类只能继承一个抽象类，而一个类却可以实现多个接口。













  
