# 面向对象编程（OOP）
如何设计优秀的面向对象的程序？
让我们来看看
推荐视频（译者注：需科学上网）：
- 面向对象编程 - Part 1 -  https://www.youtube.com/watch?v=NOD802rMMCw
- 面向对象编程 - Part 2 - https://www.youtube.com/watch?v=i6EztA-F8UI

### 01：面向对象编程（OOP）- 基本术语
在我们开始面向对象编程学习前，先看几个例子。
人类的思维是一个循序渐进的过程。
假设我要乘飞机从伦敦到纽约。我是这么思考的：
- 坐出租车去伦敦机场
- 检票
- 过安检
- 登机
- 期待空姐
- 起飞
- 航行
- 着陆
- 下机
- 做出租车去...

过程式编程正是这种思考过程的反映。上面的思考过程用过程式编程可以写成：
```java
takeACabToLondonAirport();
checkIn();
passSecurity();
boardPlane();
wishHostess();
takeOff();
cruiseMode();
land();
getOffPlane();
//...
```
面向对象编程（OOP）为解决这一问题带来了新的方式。
从不同的参与者角度考虑怎么样？将数据存储到各个参与者自身怎么样？给它们一些职责并让他们做各自的事情怎么样？
当我们考虑不同的参与者并赋予它们各自的数据与职责，代码如下：
```
  Person
    name
    boardFlight(Plane flight), wishHostess (Hostess hostess), getOffFlight(Plane flight)

  AirPlane
    altitude, pilot, speed, flightMode
  takeOff(), cruiseMode(), land()

  Hostess
    welcome()
```
不用担心实现细节。把注意力放到不同的实现方法上。
这些已经封装了数据与方法的实体现在称作**对象**。我们已经定义了对象的范围与它能做的事情。
一个对象拥有：
- 状态: 数据
- 行为：操作方式

飞机的位置会随时间改变。一架飞机包含`takeOff()`，`land()`和`cruiseMode()`这些操作。所以，一个对象的行为可以影响它的状态。
是时候向你介绍一些核心**OOP**术语了，便于后面的学习。

#### OOP 术语

让我们回顾并加强一下前几节我们写的行星示例。这一次，我们也从概念的角度展开讨论。

***Planet***

```java
class Planet
  name, location, distanceFromSun // data / state / fields
  rotate(), revolve() // actions / behavior / methods

earth : new Planet
venus : new Planet
```

看一些**OOP**术语

**class**（类）是一个模板。一个**object**（对象）是一个类的实例。在上面的例子中，`Planet`是一个类。`earth`和`venus`是对象。

- `name`，`location`和`distanceFromSun`组成对象状态
- `rotate()`和`revolve()`定义了对象的行为

**Fields**（域）是组成对象状态的元素。对象的行为通过**Methods**（方法）实现。

每个行星拥有自己的状态：

- `name`： “Earth”，“Venus”
- `loaction`：各自的轨道
- `distanceFromSun`：不同的和太阳的距离

每个行星有自己的行为：

- `rotate()`：不同的自转速度（实际上，还有不同的方向！）
- `revolve()`：在各自轨道上不同的公转速度

#### 总结

在这一小节中，我们：

- 理解了面向对象编程（OOP）和面向过程编程的区别
- 了解了几个基本的面向对象编程（OOP）的术语

### 02：编程练习 PE-01

#### 练习

在下面每个系统中，识别所涉及的基本实体，并使用面向对象的术语组织它们

1. 网上购物系统
2. 人

#### 解题1：网上购物系统

```
Customer
  name, address
  login(), logout(), selectProduct(Product)
```

```
ShoppingCart
  items
  addItem(), removeItem()
```

```
Product
  name, price, quantityAvailable
  order(), changePrice()
```

#### 解题2：人

```
Person
  name, address, hobbies, work
  walk(), run(), sleep(), eat(), drink()
```

### 03：写一个MotorBike类

下面的一系列例子中，我们想为摩托车建模。我们会实例一些摩托车对象并使用它们。

两个java文件：

- ***MotorBike.java***，包含`MotorBike`类定义。这个类将会分装我们的摩托车状态和行为
- ***MotorBikeRunner.java***，拥有`main`方法的`MotorBikeRunner`类，程序的入口

##### Snippet-1: MotorBike 类

***MotorBike.java***

```java
package com.in28minutes.oops;
  public class MotorBike {
  //behavior
  void start() {
    System.out.println("Bike started!");
  }
}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();
  }
}
```

