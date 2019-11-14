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

### 03：增加 Fan 类的行为

我们需要确定`Fan`对象应提供哪种行为。

`Fan`类对象的默认状态属性，`make`，`color`和`radius`在构造时就固定了，而且不能被此类实例的用户修改。

另外两个状态属性，`isOn`和`speed`需要暴露出来被`Fan`对象用户修改。我们将会提供方法来修改它们。

##### Snippet-01；`Fan`类 - v4

***FanRunner.java***

```java
package com.in28minutes.oops.level2;

public class FanRunner {
  public static void main(String[] args) {
    Fan fan = new Fan("Fan-Tastic", 0.456, "GREEN");
    System.out.println(fan);
    fan.switchOn();
    System.out.println(fan);
    fan.setSpeed((byte)5);
    System.out.println(fan);
    fan.switchOff();
    System.out.println(fan);
  }
}
```

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

  //isOn
  /*public void isOn(boolean isOn) {
    this.isOn = isOn;
  }*/

  public void switchOn() {
    isOn = true;
    setSpeed((byte)1);
  }

  public void switchOff() {
    isOn = false;
    setSpeed((byte)0);
  }

  public void setSpeed(byte speed) {
    this.speed = speed;
  }
}
```

***控制台输出***

*Make : Fan-Tastic, Radius : 0.45600, Color : GREEN, Is On : false, Speed : 0*

*Make : Fan-Tastic, Radius : 0.45600, Color : GREEN, Is On : true, Speed : 1*

*Make : Fan-Tastic, Radius : 0.45600, Color : GREEN, Is On : true, Speed : 5*

*Make : Fan-Tastic, Radius : 0.45600, Color : GREEN, Is On : false, Speed : 0*

##### Snippet-01 说明
- 关于状态属性`isOn`：
    - 像`public void isOn(boolean)`这样的状态更改器方法不是首选的，尽管它确实修改了这个属性。因为它从类使用者角度来看并不直观。
    - 另外，诸如`public void switchOn()`和`public void switchOff()`这样的方法不仅可以切换`isOn`属性，而且对于`Fan`类（这里是`FanRunner`类）的使用者来说更直观，更有用。
- 关于状态属性`speed`：
    - `setSpeed`既直观又有用，所以这里不再重新讨论
    - `speed`会被`switchOn()`和`switchOff()`操作影响。我们已经在这些方法定义中调用了`setSpeed()`方法
#### 总结
设计类最好的方式是使用由外而内的思考过程：
- 谁可能使用我的类？
- 哪些功能他们绝对需要？

### 04：编程练习 PE-OOP-01

1. 写一个简单的`Rectangle`类，有以下成分构成：
   - 状态
     - length
     - width
   - 构造器
   - 行为或方法

#### Solution To PE-OOP-01

***RectangleRunner.java***

```java
package com.in28minutes.oops.level2;

public class RectangleRunner {
  public static void main(String[] args) {
    Rectangle rectangle = new Rectangle(12, 23);
    System.out.println(rectangle);
    rectangle.setWidth(25);
    System.out.println(rectangle);
    rectangle.setLength(20);
    System.out.println(rectangle);
  }
}
```

***Rectangle.java***

```java
package com.in28minutes.oops.level2;

public class Rectangle {
  //state:
  private int length;
  private int width;

  //creation:
  public Rectangle(int length, int width) {
    this.length = length;
    this.width = width;
  }

  //behaviors:
  public int getLength() {
    return length;
  }

  public int getWidth() {
    return width;
  }

  public void setLength(int length) {
    this.length = length;
  }

  public void setWidth(int width) {
    this.width = width;
  }

  public int area() {
    return length * width;
  }

  public int perimeter() {
    return 2*(length + width);
  }

  public String toString() {
    return String.format("Rectangle - length : %d, width : %d, area : %d, perimeter : %d", 
                length,
                width,
                area(),
                perimeter());
  }
}
```

***控制台输出***

*Rectangle - length : 12, width : 23, area : 276, perimeter : 70*

*Rectangle - length : 12, width : 25, area : 300, perimeter : 74*

*Rectangle - length : 20, width : 25, area : 500, perimeter : 90*

#### Solution 说明

- 一个不确定`length`和`width`的`Rectangle`对象没有意义，所以没有提供默认的构造器。

### 05：了解对象组成

让我们回顾以下类`Fan`的状态属性。

***Fan.java***

```java
package com.in28minutes.oops.level2;

public class Fan {
  //state
  private String make;
  private double radius;
  private String color;
  private boolean isOn;
  private byte speed;

  //constructors
  //methods
}
```

类`Fan`所有的成员变量都是基本类型。我们能让它复杂点并包含其他类吗？

##### Snippet-01：对象组成 - 状态

***CustomerRunner.java***

```java
package com.in28minutes.oops.level2;

