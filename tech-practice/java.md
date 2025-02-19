# Java最佳实践

用自己话讲一遍知识，用自己的知识形成最佳实践

## 基础（特性、数据类型、反射、序列化、枚举、注解、泛型、拆装箱、数值处理等）

- 面向过程是过程化的编程思想，面相对象是让代码更接近现实世界，将事物抽象成对象，关注对象之间的交互，更易于理解和扩展

- 封装，对内保护实现易于维护，对外只需关注交互

- 继承，模仿现实迭代，提供代码复用和层次结构

- 多态，代码灵活与扩展

- 重载，同一个类中，方法名字相同，参数列表不同

- 重写，子类或者父类，方法名字相同，参数列表相同

- java多态，同样的操作 作用于不同的对象，有不同的解释或执行结果

- java运行时多态，重写；继承可以重写，实现必须重写

- java编译时多态，重载

- java高扩展，主要由两种途径，实现与继承（猜测，这也是jdk动态代理走实现，字节码走继承，两条路子 同样的设计理念）

- 同样可行情况下，优先组合（松耦合），而不是继承（强耦合）

- 不支持多继承，因为徒增复杂，且会有菱形继承问题

- java bean，不要写isSuccess，而要写success，首先对应的 getSuccess()更契合规范 getXxx()，其次很多IDE会将isSuccess自动生成isSuccess()方法而不是 getIsSuccess()，序列化的时候就会对应不上出问题了

- equals()底层默认就是==，只要引用指向同一个对象，就是相等

- hashcode()

- equals()和hashcode()相辅相成，两个对象相等的严格定义是 对象内容equals()相等 并且 哈希值hashcode()也要相等

- 对于散列集合（hashmap、hashset、hashtable）重写前者务必重写后者，否则无法按照预期工作；比如hashmap可能会导致相等的对象有不同的hashcode

  ```
  class Person {
      String name;
      int age;
  
      @Override
      public boolean equals(Object obj) {
          // 比较name和age是否相等
      }
      // 未重写hashCode
  }
  
  Person p1 = new Person("Alice", 30);
  Person p2 = new Person("Alice", 30);
  
  // 假设p1.equals(p2)为true，但p1.hashCode() != p2.hashCode()
  Set<Person> set = new HashSet<>();
  set.add(p1);
  set.contains(p2); // 返回false，因为哈希码不同，无法命中桶
  ```
  
- 浅拷贝，clone

- 深拷贝，序列化

- 值传递，

- 引用传递

- java平台无关性，源代码->前端编译->.class中间码->后端编译->机器语言；三个重要支撑，java语言规范，class文件，jvm虚拟机

- 对Integer.MIN_VALUE进行 abs会越界，所以先转long，再abs，降低概率

- 集合容器要求元素必须是Object，所以需要包装类

- 自动装箱：Integer a = 10；原理是 Integer a = Integer.valuesOf(10)；其他一样的 xxx.valueOf()

- 自动拆箱：int b = a；原理是 int b = a.intValue；其他一样的 .XxxValue()

- 自动拆装箱场景：基本类型放入集合、基本与包装类比较、包装类运算、三目运算符、函数返回与返回值

- 部分包装类是有缓存的（float和double范围太大且精度复杂无法高效缓存），可以避免频繁创建和销毁小范围对象，节省内存；Integer的范围可以通过jvm参数修改；自动拆装箱会有npe问题，如果在for循环中会浪费大量资源

  ```
  Integer a = 127;
  Integer b = 127;
  System.out.println(a == b);  // true（缓存范围内，对象复用）
  
  Integer c = 128;
  Integer d = 128;
  System.out.println(c == d);  // false（超出缓存范围，新建对象）
  
  Float f1 = 1.0f;
  Float f2 = 1.0f;
  System.out.println(f1 == f2);  // false（Float无缓存，每次新建对象）
  ```

  

- POJO中、RPC使用包装类，因为包装出错是null，null就是null；基本类型会是默认值具有二义性

## 异常

## 时间处理

## 语法糖

## 新版本特性

## jvm

## 集合

## io

## 并发编程

- jmm，（是什么）定义了java线程如何在共享内存中交互的规范；（如何实现）主内存与工作内存交互机制；同步策略（有啥用）并发编程三大问题：线程安全、性能、资源分配，jmm就是建立了一套内存交互规范以及
- jmm实现内存可见性与原子性、volatile保证变量可见性和禁止指令重排、sync提供互斥和可见性
- sync 作用于两种，方法，和方法块；锁的是对象；非静态锁当前实例对象，静态锁类对象
- 线程安全，并发、多线程、共享变量、正确完成
- 
