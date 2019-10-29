---
title: "Collection体系"
date: 2019-09-25T20:07:10+08:00
draft: false
---
## Collection体系
- Collection是java中非常重要的一个接口。提供了多组实用的根接口
- Collection最重要的两个东西，是List/Set约定
 <!--more-->
- Collection体系提供的常用方法有：
- new: new ArrayList(Collection), new ArrayList() 
  - R: size()/isEmpty()/contains()/for()/stream() 
  - C/U: add()/addAll()/retainAll() 
  - D: clear()/remove()/removeAll()
  - emptySet() 返回一个方便的空集合
  - synchronizedCollection 将一个集合变成线程安全的
  - unmodifiableCollection:把一个集合变成不可变的
- 一些Collection的实现
  -  Queue/Deque
  -  LinkedList
  -  ConcurrentHashMap
  -  PriorityQueue
  -  Vector/Stack  都已经被抛弃

#### List
- 本质上是一个数组，是一个有序的集合，它拓展了Collection的一些东西，比如可以有get(int index)等方法
- 最常用的是ArrayList
-  问：List本质是一个数组，那么List怎么实现无限扩容的呢？
  -   答：动态扩容，创建一个更大的空间，然后把原来的元素拷贝过去
当旧的数组装不下时，就创建一个新的数据，容量是原来数组容量的1.5倍，再把原来数组的东西都拷贝过去

#### Set
- Set没有顺序，不允许重复的元素
  - 可以利用这个特性使用equals()判断去给List去重
- Java世界⾥里里第⼆二重要的约定：hashCode
  - 同⼀一个对象必须始终返回相同的hashCode
  - 两个对象的equals返回true，必须返回相同的hashCode
  - 两个对象不不等，也可能返回相同的hashCode
- 哈希算法
  - 哈希就是⼀一个单向的映射
  - 为什么是单向的？因为对象出现的可能性比int多得多，所以可以从int映射到对象，不能从对象映射到int
- HashSet
  - 是最常用，最高效的Set实现
  - HashSet是无序的，有需要可以用LinkedHashSet

#### Map
- Map没有继承Collection接口，Map提供key到value的映射
- 常用的方法有：
  - C/U: put()/putAll()
  - R: get()/size()  containsKey()/containsValue() keySet()/values()/entrySet() 
  - D: remove()/clear()
- HashMap
  - 最常用，最高效的Map实现
  - HashMap扩容  
    - 当原来的HashMap容量不足时，创建一个更大的HashMap,把原来的东西丢进去
  - HashMap是线程不安全的
  - Java7之后，HashMap在处理同一个哈希桶里碰撞的情况时，从链表变成了红黑树，以提高性能
- TreeSet/TreeMap
  - TreeSet是有序的  内部结构是红黑树（默认从小到大）  可以利用这个特性 进行排序
  - TreeMap的key的Set就是一个TreeSet