***控制台输出***

*Bike started!*

*Bike started!*

##### Snippet-1 说明

我们一开始创建了一个简单的`MotorBike`的类，有一个`start`方法。我们创建了几个实例并调用了`start`方法

我们创建两个类的原因是我们相信`Seperation of Concerns`（关注点分离）

- `MotorBike`类负责所有的数据和行为
- `MotorBikeRunner`类负责运行`MotorBike`示例

#### 总结

这一节，我们：

- 定义了一个`MotorBike`类便于我们更好地理解接下来几节的*OOP*概念

### 04：编程练习 OO-PE-02

#### 练习

1. 写一个小的Java项目，创建一个`Book`类，然后创建几个实例表示下面的书名
   - “The Art Of Computer Programming”
   - "Effective Java"
   - "Clean Code"

#### 解题

***Book.java***

```java
public class Book {
  private String title;

  public void setTitle(String bookTitle) {
    title = bookTitle;
  }

  public String getTitle() {
    return title;
  }
}
```

***BookRunner.java***

```java
public class BookRunner {
  public static void main(String[] args) {
    Book taocp = new Book();
    taocp.setTitle("The Art Of Computer Programming");
    Book ej = new Book();
    ej.setTitle("Effective Java");
    Book cc = new Book();
    cc.setTitle("Clean Code");
    System.out.println(taocp.getTitle());
    System.out.println(ej.getTitle());
    System.out.println(cc.getTitle());
  }
}
```

***控制台输出***

*The Art Of Computer Programming*

*Effective Java*

*Clean Code*

### 05：MotorBike - 表示状态

一个对象同时封装了*状态*和*行为*。

*状态* 定义了“对象在给定时间内的状态”。用**成员变量**表示*状态*。

在`MotorBike`示例中，如果我们想要每个`MotorBike`拥有`speed`属性，我们可以这样做。

##### Snippet-2：拥有speed变量的MotorBike 

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  int speed;
  void start() {
    System.out.println("Bike started!");
  }
}

```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();

    ducati.speed = 100;
    honda.speed = 80;
    ducati.speed = 20;
    honda.speed = 0;
  }
}
```

***控制台输出***

*Bike started!*

*Bike started!*

##### Snippet-2 说明

`MotorBike`中的`int speed;`语句定义了一个成员变量。

它能被对象访问，如`ducati`和`honda`，通过对象名限定。

```java
ducati.speed = 100;
honda.speed = 80;
```

`ducati`有它自己的`speed`值，`honda`同样如此。这些值相互之间是独立无关的。改变一个不会影响另外一个。

#### Classroom Exercise CE-OO-01

1. 给之前的创建的`Book`类增加一个`noOfCopies`成员变量，并演示如何针对前面指定的三个书名分别独立地设置和更新它。

#### 解题

TODO

### 06：MotorBike - get() 和 set() 方法 （译者注：原作者此处为07）

在前面的小节中，我们直接在`main()`愉快地修改了`ducati`和`honda`对象的`speed`属性。

```java
public class MotorBikeRunner {
  public static void main(String[] args) {
    //... Other code
    ducati.speed = 100;
    honda.speed = 0;
  }
}
```

这的确可行，但是破坏了**OOP**的封装性原则。

> 一个对象的方法不应该直接访问另外一个对象的状态。为此，这样的对象应该只允许调用目标对象自身的方法。

换句话说，一个成员变量不应该被它自身类外面声明的方法访问。

