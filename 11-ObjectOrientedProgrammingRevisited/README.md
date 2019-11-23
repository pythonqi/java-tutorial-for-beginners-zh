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

##### Snippet-01：`Fan`类 - v4

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

### 08：Obejct类的介绍
在Java中，每个类，不论是Java内置库的类，还是用户自定义的类，都隐式继承了`Object`类。
`Object`类可以在Java系统包`java.lang`中查看。这个类位于Java类继承层次的根部。所有的类，包括数组，实现/继承了这个类的方法。
让我们看一下`Person`和`Student`类。

##### Snippet-01：`Object`类
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

    public void setCollegeName(String collegeName) {
        this.collegeName = collegeName;
    }

    public String getCollegeName() {
        return collegeName;
    }

    public void setYear(int year) {
        this.year = year;
    }

    punlic int getYear() {
        return year;
    }
}
```

***StudentRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class StudentRunner {
  public static void main(String[] args)
    //Student student = new Student();
    //student.setName("Ranga");
    //student.setEmail("in28minutes@gmail.com");

    Person person = new Person();
    String personStr = person.toString();
    System.out.println(personStr);
    System.out.println(person);
    int hashCode = person.hashCode();			
    person.notify();
  }
}
```

***控制台输出***

*com.in28minutes.oops.level2.inheritance.Person@7a46a697*

*com.in28minutes.oops.level2.inheritance.Person@7a46a697*

##### Snippet-01 说明

作为默认实现的`Object`类的方法，比如`toString()`，`hashCode()`和`notify()`，`Person`类的对象可以使用这些方法。

`System.out.println(person);`这条语句实际上会转化成`System.out.println(person.toString())`。因为Java系统隐式调用了`person.toString()`，这是从`Object`类继承下来的。

### 09：集合和方法重载

子类从父类继承的特性

- 状态属性：超类的成员变量
- 行为部分：超类定义的方法

这些当然是可以在子类中分别进行访问（和修改）与调用的。

你也可以在子类中覆盖父类中的方法实现 - **方法重载**。

##### Snippet-01：方法重载

**Person.java**

```java
package com.in28miutes.oops.level2.inheritance;

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
  
  public void setEmail(String emial) {
    this.emial = emial;
  }
  
  public String getEmail() {
    return emial;
  }
  
  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }
  
  public String getPhoneNumber() {
    return phoneNumber;
  }
  
  public String toString() {
    return String.format("Person %s, Emial : %s, Phone Number : %s", name, email, phoneNumber);
  }
}
```

***PersonRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class PersonRunner {
  public static void main(String[] args) {
    Person person = new Person();
    person.setName("Ranga");
    person.setEmail("in28minutes@gmail.com");
    person.setPhoneNumber("9898989898");
    String personStr = person.toString();
    System.out.println(personStr);
    System.out.println(person);
  }
}
```

***控制台输出***

*Person Ranga , Email : [in28minutes@gmail.com](mailto:in28minutes@gmail.com), Phone Number : 9898989898*

*Person Ranga , Email : [in28minutes@gmail.com](mailto:in28minutes@gmail.com), Phone Number : 9898989898*

##### Snippet-01 说明

通过在`Person`这个子类中定义`toString()`方法，我们覆盖了父类`Object`提供的默认`toString()`版本。

### 10：Classromm Exercise CE-OOP-01

创建一个`Person`类（译者注：原文将`Person`写成了`Student`，作者笔误）扩展成`Employee`类，包含以下属性：

- `title`
- `employerName` （译者注：原文为`employer`，与后面代码不符，作者笔误）
- `employeeGrade`
- `salary`

为`Employee`创建一个`toString()`方法，打印包括`Person`状态属性在内的所有状态属性值。

##### Snippet-01：Employee 继承

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

  public String toString() {
    return Sring.format("Person %s , Email : %s, Phone Number : %s", name, email, phoneNumber);
  }
}
```

***Employee.java***

