---
title: 抽象类和接口
date: 2017-10-13 21:39:01
tags: [java,知识点]
categories: [技术探索]
---
<center>抽象类是对事物的抽象,接口是对行为的规范。</center>

<!-- more -->


# 实例：

交通工具：汽车、飞机、船

```java
public  class Car {

}

public  class Aeroplane {

}

public  class Ship {

}
```


## 抽象类：

所有的交通工具都有一些共性，我们如果为每个交通工具设置相同的属性和行为就显得太麻烦，这时我们需要定义一个抽象类“交通工具”提取出各交通工具的共有属性与行为。

属性：品牌、型号、开始服役日期

行为：补充燃料


```java
public abstract class TrafficTools {
    public String brands;
    public String number;
    public int serviceDate;
    
    //补充燃料
    abstract void refuel();
}
```

上面refuel()这个方法是抽象方法,在抽象类中不做实现，因为不同交通工具补充燃料的方式五花八门，所以由继承的子类具体实现该方法

这时我们定义“汽车”就很方便了，用“汽车”继承“交通工具”它就直接拥有交通工具的基本属性和行为了


```java
public  class Car extends TrafficTools{
    //补充燃料
    public void refuel(){
        //加油...
    };
}
```

## 接口：

不同的交通工具的行为方式是有区别的，汽车是行驶，飞机是飞行、船是航行。

我们以飞机为例，正常飞行过程需要三个步骤：  

1. 起飞
2. 飞行
3. 降落

带有飞行功能的飞机如下：
```java
public  class Aeroplane extends TrafficTools{
    //补充燃料
    public void refuel(){
    };
    
    //起飞
    public void takeOff(){
    };
    
    //飞行
    public void flight(){
    };
    
    //降落
    public void landing(){
    };
}
```

然后我们再来一个交通工具“热气球”，它依然具有飞行功能，而且飞行过程和“飞机”一样，这时我们就需要统一一下飞行这个功能了，毕竟同样的飞行功能，我们不能乱写，方法名要统一，takeOff()不能随便变成take_off()或takeoff()。所以我们就定义一个接口来规范飞行这个功能.

```java
public  interface Fly {
    
    //起飞
    public void takeOff();
    
    //飞行
    public void flight();
    
    //降落
    public void landing();
}
```

实现飞行接口的类，飞行的方法都是整齐划一的了。 
 
 
热气球如下：

```java
public  class HotAirBalloon extends TrafficTools implements Fly{
    //补充燃料
    public void refuel(){
    };
    
    //起飞
    public void takeOff(){
    };
    
    //飞行
    public void flight(){
    };
    
    //降落
    public void landing(){
    };
}
```
如果我们再给“飞机”、“热气球”加上投弹功能，再定义一个接口投弹：
```java
public  interface Bomb {
    
    //装填
    public void loading();
    
    //投放
    public void PutOn();
    
}
```

同时实现飞行和投弹功能的“热气球：

```java
public  class HotAirBalloon extends TrafficTools implements Fly,Bomb{
    //补充燃料
    public void refuel(){
    
    };
    
    //起飞
    public void takeOff(){
    
    };
    
    //飞行
    public void flight(){
    
    };
    
    //降落
    public void landing(){
    
    };
    
    //装填
    public void loading(){
        
    };
    
    //投放
    public void PutOn(){
        
    };
}
```

# 总结：

## 本质：

抽象类-->像xxx一样  

接    口-->能xxx这样

抽象类是由下至上，由子类的共性提取出抽象类应该有的属性和行为，以便以在创建新的子类时更方便的获得这些共性。

接口是由上至下，由接口对实现类的某些功能进行约束和规范，以便于新的类能够快速、统一的实现这些功能。

又比如：电脑和手机都是电子设备，所以它们都需要电源、CPU，电脑的输入设备是鼠标键盘，是通过USB接口连接的。这里“电子设备”就是一个抽象类，电脑、手机都是它的子类，USB就是一个接口。但是如果新定义一种电子设备也想用鼠标键盘来实现输入，这时我们就不能自己再单独定义了连接方式了，因为这已经是一套规范了，键盘鼠标都是提供的USB接口连接，所以新的设备想使用键盘鼠标也必须实现USB接口。

## 注意点：
### 抽象类只能单继承，接口可以多实现。  

因为类的定义必须明确，一个事物是什么就是什么，它不能既是这个，又是那个。比如一个Java工程师，也许他还会PHP，会iOS，但是他就不能叫PHP工程师，也不能叫iOS工程师，因为他的职位是Java工程师，他只是实现了其他这些技能接口而已。HR招人也只是会定向招，先确定职位再研究你的技能。如果你这些技能实在是都精通，觉得只是找Java工程师太low了，想找一个新的定位方便要价。这时你就需要重新定义一个类叫“全栈工程师”，别人一看就知道你啥都会了。

### 抽象类和接口都不能自己实例化对象
因为抽象方法本身没有具体实现，创建的对象调用这些方法没有任何意义。所以拥有抽象方法的类一定是抽象类，只能通过子类继承才能体现它的价值所在。

### 抽象类可以提供成员方法的实现细节，而接口中只能存在抽象方法

因为抽象类是提取的子类的共性得到的，子类只是它逻辑的延伸，所以它能够代替子类实现一些子类共有的逻辑，而接口从本质来说就是制定规范，规范制定好了，怎么做都是实现类自己的事

### 抽象方法在子类或实现类中都是强制实现的

对于抽象类来说，抽象方法就是每个子类都该有的行为才能拿出来作为抽象方法，有些子类有这个方法有些子类没有呀，那这也根本不叫共性，也就不能单独作为抽象方法。

对于接口来说，接口本来就是规范作用，规范的意义就在于遵守，所以接口里的方法就不管三七二十一只管写就是了。

### 抽象类里面可以没有抽象方法，但有抽象方法的类一定是抽象类

没有抽象方法的抽象类意义不大

### 抽象方法不能是静态的static，也不能是私有的private
因为抽象类是不能实例化的，即不能被分配内存;而static修饰的方法在类实例化之前就已经别分配了内存，这样一来矛盾就出现了：抽象类不能被分配内存，而static方法必须被分配内存。所以抽象类中不能有静态的抽象方法。
定义抽象方法目的就是让子类去具体实现，所以不能是私有的，要让子类能够访问。