##### Snippet-3：含有私有变量的MotorBike

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  private int speed;

  void start() {
    System.out.println("Bike started!");
  }

  void setSpeed(int speed) {
    this.speed = speed;
  }
}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();

    ducati.setSpeed(100);
    honda.setSpeed(80);

    ducati.setSpeed(20);
    honda.setSpeed(0);
  }
}
```

***控制台输出***

*Bike started!*

*Bike started!*

##### Snippet-3 说明

通过将`speed`声明为`private`，我们为`MotorBike`提供了**访问控制**。Java的`public`和`private`关键字称为**访问修饰符**。它们控制外部对象可以访问给定对象的什么内容。

让我们看一下`setSpeed()`方法中的`this.speed = speed;`语句：

- 一个成员变量总是属于某个类的实例
- 一个方法的参数就像这个方法里的局部变量一样
- 为了区别它们，使用了`this`。`this.speed`代表了`Motorbike`对象的成员变量`speed`。在这个对象上调用`setSpeed()`方法

之前写的`MotorBikeRunner`代码，比如`ducati.speed = 100;` 现在这么写的话将会出错！正确访问和修改`speed`的值应该在`MotorBike`对象上调用合适的方法，比如`setSpeed()`。

#### Classroom Exercise CE-OO-02

1. 修改`Book`类，保证它不再破坏封装性原则。

#### 解题

TODO

#### 总结

这一节中，我们：

- 学习了需要使用访问控制实现封装性
- 发现Java提供了访问修饰符（如`public`和`private`）进行控制
- 理解了需要使用`get()`和`set()`方法访问对象的数据

### 07: 访问对象的状态

需要使用封装来防止对象的状态被其他对象直接访问。我们已经通过把`speed`声明为`private`来保护`MotorBike` 的状态。我们现在遇到了一种严格的情况，由于`speed`声明为`private`，导致无法访问`speed`。我们怎么处理这个问题呢？同样，答案是提供一个方法来读取现在的`speed`。

##### Snippet-4：MotorBike 的`getSpeed()`方法

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  //Same as before

  int getSpeed() {
    return this.speed;
  }
}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();

    ducati.setSpeed(100);
    honda.setSpeed(80);
    System.out.printf("Current Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Current Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

***Console Output***

*Bike started!*

*Bike started!*

*Current Ducati Speed is : 100*

*Current Honda Speed is : 80*

##### Snippet-4 说明

下面定义的`getSpeed()`方法允许我们访问当前`MotorBike`对象的`speed`。

> Eclipse 有一个非常方便的特性。当定义了一个类的成员变量以后，它会自动为每个成员变量生成默认的get()和set()方法。你会想经常使用这个功能的，可以节约打字的时间。
>
> `Right click on class > Generate Source > Generate Getters and Setters`

#### 总结

这一节中，我们：

- 了解了访问控制需要我们提供`get()`方法
- 学习了Eclipse为每个类属性生成`get()`和`set()`方法的小技巧

### 08：默认对象状态

如果一个对象的成员变量没有初始化值会发生什么？

##### Snippet-5：对象状态的默认初始化

***MotorBike.java***

```java
//Same as before
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike honda = new MotorBike();			
    System.out.printf("Current Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

***控制台输出***

***Current Honda Speed is : 0***

##### Snippet-5 说明

当我们实例化一个对象时，它的所有成员变量都会初始化成各自类型的默认值。在`MotorBike`中，`speed`声明为`int`类型的，所以它初始化为`0`。这样的初始化操作在`MotorBike`调用任何方法之前，包括`start()`。

尽管我们没有明确地初始化它，但`honda.getSpeed()`打印出了`0`。

默认值。

#### 总结

在这一节中，我们：

- 学习了对象的成员变量被赋予了默认值



### 09：封装的优点

封装的核心就是为了防止其他对象直接访问一个对象的状态。

我们最好看个例子来理解封装。

##### Snippet-6：封装的好处

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  private int speed;

  public void start() {
    System.out.println("Bike started!");
  }

  public void setSpeed(int speed) {
    this.speed = speed;
  }

  public int getSpeed() {
    return this.speed;
  }
}
```

***MotorBikeRunner.java\***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {

  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    ducati.start();
    ducati.setSpeed(-100);
    System.out.printf("Current Ducati Speed is : %d", ducati.getSpeed()).println();
  }
}
```

***控制台输出***

*Bike started!*

***Current Ducati Speed is : -100***

##### Snippet-6 说明

对于摩托车来说，`-100`的速度是不可能的。目前我们对其没有任何的验证。`setSpeed`方法让我们可以添加验证程序。

看一下怎么实现。