public class CustomerRunner {
  public static void main(String[] args) {
    Customer customer = new Customer();
  }
}
```

***Address.java***

```java
package com.in28minutes.oops.level2;

public class Address {
  //state
  private String doorNo;
  private String streetInfo;
  private String city;
 	private String zipCode;
  
  //creation
  //behaviors
}
```

***Customer.java***

```java
package com.in28minutes.oops.level2;

public class Customer {
  //state
  private String name;
  private Address homeAddress;
  private Address workAddress;

  //creation
  //behaviors
}
```

##### Snippet-01 说明

`Customer customer`由以下部分组成：

- `name`
- `homeAddress`
- `workAddress`

`String`是内置类型，它很简单。`Address`是用户定义的类型，它由下面部分组成：

- `doorNo`
- `streetInfo`
- `city`
- `zipCode`

##### Snippet-02：对象的组成 v2 - 构造

现在让我们添加构造器，用于简单地创建一些对象。

***CustomerRunner.java***

```java
package com.in28minutes.oops.level2;

public class CustomerRunner {
  public static void main(String[] args) {
    //Customer customer = new Customer();
    Address homeAddress = new Address("Flat No. 51", "Hiranandani Gardens", "Mumbai", "400076");
    Address workAddress = new Address("Administrative Office", "Western Block", "Mumbai", "400076");
    Customer customer = new Customer("Ashwin Tendulkar", homeAddress, workAddress);
  }
}
```

***Address.java***

```java
package com.in28minutes.oops.level2;

public class Address {
  //state
  private String doorNo;
  private String streetInfo;
  private String city;
  private String zipCode;

  //creation
  public Address(String doorNo, String streetInfo, String city, String zipCode) {
    this.doorNo = doorNo;
    this.streetInfo = streetInfo;
    this.city = city;
    this.zipCode = zipCode;
  }

  //behaviors
}
```

***Customer.java***

```java
package com.in28minutes.oops.level2;

public class Customer {
  //state
  private String name;
  private Address homeAddress;
  private Address workAddress;

  //creation
  //workAddress not mandatory for creation
  public Customer(String name, String homeAddress) {
    this.name = name;
    this.homeAddress = homeAddress;
  }

  //behaviors
}
```

##### Snippet-03：对象组成 v3 - 行为

让我们添加提供行为的方法。

***CustomerRunner.java***

```java
package com.in28minutes.oops.level2;

public class CustomerRunner {
  public static void main(String[] args) {
    //Customer customer = new Customer();
    Address homeAddress = new Address("Flat No. 51", "Hiranandani Gardens", "Mumbai", "400076");
    Customer customer = new Customer("Ashwin Tendulkar", homeAddress);
    System.out.println(customer);
    Address workAddress = new Address("Administrative Office", "Western Block", "Mumbai", "400076");
    customer.setWorkAddress(workAddress);
    System.out.println(customer);
  }
}
```

***Address.java***

```java
package com.in28minutes.oops.level2;

public class Address {
  //state
  private String doorNo;
  private String streetInfo;
  private String city;
  private String zipCode;

  //creation
  public Address(String doorNo, String streetInfo, String city, String zipCode) {
    super();
    this.doorNo = doorNo;
    this.streetInfo = streetInfo;
    this.city = city;
    this.zipCode = zipCode;
  }

  //behaviors
  public String toString() {
    return doorNo + ", " + streetInfo + ", " + city + " - " + zipCode;
  }
}
```

***Customer.java***

```java
package com.in28minutes.oops.level2;

public class Customer {
  //state
  private String name;
  private Address homeAddress;
  private Address workAddress;

  //creation
  //workAddress not mandatory for creation
  public Customer(String name, String homeAddress) {
    this.name = name;
    this.homeAddress = homeAddress;
  }

  //behaviors
  //certain components of homeAddress and workAddress can be modified, not the name
  public void setHomeAddress(Address homeAddress) {
    this.homeAddress = homeAddress;
  }

  public void setWorkAddress(Address workAddress) {
    this.workAddress = workAddress;
  }

  public Address getHomeAddress() {
    return homeAddress;
  }

  public Address getWorkAddress() {
    return workAddress;
  }