```java
package com.in28minutes.oops.level2.inheritance;
import java.math.BigDecimal;

public class Employee extends Person {
  private String title;
  private String employerName;
  private char employeeGrade;
  private BigDecimal salary;

  public void setTitle(String title) {
    this.title = title;
  }

  public String getTitle() {
    return title;
  }

  public void setEmployerName(String employer) {
    this.employerName = employerName;
  }

  public String getEmployerName() {
    return employerName;
  }

  public void setEmployeeGrade(char  employeeGrade) {
    this.employeeGrade = employeeGrade;
  }

  public char getEmployeeGrade() {
    return employeeGrade;
  }

  public void setSalary(BigDecimal  salary) {
    this.salary = salary;
  }

  public BigDecimal getSalary() {
    return salary;
  }

  public String toString() {
    return String.format("Employee Title: %s, Employer: %s, Employee Grade: %c, Salary: %s",
                title,
                employerName,
                employeeGrade,
                salary);
  }
}
```

***EmployeeRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class EmployeeRunner {
  public static void main(String[] args) {
    Employee employee = new Employee();
    employee.setName("Ranga");
    employee.setEmail("in28minutes@gmail.com");
    employee.setPhoneNumber("123-456-7890");
    employee.setTitle("Programmer Analyst");
    employee.setEmployerName("In28Minutes");
    employee.setEmployeeGrade('A');
    employee.setSalary(new BigDecimal("50000"));
    System.out.println(employee);
  }
}
```

***控制台输出***

*Employee Title: Programmer Analyst, Employer: In28Minutes, Employee Grade: A, Salary: 50000.0000*

##### Snippet-01 说明

我们没有在重载的`Employee.toString()`方法中打印`Person`对象信息。让我们看看下一步。

### 11：构造器与`super()`调用

`super`关键字允许子类访问父类中存在的属性。

##### Snippet-01：调用 Person.toSring()

***Employee.java***

```java
package com.in28minutes.oops.level2.inheritance;
import java.math.BigDecimal;

public class Employee extends Person {
	//focusing only on the toString() method
	public String toString() {
		return String.format("Employee Name: %s, Email: %s, Phone Number: %s, Title: %s, Employer: %s, Employee Grade: %c, Salary: %s",
								super.getName(),
								super.getEmail(),
								super.getPhoneNumber(),
								title,
								employerName,
								employeeGrade,
								salary);
	}
}
```
***EmployeeRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class EmployeeRunner {
	public static void main(String[] args) {
		Employee employee = new Employee();
		employee.setName("Ranga");
		employee.setEmail("in28minutes@gmail.com");
		employee.setPhoneNumber("123-456-7890");
		employee.setTitle("Programmer Analyst");
		employee.setEmployerName("In28Minutes");
		employee.setEmployeeGrade('A');		
		employee.setSalary(new BigDecimal("50000"));
		System.out.println(employee);
	}
}
```
***控制台输出***

Employee Name: Ranga, Email: in28minutes@gmail.com, Phone Number: 123-456-7890, Title: Programmer Analyst, Employer: In28Minutes, Employee Grade: A, Salary: 50000.0000

`super`关键字允许子类访问父类中存在的属性。因此，我们可以在`Employee`对象中调用`Person`对象的getter方法，比如`Employee.toString()`中的`super.getName()`，`super.getEmail()`和`super.getPhoneNumber()`。

#### 子类构造器

子类对象创建时发生了什么？有调用父类的构造器吗？

##### Snippet-02：Person 类

***Person.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class Person {

  public Person() {
    System.out.println("Inside Person Constructor");
  }

}
```

***Employee.java***

```java
package com.in28minutes.oops.level2.inheritance;
import java.math.BigDecimal;

public class Employee extends Person {

  public Employee() {
    //super();
    System.out.println("Inside Employee Constructor");
  }

}
```

***EmployeeRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class EmployeeRunner {
  public static void main(String[] args) {
    Employee employee = new Employee();
  }
}
```

***控制台输出***

*Inside Person Constructor*

*Inside Employee Constructor*

##### Snippet-02 说明

当创建子类对象时

- 调用了子类构造器，而且它隐式调用了它的父类构造器。

Java编译器将`super();`这行代码插入到子类默认构造器的第一行（如果它没有被程序员显示地添加的话），这里是`Employer()`构造器。

- `super();`相当于调用了父类的默认构造器。
- 因此，始终在子类构造器之前调用父类构造器。

##### Snippet-03：`Person` - 非默认构造器