##### Snippet-7：速度是否正确验证

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {

  //Other code as is

  public void setSpeed(int speed) {
    if(speed > 0)
      this.speed = speed;
  }

}
```

***MotorBikeRunner.java***

```java
//Same as before
```

代码块的输出结果是:

*Bike started!*

***Current Ducati Speed is : 0***

##### Snippet-7 说明

`setSpeed()`检查`if(speed > 0)`，负值时不更新速度。

> 这不是完美的解决方案，因为`setSpeed`方法的调用者假设这个方法已经成功了。更好的是我们应该抛出一个异常表示验证出错。我们将会在后面讨论异常。

#### 总结

在这一节中，我们：

- 学习了封装的第一个有点 - 增加了数据验证的规定
- 以`MotorBike`为例，重点介绍了如何进行这样的验证

### 10：封装的优点（代码复用）

我们已经了解了OOP中封装的一些知识点。

假设现在我们想给Honda和Ducati两辆摩托车增加`100mph`的速度。逻辑很简单，对吧？先获取当前每辆摩托车的`speed`，并加上`100`，然后再重新给摩托车设置新的`speed`。下面的例子实现了这个逻辑。

##### Snippet-8：麻烦的增加速度代码

***MotorBike.java***

```java
// No Change
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();		
    honda.start();
    ducati.setSpeed(100);

    System.out.printf("Earlier Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Earlier Honda Speed is : %d", honda.getSpeed()).println();

    int ducatiSpeed = ducati.getSpeed();
    ducatiSpeed = ducatiSpeed + 100;
    ducati.setSpeed(ducatiSpeed);

    int hondaSpeed = honda.getSpeed();
    hondaSpeed = hondaSpeed + 100;
    honda.setSpeed(hondaSpeed);

    System.out.printf("Later Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Later Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

输出结果:

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 0*

***Later Ducati Speed is : 200***

***Later Honda Speed is : 100***

##### Snippet-8 说明

注意到`MotorBikeRunner`中的重复代码了吗？修改`ducati`的`speed`的代码几乎和`honda`一样。记得在本书的开头，我们是这么说的：

*“任何的计算机程序的目标是为了让任务对程序员来说更简单，更方便和更优雅。”*

OOP通过封装实现了所有的这些。将重复的逻辑用一个方法封装起来，然后传递特定对象的信息作为它的参数。下个例子展示了其中一种实现方式。

##### Snippet-9：通过代码封装增加速度

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  //Other code same as before
  public void increaseSpeed(int howMuch) {
    this.speed = this.speed + howMuch;
  }
}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {

    MotorBike duati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();

    ducati.setSpeed(100);

    System.out.printf("Earlier Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Earlier Honda Speed is : %d", honda.getSpeed()).println();

    ducati.increaseSpeed(100);
    honda.increaseSpeed(100);

    System.out.printf("Later Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Later Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

输出结果:

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 0*

***Later Ducati Speed is : 200***

***Later Honda Speed is : 100***

##### Snippet-9 说明

`MotorBike`类新增了`increaseSpeed()`方法。`ducati`和`honda`对象能够调用它。

现在我们给`MotorBike`类增加减速特性。

##### Snippet-10：代码封装实现速度增减

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  // Other methods same as before
  public void decreaseSpeed(int howMuch) {
    this.speed = this.speed - howMuch;
  }
}
```

***MotorBikeRunner.java\***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike();
    MotorBike honda = new MotorBike();
    ducati.start();
    honda.start();

    ducati.setSpeed(100);
    System.out.printf("Earlier Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Earlier Honda Speed is : %d", honda.getSpeed()).println();

    ducati.increaseSpeed(100);
    honda.increaseSpeed(100);
    ducati.decreaseSpeed(50);
    honda.decreaseSpeed(50);

    System.out.printf("Later Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Later Honda Speed is : %d", honda.getSpeed()).println();

    ducati.decreaseSpeed(200);
    honda.decreaseSpeed(200);

    System.out.printf("Final Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Final Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

输出结果:

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 0*

***Later Ducati Speed is : 150***

***Later Honda Speed is : 50***

***Final Ducati Speed is : -50***

***Final Honda Speed is : -150***

##### Snippet-10 说明

`MotorBike`类已经增加了`decreaseSpeed()`方法。`MotorBikeRunner`类的`main()`方法中的`ducati`和`honda`可以调用这个方法。

又出现了**负的速度值**，我们的验证逻辑需要改进。

##### Snippet-11：再次用方法验证

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {

  //Same as before

  public void increaseSpeed(int howMuch) {
    if(this.speed + howMuch > 0)
       this.speed = this.speed + howMuch;
  }

  public void decreaseSpeed(int howMuch) {
    if(this.speed - howMuch > 0)
       this.speed = this.speed - howMuch;
  }
}
```

***MotorBikeRunner.java***

```java
//Same as before
```

输出结果：

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 0*

*Later Ducati Speed is : 150*

*Later Honda Speed is : 50*

***Final Ducati Speed is : 150***

***Final Honda Speed is : 50***

##### Snippet-11 说明

我们已经实现了数据验证，因为如果想要把`ducati`和`honda`的速度减到`0`以下，现在会被忽略。

但是这样的代价就是代码冗余。

那我们怎么减少重复代码呢？

##### Snippet-12：利用代码复用进行验证

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  //Other methods same as before


  public void setSpeed(int speed) {
    if(speed > 0)
      this.speed = speed;
  }

  public void increaseSpeed(int howMuch) {
    setSpeed(this.speed + howMuch);
  }

  public void decreaseSpeed(int howMuch) {
    setSpeed(this.speed - howMuch);
  }
}
```

***MotorBikeRunner.java***

```java
//Same as before
```

输出结果：

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 0*

*Later Ducati Speed is : 150*

*Later Honda Speed is : 50*

***Final Ducati Speed is : 150***

***Final Honda Speed is : 50***

##### Snippet-12 说明

这种处理方式背后的思路是更新速度的操作和`set()`是一样。因为`setSpeed()`已经有了验证机制，所以在`increaseSpeed()`和`decreaseSpeed()`中传递适当的参数就可以调用它。

通过这种方式，验证逻辑可以通过更新方法重用。

> 注意。重复的逻辑会让你的代码难以维护。

##### 总结

这一小节中，我们：

- 开始研究封装的代码复用的优点
- 在数据验证的基础上，将这种思想映射到`MotorBike`示例

### 11：编程练习 PE-OO-03

#### 练习

1. 使用封装性编写`Book`类的方法
   - 增加书本数量
   - 减少书本数量

#### 解题

***BookRunner.java***

```java
public class BookRunner {
  public static void main(String[] args) {
    Book taocp = new Book();
    taocp.setTitle("The Art Of Computer Programming");
    Book ej = new Book();
    ej.setTitle("Effective Java");
    Book cc = new Book();
    cc.setTitle("Clean Code");

    System.out.println(taocp.getTitle());
    System.out.println(ej.getTitle());
    System.out.println(cc.getTitle());

    taocp.increaseCopies(10);
    ej.increaseCopies(15);
    cc.increaseCopies(20);
    taocp.decreaseCopies(5);
    ej.decreaseCopies(10);
    cc.decreaseCopies(15);

    System.out.println(taocp.getNumberOfCopies());
    System.out.println(ej.getNumberOfCopies());
    System.out.println(cc.getNumberOfCopies());
  }
}
```

***Book.java***

```java
public class Book {
  private String title;
  private int numberOfCopies;

