---
title: RxJava入门简介
date: 2017-9-16 3:39:01
tags: [Android,RxJava,安卓框架]
categories: [技术探索]
---
<center>让你的代码简洁起来，RxJava你值得拥有</center>

<!-- more -->

# 一、RxJava是什么？

> "a library for composing asynchronous and event-based programs using observable sequences for the Java VM"

以上是官方的解释即：一个在 Java VM上使用可观测的序列来组成异步的、基于事件的程序的库。

[github地址](https://github.com/ReactiveX/RxJava)

第一次看到这解释时简直是黑人问号脸，到底说的什么鬼，后来翻阅了国内诸位大神实践过后编写的文档，小弟终于领悟到了一点皮毛，何为RxJava?

## 针对复杂异步场景
对于异步我们都不应该陌生，安卓开发过程中无处不在，无论是网络获取数据，还是数据库读写操作，总之一切耗时操作都是需要异步执行的，那RxJava就是为**复杂异步操作**而生的库。

## 基于观察者设计模式
RxJava把异步处理拆解为了**观察者**和**被观察者**两部分，两者之间通过**订阅**操作建立联系。


# 二、怎样使用RxJava？

## 简单概念：

要想理解RxJava的意图，还得从其使用方法上入手，先来看RxJava最基本的用法：

比如说一个文本需要填充数据，需要**数据获取**和**数据呈现**两部分操作。



### 1、被观察者：
通过以下方式创建一个被观察者，被观察者往往就是代表着**数据获取**，把得到的数据作为参数放置于onNext（）方法中。

```java
Observable<String> observable = Observable.create(new Observable.OnSubscribe<String>() {

           @Override
            public void call(Subscriber<? super String> subscriber) {
            
                //这里是数据源获取操作...
                
                subscriber.onNext("Holle");  //发送数据"Holle"
            }
        });
```
### 2、观察者
通过以下方式创建一个观察者，其中会执行三个方法，分别代表：  

- onCompleted() : 数据获取成功时调用
- onError() : 数据获取失败时调用
- onNext() : 获取数据后的下一步操作

观察者就是从被观察者那里**得到数据**，并在回调方法onNext(String s)中执行**数据展示**，

```java
Observer<String> observer = new Observer<String>() {

            @Override
            public void onCompleted() {

                //数据接收完成时调用
            }

            @Override
            public void onError(Throwable e) {

                //发生错误调用
            }

            @Override
            public void onNext(String s) {

               //正常接收数据调用
                System.out.print(s);  //
            }
        };
```

### 3、订阅操作
observable和observer建立联系，要注意的是，订阅操作是 被观察者-**订阅**-观察者，即同一个数据源可以给多个观察者提供数据，类似于某些资讯类APP有目的性的给特定用户发送资讯推送

```java
observable.subscribe(observer);
```

## 基本概念及用法

### 1、基本概念：

- Observable：**被观察者** - 代表数据获取，内部主要执行数据获取操作，还可以链式调用**RxJava运算符**，在其中执行数据内容筛选，转换，存储等复杂操作；

- Observer：**观察者** - 主要在内部回调方法中执行数据接收或展示等操作；

- Subscriber：**订阅者** - Subscriber实现了Observer接口，比Observer多了一个最重要的方法unsubscribe( )，用来取消订阅，当你不再想接收数据了，可以调用unsubscribe( )方法停止接收，Observer 在 subscribe() 过程中,最终也会被转换成 Subscriber 对象，一般情况下，**建议使用Subscriber作为接收源**；

- Subscription ：Observable调用subscribe( )方法返回的对象，同样有unsubscribe( )方法，可以用来取消订阅事件；

- Action0：RxJava中的一个接口，它只有一个无参call（）方法，且无返回值，同样还有Action1，Action2...Action9等，Action1封装了含有 1 个参的call（）方法，即call（T t），Action2封装了含有 2 个参数的call方法，即call（T1 t1，T2 t2），以此类推；

- Func0：与Action0非常相似，也有call（）方法，但是它是有返回值的，同样也有Func0、Func1...Func9;

### 2、基本用法：

- Observable的创建

1.使用create( ),最基本的创建方式（这种方法**需要手动调用onCompleted**，才会回调Observer的onCompleted方法）：

```java
normalObservable = Observable.create(new Observable.OnSubscribe<String>() {
  @Override
  public void call(Subscriber<? super String> subscriber) {
      subscriber.onNext("create1"); //发射一个"create1"的String
      subscriber.onNext("create2"); //发射一个"create2"的String
      subscriber.onCompleted();//这种方法需要手动调用onCompleted，才会回调Observer的onCompleted方法
  }});
```

2.使用just( )，将为你创建一个Observable并自动为你调用onNext( )发射数据：


```java
justObservable = Observable.just("just1","just2");//依次发送"just1"和"just2"
```


3.使用from( )，参数传入集合，该方法将会遍历集合，发送每个item，每次发送一个：


```java
List<String> list = new ArrayList<>();
list.add("from1");
list.add("from2");
list.add("from3");
fromObservable = Observable.from(list);  //遍历list 每次发送一个
/** 注意，just()方法也可以传list，但是发送的是整个list对象，而from（）发送的是list的一个item** /
```


4.使用defer( )，有观察者订阅时才创建Observable，并且为每个观察者创建一个新的Observable：

```java
deferObservable = Observable.defer(new Func0<Observable<String>>() {
  @Override
  //注意此处的call方法没有Subscriber参数
  public Observable<String> call() {
      return Observable.just("deferObservable");
  }});
```

5.使用interval( ),创建一个按固定时间间隔发射整数序列的Observable，可用作**定时器**：


```java
intervalObservable = Observable.interval(1, TimeUnit.SECONDS);//每隔一秒发送一次
```

6.使用range( ),创建一个发射特定整数序列的Observable，第一个参数为起始值，第二个为发送的个数，如果为0则不发送，负数则抛异常：


```java
rangeObservable = Observable.range(10, 5);//将发送整数10，11，12，13，14
```

7.使用timer( ),创建一个Observable，它在一个给定的延迟后发射一个特殊的值，等同于Android中Handler的postDelay( )方法：

```java
timeObservable = Observable.timer(3, TimeUnit.SECONDS);  //3秒后发射一个值
```

8.使用repeat( ),创建一个重复发射特定数据的Observable:


```java
repeatObservable = Observable.just("repeatObservable").repeat(3);//重复发射3次
```
- Observer的创建

```java
mObserver = new Observer<String>() {
  @Override
  public void onCompleted() {
      LogUtil.log("onCompleted");
  }
  @Override
  public void onError(Throwable e) {
  }
  @Override
  public void onNext(String s) {
      LogUtil.log(s);
  }};
```

如果你不在意数据是否接收完或者是否出现错误，即不需要Observer的onCompleted()和onError()方法，可使用Action1，subscribe()支持将Action1作为参数传入,RxJava将会调用它的call方法来接收数据，代码如下：


```java
justObservable.subscribe(new Action1<String>() {
    @Override
    public void call(String s) {

          LogUtil.log(s);
     }});
```


# 三、为什么使用RxJava？

 单看基本用法可以说和普通的异步操作（AsyncTask、Handler）没什么区别，那使用RxJava究竟有什么好处
 
 参考以下例子：

```java
Observable.create(new Observable.OnSubscribe<List<User>>() {
          @Override
          public void call(Subscriber<? super List<User>> subscriber) {
              List<User> userList = null;
              ···
              //从数据库获取用户表数据并赋给userList
              ···
              subscriber.onNext(userList);
          } 
     }).flatMap(new Func1<List<User>, Observable<User>>() {
          @Override
          public Observable<User> call(List<User> users) {
              return Observable.from(users);
          }
      }).filter(new Func1<User, Boolean>() {
          @Override
          public Boolean call(User user) {
              return user.getName().equals("小明");
          }
      }).map(new Func1<User, User>() {
          @Override
          public User call(User user) { 
              //根据小明的数据user从数据库查找出小明的父亲user2
              return user2;
          }
      }).subscribeOn(Schedulers.io())
        .observeOn(AndroidSchedulers.mainThread())
        .subscribe(new Action1<User>() {
          @Override
          public void call(User user2) {
            //拿到谜之小明的爸爸的数据
          }
      });

```

在上面代码中我们可以看到Observable在调用订阅方法subscribe前还分别调用了flatMap()、filter()、map()、subscribeOn()、observeOn()等方法，这些方法就是RxJava的核心优势所在。  

flatMap()、filter()、map()方法就是RxJava操作符 - 主要对数据进行转换、预处理

subscribeOn()、observeOn()就是数据操作过程中的线程控制  - 设置数据获取和数据呈现等操作所在线程

 
##  RxJava常用操作符：
###     Map：
最常用且最实用的操作符之一，将对象转换成另一个对象发射出去，应用范围非常广，如数据的转换，数据的预处理等。
例一：数据类型转换，改变最终的接收的数据类型。假设传入本地图片路径，根据路径获取图片的Bitmap。

```java
Observable.just(filePath).map(new Func1<String, Bitmap>() {
  @Override
  public Bitmap call(String path) {

       return getBitmapByPath(path);
  }}).subscribe(new Action1<Bitmap>() {
   @Override
  public void call(Bitmap bitmap) {

          //获取到bitmap，显示
}});
```

例二：对数据进行预处理，最后得到理想型数据。实际开发过程中，从后台接口获取到的数据也许不符合我们想要的，这时候可以在获取过程中对得到的数据进行预处理（结合Retrofit）。


```java
Observable.just("12345678").map(new Func1<String, String>() {
  @Override
  public String call(String s) {
      return s.substring(0,4);//只要前四位
  }})
.subscribe(new Action1<String>() {
  @Override
  public void call(String s) {
      Log.i("mytag",s);
  }});
```

先说明一下，为了方便理解，所以写的例子都比较简单，不要以为明明可以简单用if-else解决的事，没必要用这种方式去写，当你真正将这些操作符使用到数据处理中去的时候，你就会发现有多方便。
FlatMap：和Map很像但又有所区别，Map只是转换发射的数据类型，而FlatMap可以将原始Observable转换成另一个Observable。还是举例说明吧。假设要打印全国所有学校的名称，可以直接用Map：
为了更清晰一点，先贴一下School类：


```java
public class School {

  private String name;
  private List<Student> studentList;

  public List<Student> getStudentList() {
      return studentList;
  }
  public void setStudentList(List<Student> studentList) {
      this.studentList = studentList;
  }
  public String getName() {
      return name;
  }
  public void setName(String name) {
      this.name = name;
  }
  public static class Student{
      private String name;
      public String getName() {
          return name;
      }
      public void setName(String name) {
          this.name = name;
      }
  }
}
```

接着用Map打印学校名称：


```java
List<School> schoolList = new ArrayList<>();
Observable.from(schoolList).map(new Func1<School, String>() {
  @Override
  public String call(School school) {
        return school.getName();
  }}).subscribe(new Action1<String>() {
  @Override
  public void call(String schoolName) {
        Log.i("mytag",schoolName);
  }});
```
### FlatMap：
再进一步，打印学校所有学生的姓名，先考虑用Map实现，将所有School对象直接转成Student：


```java
Observable.from(schoolList).map(new Func1<School, School.Student>() {
  @Override
  public School.Student call(School school) {
      return school.getStudentList();
  }}).subscribe(new Action1<School.Student>() {
  @Override
  public void call(School.Student student) {

          Log.i("mytag",student.getName());
  }});
```

看似可行，但事实上，这是一段错误的代码，细心的人就会发现错误的地方


```java
@Override
public School.Student call(School school) {
  return school.getStudentList();  //错误，Student 是一个对象，返回的却是一个list
}
```

所以用Map是无法实现直接打印学校的所有学生名字的，因为Map是一对一的关系，无法将单一的School对象转变成多个Student。前面说到，FlatMap可以改变原始Observable变成另外一个Observable，如果我们能利用from()操作符把school.getStudentList()变成另外一个Observable问题不就迎刃而解了吗，这时候就该FlatMap上场了，来看看它是怎么实现的：


```java
Observable.from(schoolList).flatMap(new Func1<School, Observable<School.Student>>() {
  @Override
  public Observable<School.Student> call(School school) {

      return Observable.from(school.getStudentList()); //关键，将学生列表以另外一个Observable发射出去

  }}).subscribe(new Action1<School.Student>() {

  @Override
  public void call(School.Student student) {
      Log.i("mytag",student.getName());
  }});
```

Map和FlatMap在我看来就像孪生兄弟一样，非常实用，实际开发中也我也经常使用，个人觉得要想上手RxJava，掌握这两个操作符必不可少。

### Buffer：
缓存，可以设置缓存大小，缓存满后，以list的方式将数据发送出去；例：


```java
Observable.just(1,2,3).buffer(2).subscribe(new Action1<List<Integer>>() {
  @Override
  public void call(List<Integer> list) {
      Log.i("mytag","size:"+list.size());
  }});
```

运行打印结果如下：


```java
11-02 20:49:58.370 23392-23392/? I/mytag: size:2
11-02 20:49:58.370 23392-23392/? I/mytag: size:1
```

在开发当中，个人经常将Buffer和Map一起使用，常发生在从后台取完数据，对一个List中的数据进行预处理后，再用Buffer缓存后一起发送，保证最后数据接收还是一个List，如下：


```java
List<School> schoolList = new ArrayList<>();
Observable.from(schoolList).map(new Func1<School, School>() {
  @Override
  public School call(School school) {
      school.setName("NB大学");  //将所有学校改名
      return school;
  }}).buffer(schoolList.size())  //缓存起来，最后一起发送
.subscribe(new Action1<List<School>>() {
  @Override
  public void call(List<School> schools) {   
}});
```

### Take：
发射前n项数据，还是用上面的例子，假设不要改所有学校的名称了，就改前四个学校的名称：

```java
Observable.from(schoolList).take(4).map(new Func1<School, School>() {
  @Override
  public School call(School school) {
      school.setName("NB大学");
      return school;
  }}).buffer(4).subscribe(new Action1<List<School>>() {
  @Override
  public void call(List<School> schools) {
  }});
```

### Distinct:
去掉重复的项，比较好理解：

```java
Observable.just(1, 2, 1, 1, 2, 3)
      .distinct()
      .subscribe(new Action1<Integer>() {
          @Override
          public void call(Integer item) {
              System.out.println("Next: " + item);
          }
      });
```

输出

```java
Next: 1
Next: 2
Next: 3
```

### Filter：
过滤，通过谓词判断的项才会被发射，例如，发射小于4的数据：

```java
Observable.just(1, 2, 3, 4, 5)
      .filter(new Func1<Integer, Boolean>() {
          @Override
          public Boolean call(Integer item) {
              return( item < 4 );
          }
      }).subscribe(new Action1<Integer>() {
        @Override
        public void call(Integer item) {
              System.out.println("Next: " + item);
    }});
```

输出：

```java
Next: 1
Next: 2
Next: 3
```
 
##  线程控制（Scheduler）：

使用RxJava，你可以使用subscribeOn()指定观察者代码运行的线程，使用observerOn( )指定订阅者运行的线程，
在不指定线程的情况下， RxJava 遵循的是线程不变的原则，即：在哪个线程调用subscribe( )，就在哪个线程生产事件；在哪个线程生产事件，就在哪个线程消费事件。如果需要切换线程，就需要用到 Scheduler （调度器）。  


RxJava 已经内置了几个 Scheduler ，它们已经适合大多数的使用场景：

- **Schedulers.immediate( )**: 直接在当前线程运行，相当于不指定线程。这是默认的 Scheduler。

- **Schedulers.newThread( )**: 总是启用新线程，并在新线程执行操作。

- **Schedulers.io( )**: I/O 操作（读写文件、读写数据库、网络信息交互等）所使用的 Scheduler。行为模式和 newThread() 差不多，区别在于 io() 的内部实现是是用一个无数量上限的线程池，可以重用空闲的线程，因此多数情况下 io() 比 newThread() 更有效率。不要把计算工作放在 io() 中，可以避免创建不必要的线程。

- **Schedulers.computation( )**: 计算所使用的 Scheduler。这个计算指的是 CPU 密集型计算，即不会被 I/O 等操作限制性能的操作，例如图形的计算。这个 Scheduler 使用的固定的线程池，大小为 CPU 核数。不要把 I/O 操作放在 computation() 中，否则 I/O 操作的等待时间会浪费 CPU。

- **AndroidSchedulers.mainThread()**：它指定的操作将在 Android 主线程运行。

有了以上这几个 Scheduler ，就可以使用 subscribeOn() 和 observeOn() 两个方法来对线程进行控制了。

- **subscribeOn( )**: 指定 subscribe() 所发生的线程，即 Observable.OnSubscribe 被激活时所处的线程。或者叫做事件产生的线程。经常设置为Schedulers.io( )用在获取数据为耗时操作的时候，比如说网络获取数据，数据库读写，文件读写。

- **observeOn( )**: 指定 Subscriber 所运行在的线程。或者叫做事件消费的线程。经常设置为AndroidSchedulers.mainThread()用在得到数据后，数据界面展示更新UI。

# 四、使用场景：

## RxJava + Retrofit
## RxBinding
## RxLifecyle
## RxBus
## RxPermission
 
# 五、参考文章：

[我所理解的RxJava——上手其实很简单（一）](http://www.jianshu.com/p/5e93c9101dc5)

[我所理解的RxJava——上手其实很简单（三）](http://www.jianshu.com/p/5c221c58e141  )

[RxJava 从入门到放弃再到不离不弃](https://www.daidingkang.cc/2017/05/19/Rxjava/)

[给 Android 开发者的 RxJava 详解 - 扔物线](http://gank.io/post/560e15be2dca930e00da1083)

[RxJava 与 Retrofit 结合的最佳实践 - tough1985](http://gank.io/post/56e80c2c677659311bed9841)

 