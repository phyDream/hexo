---
title: 面向对象中的多态
date: 2017-10-15 21:39:01
tags: [java,知识点，面向对象]
categories: [技术探索]
---
<center>多态:简而言之就是同一个行为具有多个不同表现形式或形态的能力</center>

<!-- more -->

# 概念：

我们都知道面向对象有三大特性：**封装、继承、多态**

其中封装和继承都很好理解，唯独多态理解起来可能有些抽象。

## 什么是多态：
我个人的理解是同一个行为具有不同的表现形式，比如说“移动”这一行为，不同的交通工具，比如：汽车、飞机、轮船的移动方式都是不一样的，但它们都是执行移动这一行为。


```Java
public class TrafficTool {
    public void move(){
        System.out.println("普通移动");
    }
}

public class Car extends TrafficTool {
    public void move(){
        System.out.println("行驶");
    }
}

public class Aeroplane extends TrafficTool {
    public void move(){
        System.out.println("飞行");
    }
}

public class Steamer extends TrafficTool {
    public void move(){
        System.out.println("航行");
    }
}

public class TestMove{
    public static void main(String[] args) {
        TrafficTool t = new Car();
        t.move();

        t = new Aeroplane();
        t.move();

        t = new Steamer();
        t.move();

    }
}

//结果:
//行驶
//飞行
//航行
```
在上面例子中，汽车、飞机、轮船都是作为交通工具在进行移动这一行为，但是它们各自移动的方式不同，也就是说它们同是交通工具却表现除了不同的状态。

## 多态的分类：

**重写式多态和重载式多态**

- 重载式多态：

**重载**是方法名相同而参数列表不同的一组方法就是重载，在调用这种重载的方法时，通过传入不同的参数最后得到不同的结果。根据个人理解不同，也许有人认为重载不算是多态，但从逻辑角度来说，重载满足**同一行为有不同的表现形式**这种说法，因为重载时，方法名都一样，但通过传入不同类型、不同个数的参数，我们就能得到不同的结果。

- 重写式多态：

这就是面向对象中真正意义上的多态了，它是通过**动态绑定**（dynamic binding）来实现的，也就是运行时多态。交通工具要调用移动这一方法，但我们要知道他是具体哪个交通工具才能确定怎么移动。

## 重写式多态：

**重写**涉及到面向对象特性中的**继承**，子类继承了父类中的方法才能有重写这一说法。 上面例子中说到的TrafficTool，它具有move()这一方法，它的子类们也都具有move()这一方法，并且方法名都一样，只是在父类的基础上，根据自己的特性，重新定义move()这一方法的具体实现。  

```java
        TrafficTool t = new Car();
        t.move();

        t = new Aeroplane();
        t.move();

        t = new Steamer();
        t.move();

//结果:
//行驶
//飞行
//航行
```

最后我们用相同的引用，调用了三次相同的方法，结果却不同。  

区别就在于这三个引用指向的对象本质上是不同的，汽车是汽车，飞机是飞机，不过我们把他们都当作交通工具而已，像这样把父类当做子类来用，就是所谓的**向上转型**。  

就比如我说我要从成都出发去上海，我说出这句话时，你根本不知道我通过什么交通工具去，但我出发的时候肯定只能选一种交通工具，其实我之前已经订好票坐飞机去，所以我出发的时候，调用的是飞机实现的move()方法。 

向上转型意义在于我们需要大量调用父类的共有方法时，不用管具体是哪个子类调用该方法，当执行到这一方法时，它自己就会调用对应子类的实现。

例子：

模拟加油站给来往车辆加油：


```java
public class Truck {
   public void refueling(){
        System.out.println("加柴油");
    }
}

public class Car {
   public void refueling(){
        System.out.println("加柴油");
    }
}

public class Benz {
   public void refueling(){
        System.out.println("加更好的汽油");
    }
}

public class GasStation {
    public void refueling(Truck t){
        t.refueling();
    }
    
    public void refueling(Car c){
        t.refueling();
    }
    
    public void refueling(Benz bc){
        t.refueling();
    }
}

public class TestRefueling{
    public static void main(String[] args) {
        GasStation g = new GasStation();
        g.refueling(new Truck());
        g.refueling(new Car());
        g.refueling(new Benz());
    }
}
```
好像看着没什么毛病，但如果车的类型更多了呢，拖拉机、货车、客车、摩托车，那样的话GasStation中会为每一种车都写一个refueling方法。明明方法名都一样，方法内容也是一样，这样是不是太麻烦了，我们这是就可以利用**向上转型**了，实现车的**多态**。