让我们删除`Person`类里的无参构造器，然后再添加有一个参数的构造器。

```java
  public Person(String name) {
    this.name = name;
  }
```

***PersonRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class PersonRunner {
  public static void main(String[] args)
    Person person = new Person("Ranga");
    person.setEmail("in28minutes@gmail.com");
    person.setPhoneNumber("123-456-7890");
    System.out.println(person);
  }
}
```

***控制台输出***

*Person Ranga , Email : [in28minutes@gmail.com](mailto:in28minutes@gmail.com), Phone Number : 123-456-7890*

##### Snippet-03 说明

当我们为`Person`类（译者注：原文为`Employee`，作者笔误）添加了带一个参数的构造器时，现存的**EmployeeRunner.java**代码会报编译错误，因为在`Person`中已经没有默认的构造器了。

`super()`在`Employee`里的默认构造器中无法被调用。

一个选择是把无参构造器放回去

```java
public Person() {
  System.out.println("Inside Person Constructor");
}
```

但是，实际上创建一个没有`name`的`Person`是没意义的，对吧？

这个例子的解决办法是调用这个带一个参数的构造器`Person(String name)`，比如使用`super(name);`。

```java
  public Employee(String name, String title, String employerName, char employeeGrade) {
    super(name);
    this.title = title;
    this.employerName = employerName;
    this.employeeGrade = employeeGrade;
  }
```

***EmployeeRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class EmployeeRunner {
  public static void main(String[] args) {
    Employee employee = new Employee("Ranga", "Programmer Analyst", "In28Minutes", 'A');
    System.out.println(employee);
  }
}
```

***控制台输出***

*Employee Name: Ranga, Email: null, Phone Number: null, Title: Programmer Analyst, Employer: In28Minutes, Employee Grade: A, Salary: null*

##### Snippet-04 补全EmployeeRunner

让我们用setter方法设置非强制的属性。

***EmployeeRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class EmployeeRunner {
  public static void main(String[] args) {
    Employee employee = new Employee("Ranga", "Programmer Analyst", "In28Minutes", 			'A');
    employee.setEmail("in28minutes@gmail.com");
    employee.setPhoneNumber("123-456-7890");
    employee.setSalary(new BigDecimal("50000"));
    System.out.println(employee);
  }
}
```

**控制台输出**

*Employee Name: Ranga, Email: [in28minutes@gmail.com](mailto:in28minutes@gmail.com), Phone Number: 123-456-7890, Title: Programmer Analyst, Employer: In28Minutes, Employee Grade: A, Salary: 50000.0000*

##### Snippet-05 更新`Student`

让我们给`Student`类添加一个带两个参数的构造器。

***Student.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class Student extends Person {
  private String collegeName;
  private int year;

  public Student(String name, String collegeName) {
    super(name);
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

  public String toString() {
    return "Student : " + super.name() + ", College: " + collegeName;
  }
}
```

***StudentRunner.java***

```java
package com.in28minutes.oops.level2.inheritance;

public class StudentRunner {
  public static void main(String[] args)
    //Student student = new Student();
    Student student = new Student("Ranga", "IIT Bombay");
    System.out.println(student);
  }
}
```

***控制台输出***

*Student : Ranga, College : IIT Bombay*

### 12：多重继承，引用变量和`instanceof`

在有些编程语言中，允许多重继承。一个类能够直接继承两个或更多的类。

然而，Java不允许多继承。

##### Snippet-01 : Multiple Inheritance

```java
jshell> class Animal {
   ..>> }
| created class Animal
jshell> class Pet {
   ..>> }
| created class Pet

jshell> class Dog extends Animal, Pet {
   ..>> }
| Error:
| '{' expected
| class Dog extends Animal, Pet {
|_________________________^
jshell>
```

`class Dog extends Animal, Pet {}`抛出了错误。你不能扩展两个类。

#### 继承链

但是你可以使用继承链。

- 类`C`继承类`B`
- 类`B`继承类`A`

让我们看一小段代码

##### Snippet-02：继承链

`Dog`继承`Per`，`Pet`继承`Animal`。这就是所谓的继承层次的示例。

