# 面向对象编程（OOP）- 回顾
在这一节中，我们将基于以下指示重新回顾OOP的原理：
- 数组及其变体
- 内置Java类和实用程序
- 条件循环（一般的和增强的）

### 对象回顾 - 状态和行为
对象的属性决定了它的构成。在对象生命周期的不同时间点，其任何属性的值都可以改变。

在给定的任何时刻，这些属性值定义了这个对象的**状态**。

在`MotorBike`例子中，`speed`属性定义了`MotorBike`的状态。`ducati`的`speed`定义了它的状态。

对象如何响应外部事件或发送给它的消息定义了其行为。

使用方法可以传递消息给一个对象。方法用来实现对象的**行为**。

`setSpeed`，`increaseSpeed`和`decreaseSpeed`这些方法对所观测到的`MotorBike`的`speed`有影响。`MotorBike`未来的状态依赖于它的行为和当前的状态。

行为影响状态。状态也会影响行为。

***MotorBikeRunner.java***

```java
package com.in28minutes.oops;

public class MotorBikeRunner {
  public static void main(String[] args) {
    MotorBike ducati = new MotorBike(100);
    MotorBike honda = new MotorBike(200);
    MotorBike yamaha = new MotorBike();
    ducati.start();
    honda.start();
    yamaha.start();

    ystem.out.println(ducati.getSpeed());
    System.out.println(honda.getSpeed());
    System.out.println(yamaha.getSpeed());

    ducati.increseSpeed(50);
    yamaha.setSpeed(250);
    honda.increaseSpeed(100);
    yamaha.decreaseSpeed(50);
    System.out.println(ducati.getSpeed());
    System.out.println(honda.getSpeed());
    System.out.println(yamaha.getSpeed());
  }
}
```

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

  public void start() {
    System.out.println("Bike started!");
  }

  public void setSpeed(int speed) {
    if(speed > 0)
      this.speed = speed;
  }

  public int getSpeed() {
    return this.speed;
  }

  public void increaseSpeed(int howMuch) {
    setSpeed(this.speed + howMuch);
  }

  public void decreaseSpeed(int howMuch) {
    setSpeed(this.speed - howMuch);
  }
}
```

### 02：管理类的状态

在基础阶段上，当我们设计类时，我们需要决定：

- `状态（state）` - 成员变量
- `如何创建对象` - 定义构造器
- `行为（behavior）` - 向外暴露的方法

看一下类`Fan`这个例子。

与这个类设计相对应的以上三个主要领域如下：

- 状态
  - make
  - radius
  - color
  - isOn
  - speed
- 构造器
  - Fan(String make, double radius, String color)
- 行为
  - void switchOn()
  - void switchOff()
  - void changeSpeed(int change)
  - String toString()

让我们尝试写一个简单的`Fan`类，涵盖所有这些方面。

***Fan.java***

```java
package com.in28minutes.oops.level2;

public class Fan {
  //state
  private String make;
  private double radius;
  private String color;
  private boolean isOn;
  private byte speed;	//levels: 0 to 5

  //constructors

  public Fan(String make, double radius, String color) {
    this.make = make;
    this.radius = radius;
    this.color = color;
  }

  //methods
  public String toString() {
    return String.format("Make : %s, Radius : %f, Color : %s, Is On : %b, Speed : %d",
                make,
                radius,
                color,
                isOn,
                speed);
  }
}
```

***FanRunner.java***

```java
package com.in28minutes.oops.level2;

public class FanRunner {
  public static void main(String[] args) {
    Fan fan = new Fan("Fan-Tastic", 0.456, "GREEN");
    System.out.println(fan);
  }
}
```

***控制台输出***

*Make : Fan-tastic, Radius : 0.45600, Color : GREEN, Is On : false, Speed : 0*

构造器未设置的字段`isOn`和`speed`，根据它们各自的数据类型设置默认值，即`false`（对于`booelan`）和`0`（对于`int`）。