  public String toString() {
    return String.format("Customer [%s] lives at [%s], works at [%s]", 
                name,
                homeAddress,
                workAddress);
  }
}
```

***控制台输出***

*Customer [Ashwin Tendulkar] lives at [Flat No. 51, Hiranandani Gardens, Mumbai - 400076], works at [null]*

*Customer [Ashwin Tendulkar] lives at [Flat No. 51, Hiranandani Gardens, Mumbai - 400076], works at [Administrative Office, Western Block, Mumbai - 400076]*

### 06：编程练习 PE-OOP-02

#### Exercises

编写一个程序用来管理书本和书评

- Book：
  - `id`
  - `name`
  - `authoer`
- Review:
  - `id`
  - `description`
  - `rating`

```java
Book book = new Book(123, "Object Oriented Programming With Java", "Ranga");
book.addReview(new Review(10, "Great Book", 4));
book.addReview(new Review(101, "Awesome", 5));
System.out.println(book);
```

#### Solution To PE-OOP-02

***BookReviewRunner.java***

```java
package com.in28minutes.oops.level2;

public class BookReviewRunner {
  public static void main(String[] args) {
    Book book = new Book(123, "Object Oriented Programming With Java", "Ranga");
    book.addReview(new Review(10, "Great Book", 4));
    book.addReview(new Review(101, "Awesome", 5));
    System.out.println(book);
  }
}
```

***Review.java***

```java
package com.in28minutes.oops.level2;

public class Review {
  private int id;
  private String description;
  private byte rating;

  public Review(int id, String description, byte rating) {
    this.id = id;
    this.description = description;
    this.rating = rating;
  }

  public String toString() {
    return "(Review-" + id + ", " + description + ", " + rating + ")";
  }
}
```

***Booke.java***

```java
package com.in28minutes.oops.level2;

public class Book {
  private int id;
  private String title;
  private String author;

  private ArrayList<Review> reviewList = new ArrayList<Review>();
  public Book(int id, String title, String author) {
    this.id = id;
    this.title = title;
    this.author = author;
  }

  public void addReview(Review review) {
    reviewList.add(review);
  }

  public String toString() {
    return "Book-" + id + ",  " + title + ", " + author + ", " + reviews);
  }
}
```

***控制台输出***

*Book-123, Object Oriented Programming With Java, Ranga, [(Review-10, Great Book", 4), (Review-101, Awesome, 5)]*

### 07：继承的需要

让我们看两个类，`Person`和`Student`。

***Person.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class Person {
  private String name;
  private String email;
  private String phoneNumber;

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getEmail() {
    return email;
  }

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }

  public String getPhoneNumber() {
    return phoneNumber;
  }
}
```

***StudentWithoutInheritance.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class StudentWithoutInheritance {
  private String name;
  private String email;
  private String phoneNumber;
  private String college;
  private int year;

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getEmail() {
    return email;
  }

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }

  public String getPhoneNumber() {
    return phoneNumber;
  }

  public void setCollege(String college) {
    this.college = college;
  }

  public String getCollege() {
    return college;
  }

  public void setYear(int year) {
    this.year = year;
  }

  public int getYear() {
    return year;
  }
}
```

从上面的代码示例中，你可以看到有很多东西

- `Person`的成员变量，`name`，`email`和`phoneNumber`在`Student`中重复了。
- `Person`中各个域的更改器和访问器也在`Student`中重复了。

每一个`Student`都是`Person`。假如我们能扩展`Person`类而不是重写所有东西会怎么样？

#### 开始继承

`Student`**是**`Person`。Java支持一种基本的面向对象范例：**继承**。

`Student`能够继承`Person`，用来模拟一个`Student`是一个`Person`这个事实。

在定义`Student`这个类时，可以使用Java关键字`extends`来实现。

```java
public class Person {
  // <Person Definition>
}

public class Student extends Person {
  // <Student Definition, after reusing Person Code>
}
```

继承是代码重用的一种机制。在这个例子中，所有之前在`Person`中定义的域和方法同样在`Student`中有效。

在这种继承关系中，`Person`称为`Student`的**超类**。同样地，`Student`是`Person`的**子类**。

让我们看看如何去修改`Student`类的定义。

##### Snippet-02：Student 继承 Person - v1

***Person.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class Person {
  private String name;
  private String email;
  private String phoneNumber;

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  public void setEmail(String email) {
    this.email = email;
  }

  public String getEmail() {
    return email;
  }

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }

  public String getPhoneNumber() {
    return phoneNumber;
  }
}
```

***Student.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class Student extends Person {
  private String collegeName;
  private int year;

  public void setCollegeName(String college) {
    this.collegeName = collegeName;
  }

  public String getCollegeName() {
    return collegeName;
  }

  public void setYear(int year) {
    this.year = year;
  }

  public int getYear() {
    return year;
  }
}
```

***StudentRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;
public class StudentRunner {
  public static void main(String[] args)
    Student student = new Student();
    // < all setter() and getter() methods of Person and Student available >
    student.setName("Ranga");			
    student.setEmail("in28minutes@gmail.com");
  }
}
```