```java
jshell> class Animal {
   ..>> }
| created class Animal
jshell> class Pet extends Animal {
   ..>> public void groom() {
   ..>> System.out.println("Pet Groom");
   ..>> }
   ..>> }
| created class Pet_
jshell> class Dog extends Pet {
   ..>> }
| created class Dog
```

如果你想的话，你可以在脑海中想象：*`Dog` --> `Pet` --> `Animal` --> `Object`* （没错，`Object`类在Java中位于所有继承层次的顶部！）

`Dog dog = new Dog();`语句引发了构造器对继承层次的调用：`Dog()`调用了`Pet()`，`Pet()`调用了`Animal()`，`Amimal()`调用了`Object()`。

```java
jshell> Dog dog = new Dog();
dog ==> Dog@23a6e47f
```

`dog.toString()`表达式也对继承层次进行了遍历：因为`Dog.toString()`没有定义，编译器就查找`Pet.toString()`；因为`Pet.toString()`没有定义，编译器查找`Animal.toString()`；因为`Animal.toString()`没有定义，编译器查找`Object.toString()`，它始终作为Java中`Object`类的所有子类的默认实现提供。

```java
jshell> dog.toString();
$1 ==> "Dog@23a6e47f"
```

`dog.groom();`的调用也可以通过遍历继承层次来解决。

```java
jshell> dog.groom();
"Pet Groom"
```

`Pet pet = new Dog();` 这条语句真的很有意思。在Java中允许父类引用变量指向子类对象实例。

通过这样的引用，也允许调用方法，而且会正确调用。所以，`per.groom();`输出了"*`Pet Groom`*"。

但是不允许反向赋值。子类引用变量**不能**指向父类对象实例。所以`Dog dog = new Pet();`这条语句会造成编译出错。

```java
jshell> Pet pet = new Dog();
pet ==> Dog@22d37d54
jshell> pet.groom();
Pet Groom
```

```java
jshell> Dog dog = new Pet();
| Error:
| incompatible types: Pet cannot be converted to Dog
| Dog dog = new Pet();
|___________^-------^
```

`instanceof`操作符用来查看对象和类之间的关系。如果一个对象是所提供类或者子类的实例，返回`true`。

```java
jshell> pet instanceof Pet
$2 ==> true
jshell> pet instanceof Dog
$3 ==> true
```

如果对象和类没有关系，`instanceof`操作符会抛出错误。

```java
jshell> pet instanceof String
| Error:
| incompatible types: Pet cannot be converted to java.lang.String
| pet instanceof String
|_^-^
jshell> pet instanceof Animal
$4 ==> true
jshell> pet instanceof Object
$5 ==> true
```

如果这个对象是所提供类的父类的实例，`instanceof`操作符返回`false`。

```java
jshell> Animal animal = new Animal();
animal ==> Animal@3632be31
jshell> animal instanceof Pet
$6 ==> false
jshell> animal instanceof Dog
$7 ==> false
jshell> animal instanceof Object
$8 ==> true
jshell>
```

### 13：抽象类介绍

抽象类可以包含抽象方法。

抽象方法没有方法定义。

这里有一个典型类，你可以在这个类中创建方法，并且你可以创建这个类的实例。

```java
jshell> class Animal {
   ..>> public void bark() {
   ..>> System.out.println("Animal Bark");
   ..>> }
   ..>> }
| created class Animal
jshell> Animal animal = new Animal();
animal ==> Animal@335eadca
jshell> animal.bark();
Animal Bark
```

让我们看看如何创建一个抽象类：

```java
jshell> abstract class AbstractAnimal {
   ..>> abstract public void bark();
   ..>> }
| created class AbstractAnimal
```

语法很简单：在`class`前加上`abstract`关键字。

抽象类无法实例化。

```java
jshell> AbstractAnimal animal = new AbstractAnimal();
| Error:
| AbstractAnimal is abstract; cannot be instantiated.
| AbstractAnimal animal = new AbstractAnimal();
|^--------------------------------------------^
jshell>
```

但是，它可以子类化，通过创建它的继承层次。抽象类的子类（通常称为**具体类**）必须重载抽象类中的抽象方法。（译者注：如果子类没有实现抽象父类的所有抽象方法，这个子类也必须声明为抽象类。**只要有抽象方法，必须声明为抽象类**。）