  public void setTitle(String bookTitle) {
    title = bookTitle;
  }

  public String getTitle() {
    return title;
  }

  public void setNumberOfCopies(int numberOfCopies) {	
    if(numberOfCopies > 0) {
      this.numberOfCopies = numberOfCopies;
    }
  }

  public int getNumberOfCopies() {
    return numberOfCopies;
  }

  public void increaseCopies(int howMuch) {
    setNumberOfCopies(numberOfCopies + howMuch);
  }

  public void decreaseCopies(int howMuch) {
    setNumberOfCopies(numberOfCopies - howMuch);
  }
}
```

***控制台输出***

*The Art Of Computer Programming*

*Effective Java*

*Clean Code*

*5*

*5*

*5*

### 12：构造器介绍

当我们新建Ducati和Honda这两辆摩托车时，也许想给它们设置一个初始速度。

假设我们想让Ducati一开始有100mph的速度，并且Honda有200mph的速度。

##### Snippet-13：MotorBike 构造器

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  private int speed;


  MotorBike(int speed) {
    if(speed > 0)
      this.speed = speed;
  }

  //Same as before

}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike(100);
    MotorBike honda = new MotorBike(200);
    ducati.start();
    honda.start();
    System.out.printf("Earlier Ducati Speed is : %d", ducati.getSpeed()).println();
    System.out.printf("Earlier Honda Speed is : %d", honda.getSpeed()).println();
  }
}
```

输出结果：

*Bike started!*

*Bike started!*

*Earlier Ducati Speed is : 100*

*Earlier Honda Speed is : 200*

##### Snippet-13 说明

我们定义了拥有单个参数的`MotorBike`构造器

`public MotorBike(int speed) { /* Constructor Code Goes Here */ }`

构造器是一个命名和类名相同的方法。所有Java的对方法的规范同样适用于构造器。构造器不能被直接调用。

当使用`new`关键字实例化类对象时，会调用构造器方法。一个类的构造器方法可以接受任意个参数。接下来让我们为`MotorBike`构造器编写一些完整的代码。