```java
//定义所有车的父类
public class AllCar {
   public void refueling(){
        System.out.println("");
    }
}


public class Truck extend AllCar{
   public void refueling(){
        System.out.println("加柴油");
    }
}

public class Car extend AllCar{
   public void refueling(){
        System.out.println("加柴油");
    }
}

public class Benz extend AllCar{
   public void refueling(){
        System.out.println("加更好的汽油");
    }
}
```

这时加油站中就只用写一个方法了


```
public class GasStation {
    public void refueling(AllCar a){
        a.refueling();
    }
}

public class TestRefueling{
    public static void main(String[] args) {
        GasStation g = new GasStation();
        g.refueling(new Truck());
        g.refueling(new Car());
        g.refueling(new Benz());
    }
}
```

# 经典案例:


求Demo中输出结果：

```java
class A {
    //方法1
    public String show(D obj) {
        return ("A and D");
    }
    //方法2
    public String show(A obj) {
        return ("A and A");
    }

}

class B extends A{
    //方法3
    public String show(B obj){
        return ("B and B");
    }
    //方法4
    public String show(A obj){
        return ("B and A");
    }
}

class C extends B{

}

class D extends B{

}

public class Demo {
    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new B();
        B b = new B();
        C c = new C();
        D d = new D();

        System.out.println("1--" + a1.show(b));
        System.out.println("2--" + a1.show(c));
        System.out.println("3--" + a1.show(d));
        System.out.println("4--" + a2.show(b));
        System.out.println("5--" + a2.show(c));
        System.out.println("6--" + a2.show(d));
        System.out.println("7--" + b.show(b));
        System.out.println("8--" + b.show(c));
        System.out.println("9--" + b.show(d));
    }
}

//结果：
//1--A and A
//2--A and A
//3--A and D
//4--B and A
//5--B and A
//6--A and D
//7--B and B
//8--B and B
//9--A and D
```

## 解析：
- a1.show(b):  
a1 对象本质是实例化的A，也就是说他本身就是A。
那自然就是调用的A中的方法，A中有两个方法，参数分别是A和D的对象，这里传入的是B，他是A的子类所以能向上转型成A，满足条件，所以调用的是方法1

- a1.show(c): 理由同上调用的是方法1

- a1.show(d):  
方法中传入的参数是D的对象，所以自然调用的是方法2


 在作下面的解释前，我们需要先了解A和B中的方法： 
 
 
1.  A作为父类有自己的方法和子类重写自父类的方法。

```java
//自有
    public String show(D obj) {
        return ("A and D");
     }
     //被B重写的方法
     public String show(A obj) {
         return ("A and A");
     }
```

1.  B作为A的子类，不仅有自己的方法，还有继承自A的方法和重写自A的方法。

```java
//隐式的继承自A
     public String show(D obj) {
         return ("A and D");
    }
     //自有（非继承和重写）,父类不能调用
     public String show(B obj){
         return ("B and B");
     }
     //重写的方法
     public String show(A obj){
         return ("B and A");
     }
```


- a2.show(b):  
a2 是A的引用，但他是实例化的B向上转型得来的，所以这里传入b会先在B类中找方法，刚好找到方法show(B obj),但是a2是A的引用，不能调用B的自有方法，所以只能找到方法4
，方法4是重写的A中方法，可以被A的引用a2调用,刚好这里传入的对象b是A的子类可以向上转型，满足条件，所以调用的是方法4。


- a2.show(c): 
a2 是A的引用，但他是实例化的B向上转型得来的，所以这里传入c会先在B类中找方法，找到方法show(B obj),但是a2是A的引用，不能调用B的自有方法，所以只能找到方法4
，方法4是重写的A中方法，可以被A的引用a2调用,刚好这里传入的对象c是A的孙子类可以向上转型，满足条件，所以调用的是方法4。

- a2.show(d):  
a2 是A的引用，但他是实例化的B向上转型得来的，所以这里传入d会先在B类中找方法，B类中刚好存在隐式继承自A的方法show(D obj)满足条件，所以调用的方法1。

- b.show(b):  
b 是B的引用，也是实例化的B，所以这里传入b直接在B类中找方法，方法3正好需要的是B,而且没有被子类重写，满足条件，所以调用的是方法3。

- b.show(c): 
b 是B的引用，也是实例化的B，他有继承自A中的两个父类方法，也有B中自有两个方法，其中方法4是重写的A中方法2，所以这里传入c直接在B类中找方法，方法3需要的是B,C是B的子类，可以向上转型成B,且方法3没有被子类重写，满足条件，所以还是调用的方法3。

- b.show(d):  

b 是B的引用，也是实例化的B，所以这里传入d直接在B类中找方法，B类中刚好存在隐式继承自A的方法show(D obj)满足条件，所以调用的方法1。

## 总结： 

继承链中对象方法的调用的优先级：this.show(O)、super.show(O)、this.show((super)O)、super.show((super)O)。