```java
jshell> class Dog extends AbstractAnimal {
   ..>> }
| Error:
| Dog is not abstract and does not override abstract method bark() in AbstractAnimal
| class Dog extends AbstractAnimal {
|^----------------------------------...
jshell> class Dog extends AbstractAnimal {
   ..>> public void bark() {
   ..>> System.out.println("Bow Bow");
   ..>> }
   ..>> }
| created class Dog
jshell> Dog dog = new Dog();
dog ==> Dog@5a8e6209
jshell> dog.bark();
Bow Bow
```

### 14：抽象类 - 设计部分

为什么我们需要抽象类？

想象一下在家中准备一场盛宴，活动菜单上有几道菜。很显然，准备每道菜都有具体的工序。烹饪任何菜肴通常都需要遵循久经考验的食谱，它的准备工作可以归结为以下几个基本步骤：

- 准备原料
- 烹饪食谱
- 清理（会变乱！）

对于每道菜肴，这些步骤将有所不同，但是步骤的顺序保持不变。

##### Snippet-01：食谱层次

让我们使用抽象类来构建这个食谱。

***AbstractRecipe.java***

```java
package com.in28minutes.oops.level2;

public abstract class AbstractRecipe {
  public void execute() {
    prepareIngredients();
    cookRecipe();			
    cleanup();
  }

  abstract void prepareIngredients();
  abstract void cookRecipe();
  abstract void cleanup();
}
```

我们为每个步骤定义了抽象方法，并且创建了一个`execute`方法来调用它们。`execute`方法确保遵循方法调用的顺序。

你可以定义抽象方法的具体实现。

***CurryRecipe.java***

```java
package com.in28minutes.oops.level2;

public class CurryRecipe extends AbstractRecipe {
  public CurryRecipe() {
    System.out.println("[Curry Preparation Method]");
  }

  @Override
  void prepareIngredients() {
    System.out.println("Get Vegetables Cut and Ready");
    System.out.println("Get Spices Ready");
  }

  @Override
  void cookRecipe() {
    System.out.println("Steam And Fry Vegetables");
    System.out.println("Cook With Spices");
    System.out.println("Add Seasoning");
  }

  @Override
  void cleanup() {
    System.out.println("Discard unused Vegetables");
    System.out.println("Discard unused Spices");
  }
}
```

***RecipeRunner.java***

```java
package com.in28minutes.oops.level2;

public class RecipeRunner {
  public static void main(String[] args) {
    CurryRecipe curryRecipe = new CurryRecipe();
    curryRecipe.execute();
  }
}
```

***控制台输出***

*[Curry Preparation Method]*

*Get Vegetables Cut and Ready*

*Get Spices Ready*

*Steam And Fry Vegetables*

*Cook With Spices*

*Add Seasoning*

*Discard unused Vegetables*

*Discard unused Spices*

##### Snippet-01 说明

`CurryRecipe`类定义了在每一步中需要做什么。当我们调用`execute`方法时，就会按照顺序执行这些步骤。

##### Snippet-02：MicrowaveCurryRecipe

我们可以轻松地创建更多食谱。

***MicrowaveCurryRecipe.java***

```java
package com.in28minutes.oops.level2;

public class MicrowaveCurryRecipe extends AbstractRecipe {
  public MicrowaveCurryRecipe() {
    System.out.println("[Curry Microwave Method]");
  }

  @Override
  void prepareIngredients() {
    System.out.println("Get Vegetables Cut and Ready");
    System.out.println("Switch on Microwave");
  }

  @Override
  void cookRecipe() {
    System.out.println("Microwave Vegetables");
    System.out.println("Add Seasoning");
  }

  @Override
  void cleanup() {
    System.out.println("Switch Off Microwave");
    System.out.println("Discard unused Vegetables");
  }
}
```

***RecipeRunner.java***

```java
package com.in28minutes.oops.level2;

public class RecipeRunner {
  public static void main(String[] args) {
    MicrowaveCurryRecipe mcirowaveRecipe = new MicrowaveCurryRecipe();
    microwaveRecipe.execute();
  }
}
```

***控制台输出***

*[Curry Microwave Method]*

*Get Vegetables Cut and Ready*

*Switch on Microwave*