#### 总结

这一节中，我们学习了类构造器的概念。

### 13：编程练习 PE-OO-04，构造器扩展知识

#### 练习

1. 重写`Book`类，增加构造器方法。这个构造器接受一个整形参数用来指定已经出版的副本数：
   - "The Art Of Computer Programming" : 100 副本
   - "Effective Java" : 75 副本
   - "Clean Code" : 60 副本

#### 解题

***BookRunner.java***

```java
public class BookRunner {
  public static void main(String[] args) {
    Book taocp = new Book(100);
    taocp.setTitle("The Art Of Computer Programming");

    Book ej = new Book(75);
    ej.setTitle("Effective Java");

    Book cc = new Book(60);
    cc.setTitle("Clean Code");

    System.out.println(taocp.getTitle());
    System.out.println(taocp.getNumberOfCopies());

    System.out.println(ej.getTitle());`
    System.out.println(ej.getNumberOfCopies());

    System.out.println(cc.getTitle());
    System.out.println(cc.getNumberOfCopies());
  }
}
```

***Book.java\***

```java
public class Book {
  private String title;
  private int numberOfCopies;

  public Book(int numberOfCopies) {
    this.numberOfCopies = numberOfCopies;
  }

  public void setTitle(String bookTitle) {
    title = bookTitle;
  }

  public String getTitle() {
    return title;
  }

  public int getNumberOfCopies() {
    return numberOfCopies;
  }
}
```

***控制台输出***

*The Art Of Computer Programming*

*100*

*Effective Java*

*75*

*Clean Code*

*60*

#### 构造器扩展知识

我们定义了`MotorBike`类，然后检验了`ducati`和`honda`两个`MotorBike`实例的方法。

我们一开始使用下面的命令创建`MotorBike`类的实例：

`MotorBike ducati = new MotorBike();`

你有注意到一些熟悉的东西吗？`new MotorBike()`表达式是不是和调用构造器方法很像？

实际上就是调用了`MotorBike`的构造器方法！

当我们在Java中定义了一个类（甚至看起来是一个空的类），会发生一些神奇的事情。看一下这个`Cart`类：

```java
class Cart {
  
};
```

这个类既没有成员变量也没有方法。当我们尝试实例化这个“空”的类：

```java
class CartRunner {
  public static void main(String[] args) {
    Cart cart = new Cart();
  }
}
```

代码似乎可以很顺利地编译、执行和初始化!实际上，编译器为`Cart`类生成了**默认的构造器**。

默认的构造器没有任何形参。就像用下面的方式定义`Cart`类：

```java
class Cart {
  public Cart() {
  }
};
```

构造器也可能有重载的定义。

现在我们默认初始化`MotorBike`类的实例，就像实例化`Cart`类一样。

##### Snippet-15：默认`MotorBike`构造器

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {

  private int speed;

  MotorBike(int speed) {
    if(speed > 0)
      this.speed = speed;
  }
}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike(100);
    MotorBike honda = new MotorBike(200);
    MotorBike yamaha = new MotorBike();
  }
}
```

***控制台输出***

***Compiler Error***

##### Snippet-15 说明

**MotorBikeRunner.java**文件编译出错。`MotorBike yamaha = new MotorBike();`编译失败了。为什么？

查立并没有生成默认的构造器！如果你已经在类中定义了构造器，那编译器就不会添加默认的构造器了。**如果你不喜欢我为你做的事情，那你就自己去做！**这就是编译器的回应。

如果你需要默认的构造器，可以显示地写出来。

##### Snippet-16：程序员自定义的默认构造器

***MotorBike.java***

```java
package com.in28minutes.oops;

public class MotorBike {
  //state
  private int speed;

  //behavior
  MotorBike() {
    this(5);
  }

  MotorBike(int speed) {
    if(speed > 0)
      this.speed = speed;
  }

}
```

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike(100);
    MotorBike honda = new MotorBike(200);
    MotorBike yamaha = new MotorBike();
    System.out.printf("Earlier Yamaha Speed is : %d", yamaha.getSpeed()).println();
  }
}
```

输出结果：

***Earlier Yamaha Speed is : 5***

##### Snippet-16 说明

我们为`MotorBike`类定义了0个形参的构造器使对象可以默认初始化。但是`this(5);`这条语句是干什么的？

我们在`MotorBike()`中利用`this`关键字调用了构造函数`MotorBike(int)`。