*Microwave Vegetables*

*Add Seasoning*

*Switch off Microwave*

*Discard unused Vegetables*

##### Snippet-02 说明

`MicrowaveCurryRecipe`类定义了在每一步中需要做什么。当我们调用`execute`方法时，就会按照顺序执行这些步骤。

#### 总结

这种模式称为`模板方法`模式。你可以在抽象类中定义这些步骤，将每一步的具体实现留给了子类。

### 15：抽象类 - 疑问

让我们看几个关于抽象类的FAQ。

没有抽象方法的类，也可以声明为抽象类。

```java
jshell> abstract class AbstractTest {
   ...>}
| creates abstract class AbstractTest
```

一个抽象类可以是另一个抽象类的子类，不覆盖任何父类的抽象方法。

```java
jshell> abstract class AbstractAlgorithm {
   ...> abstract void flowChart();
   ...> }
| creates abstract class AbstractAlgorithm
jshell> abstract class AlgorithmTypeOne extends AbstractAlgorithm {
   ...> }
| creates abstract class AlgorithmTypeOne
```

抽象类可以有成员变量。

```java
jshell> abstract class AbstractAlgorithm {
   ...> private int stepCount;
   ...> }
| replaced abstract class AbstractAlgorithm
```

抽象类可以非抽象方法。

```java
jshell> abstract class AbstractAlgorithm {
   ...> private int stepCount;
   ...> public int getStepCount() {
   ...> return stepCount;
   ...> }
   ...> }
| replaced abstract class AbstractAlgorithm
jshell>
```

### 16：接口介绍
“游戏机”对你来说意味着什么？

有按钮或其他控件的设备，可以让我们来打游戏。

它上面有哪些常见的按钮？

- 方向键 - 上 下 左 右
- 选择键
- 等等

游戏机提供了一个接口来玩游戏。

谁提供了按钮被单击时所发生事件的实现？游戏制作者 - 例如，马里奥游戏或国际象棋游戏的制作者。

如何在Java程序中表示它？

***GamingConsole.java***

```java
package com.in28minutes.oops.level2.interfaces;

public interface GamingConsole {
  public void up();
  public void down();
  public void left();
  public void right();
}
```

`GamingConsole`接口包含了没有定义的方法。

是提供了它们的实现？

有请`MarioGame`。

***MarioGame.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class MarioGame implements GamingConsole {
  @Override
  public void up() {
    System.out.println("Jump");
  }

  @Override
  public void down() {
  System.out.println("Go into a hole");
  }

  @Override
  public void left() {
  }

  @Override
  public void right() {
    System.out.println("Go Forward");
  }
}
```

`MarioGame`提供了所有在`GamingConsole`接口中声明方法的定义。语法很简单。`class MarioGame implements GamingConsole`，然后实现所有方法。

让我们看看如何运行这些游戏。

***GameRunner.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class GameRunner {
  public static void main(String[] args) {
    MarioGame game = new MarioGame();
    game.up();
    game.down();
    game.left();
    game.right();
  }
}
```

***控制台输出***

*Jump*

*Go into a hole*

*Go forward*

##### Snippet-01 说明

接口的最主要的优点是让实现者执行一个约定。

##### Snippet-02：接口的代码复用

让我们来看另外一个例子 - `ChessGame`。

***ChessGame.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class ChessGame implements GamingConsole {

  @Override
  public void up() {
    System.out.println("Move Piece Up");
  }

  @Override
  public void down() {
    System.out.println("Move Piece Down");
  }

  @Override
  public void left() {
    System.out.println("Move Piece Left");
  }

  @Override
  public void right() {
    System.out.println("Move Piece Right");
  }
}
```

执行这段代码很简单。你所要做的就是注释掉`MarioGame game = new MarioGame();`然后用`ChessGame`的实现去代替它。

***GameRunner.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class GameRunner {
  public static void main(String[] args) {
    //MarioGame game = new MarioGame();
    ChessGame game = new ChessGame();
    game.up();
    game.down();
    game.left();
    game.right();
  }
}
```

***控制台输出***

*Move Piece Up*

*Move Piece Down*

*Move Piece Left*

*Move Piece Right*

##### Snippet-2 说明

在同一个`GameRunner`类中，如果我们想要实例化一个`ChessGame`对象来替换`MarioGame`，其余的代码都不需要修改。这是因为`MarioGame`和`ChessGame`都实现了同样的接口，`GamingConsole`。

#### 使用接口作为引用变量类型

`GamingConsole`是一个接口。`MarioGame`和`ChessGame`是它的实现。

让我们试试这行代码 - `GamingConsole game = new ChessGame();`

***GameRunner.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class GameRunner {
  public static void main(String[] args) {
    GamingConsole game = new ChessGame();
    game.up();
    game.down();
    game.left();
    game.right();
  }
}
```

***控制台输出***

*Move Piece Up*

*Move Piece Down*

*Move Piece Left*

*Move Piece Right*

**说明**

`GamingConsole game = new ChessGame();` - 你能将一个接口的实现存到这个接口的引用变量类型中。

这样做有什么用呢？

让我们看下一个例子：

##### Snippet-4：GameRunner Version 4

***GameRunner.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class GameRunner {
  public static void main(String[] args) {
    GamingConsole game = new MarioGame();
    game.up();
    game.down();
    game.left();
    game.right();
  }
}
```

***控制台输出***

*Jump*

*Go into a hole*

*Go forward*

##### Snippet-04 说明

你能用`GamingConsole game = new MarioGame()`替换`GamingConsole game = new ChessGame()`。并且程序运行了`MarioGame`。是不是很棒？

### 17：用接口来设计APIs

思考一下，一个软件开发项目需要编写相当巨大而且复杂的应用。项目团队（团队A）决定外包这个项目的一部分给外部团队（团队B）。假设这个外部团队需要实现一个非常复杂的算法来完成特定的任务，并且需要与应用程序的其余部分进行交互。应用程序的两个部分的开发工作需要同时进行。

假设用一个简单的方法实现这个算法逻辑：

`int complexAlgorithm(int number1, int number2);`

我们如何确保两个团队所做的工作保持兼容?

他们从定义接口开始。

***ComplexAlgorithm.java***

```java
package com.in28minutes.oops.level2.interfaces;

public interface ComplexAlgorithm {
  int complexAlgorithm(int number1, int number2);
}
```

现在两支团队可以继续了。团队A可以为这个接口创建一个占位`OneComplexAlgorithm`，然后开始他们的项目。

***OneComplexAlgorithm.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class OneComplexAlgorithm implements ComplexAlgorithm {
  public int complexAlgorithm(int number1, int number2) {
    return number1 + number2;
  }
}
```

团队B花时间实现真正的算法。

***ActualComplexAlgorithm.java***

```java
package com.in28minutes.oops.level2.interfaces;

public class ActualComplexAlgorithm implements ComplexAlgorithm {
  public int complexAlgorithm(int number1, int number2) {
    //Your complex implementation will be present here..
    return number1 * number2;
  }
}
```

(译者注：原文中`OneComplexAlgorithm`和`ActualComplexAlgorithm`中没有`implements ComplexAlgorithm`这部分，应该是作者遗漏了)

### 18：接口 - 疑问与有趣的事实

让我们看几个例子来更好地了解接口。

一个接口可以被另外的接口扩展。我们可以构建一个只包含接口的继承层次。

```java
jshell> interface InterfaceOne {
   ...> void methodOne();
   ...> }
| created interface InterfaceOne

jshell> interface InterfaceTwo extends InterfaceOne {
   ...> void methodTwo();
   ...> }
| created interface InterfaceTwo
```

实现一个接口，应该实现这个接口所有的方法，包括父类接口中的方法。

```java
jshell> class Implementation implements InterfaceTwo {
   ...>}
| Error:
| Implementation is not abstract and does not implement abstract method methodTwo() of 	InterfaceTwo
| class Implementation implements InterfaceTwo {
|^---------------------------------------------...

jshell> public class Implementation implements InterfaceTwo {
   ...> public void methodTwo() {}
   ...> }
| Error:
| Implementation is not abstract and does not implement abstract method methodOne() of 	InterfaceOne
| class Implementation implements InterfaceTwo {
|^---------------------------------------------...

jshell> public class Implementation implements InterfaceTwo {
   ...> public void methodTwo() {}
   ...> public void methodOne() {}
   ...> }
| created class Implementation
```

如果一个类声明为抽象类，它可以不用实现所有的接口方法。

```java
jshell> public abstract class AbstractImplementation implements InterfaceTwo {
   ...> public void methodOne() {}
   ...> }
| created class AbstractImplementation
```

接口不能拥有成员变量。一个接口只能声明**常量**。

```java
jshell> interface InterfaceThree {
   ...> int test;
   ...> }
| Error:
| = expected 
| int test;
|_________^

jshell> interface InterfaceThree {
   ...> int test = 5;
   ...> }
| created interface InterfaceThree
```

从Java SE 8开始，接口可以为它的方法提供一个默认实现。通过在方法签名中包含`default`关键字，并在方法的定义中提供一个主体来实现。

```java
jshell> interface InterfaceFour {
   ...> public default void print() {
   ...> System.out.println("default print");
   ...> }
   ...> }
| created interface InterfaceFour

jshell> class TestPrint implements InterfaceFour {
   ...> }
| created class TestPrint


jshell> TestPrint testPrint = new TestPrint();
testPrint ==> TestPrint@6ebc05a6
jshell> testPrint.print();
default print
```

接口的实现可以覆盖这个默认的方法实现。

```java
jshell> class ParticularPrint implements InterfaceFour {
   ...> public void print() {
   ...> System.out.println("particular print");
   ...> }
   ...> }
| created class ParticularPrint
```

```java
jshell> ParticularPrint particularPrint = new ParticularPrint();
particularPrint ==> ParticularPrint@5fad14c4
jshell> particularPrint.print();
particular print
jshell>
```

不能将接口中的方法的访问修饰符声明为`private`。但是，抽象类可以将方法声明为`private`。

#### 为什么我们需要默认方法

让我们考虑一下有是哪个实现的`Provider`接口。

```java
public interface Provider {
  public void doSomething();
}

public class ImplementorOne implements Provider {
  @Override
  public void doSomething() {
    System.out.println("Do One");
  }
}

public class ImplementorTwo implements Provider {
  @Override
  public void doSomething() {
    System.out.println("Do Two");
  }
}

public class ImplementorThree implements Provider {
  @Override`
  public void doSomething() {
    System.out.println("Do Three");
  }
}
```

如果在这个接口中新增一个方法会发生什么？

```java
public interface Provider {
  public void doSomething();
  public void doMore();
}
```

编译出错！所有的实现该接口的类`ImplementationOne`，`ImplementationTwo`和`ImplementationThree`必须实现`doMore()`方法。

另一种选择：为`doMore`提供一个默认实现。

```java
public interface Provider {
  public void doSomething();

  public default void doMore(){
    System.out.println("Do More");
  }
}
```

不需要立即修改其他代码，而且具体实现接口的类可以在需要的时候覆盖默认方法。

这在构建和扩展框架时特别有用。当你向框架接口中添加新方法时，并不会破坏用户的接口。

### 19：抽象类与接口：比较

抽象类与接口除了它们有很相似的语法外，有很大的区别。

什么时候在应用程序中使用它们?

#### 接口

接口是一种**约定**。

接口主要用于当你有两个软件组件需要相互通信时，这时候需要建立一个约定。

回想下面的例子：`ComplexAlgorithm`定义了两个团队都涉及到的接口。

```java
package com.in28minutes.oops.level2.interfaces;
public interface ComplexAlgorithm {
  int complexAlgorithm(int number1, int number2);
}
```

#### 抽象类

抽象类主要用于通过创建父类泛化行为。

回顾一下我们之前讨论的例子：

```java
public abstract class AbstractRecipe {
  public void execute() {
    prepareIngredients();
    cookRecipe();
    cleanup();
  }

  abstract void prepareIngredients();
  abstract void cookRecipe();
  abstract void cleanup();
}
```

#### 语法比较

这里有一重要的语法差异：

- 不能将接口中的方法的访问修饰符声明为`private`。但是，抽象类可以将方法声明为`private`。
- 接口不能声明成员变量，而抽象类可以声明成员变量。
- 类或者抽象类可以实现多个接口。但是接口只能继承一个接口，并且类或者抽象类只能继承一个类或者一个抽象类。
