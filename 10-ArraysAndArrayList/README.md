# 数组和数组列表
我们将会通过下面的练习来学习Java中最常用的数据结构 - 数组和数组列表。
我们想创建一个学生成绩单的类，它有以下功能：
```java
Student student - new Student(name, list-of-marks);
int number = student.getNumberOfmarks();
int sum = student.getTotalSumOfMarks();
int maximumMark = student.getMaximumMark();
int minimumMark = student.getMinimumMark();
BigDecimal average = student.getAverageMarks();
student.addMark(35);
student.removeMarkAtIndex(5);
```

像数组和数组列表这样的数据结构允许你存储多个相同类型的对象。我们称之为聚合。

### 01：数组的必要性

我们先了解以下为什么需要数组。
思考下面的示例。我们创建了3个`mark`变量，然后求它们的和。

```java
jshell> int mark1;
mark1 ==> 0
jshell> mark1 = 100;
mark1 ==> 10
jshell> int mark2 = 75;
mark2 ==> 75
jshell> int mark3 = 60;
mark3 ==> 60
jshell> int sum = mark1 + mark2 + mark3;
sum ==> 235
jshell> int mark4 = 56;
mark4 ==> 56
jshell> sum = mark1 + mark2 + mark3 + mark4;
sum ==> 291
jshell>
```

如果`mark1`，`mark2`和`mark3`中又新增了额外的`mark4`，那计算`sum`的代码就要改写。

所有这些`mark`变量都是相似的。把这些`mark`值都存在一个变量里怎么样？

让我们创建一个数组 - `marks`

```java
jshell> int[] marks = {75, 60, 56};
marks ==> int[3]{ 75,60,56 }
```

在上面的示例代码中

- `marks`是一个数组
- `marks`存了多个`int`类型的值
- `marks`数组长度为3

在数组中，下标从0到数组长度-1.在上面的示例代码中，下标范围是0到2。

你可以用下标找到数组中的指定元素。用下标操作符（`[]`）完成。表达式`marks[0]`表示数组`marks`的第一个元素，它的下标为`0`。

```java
jshell> marks[0]
$20 ==> 75

jshell> marks[1]
$21 ==> 60

jshell> marks[2]
$22 ==> 56
```

如果要求`marks`数组所有元素值的和，该怎么写代码？

```java
jshell> int sum = 0;
sum ==> 0
jshell> for(int mark:marks) {
   ..>> sum = sum + mark;
   ..>> }
jshell> sum
sum ==> 191
jshell>
```

上面的结构叫做增强的`for`循环。

`mark`是循环控制变量。它的类型需要和数组元素类型`int`匹配。

上面使用的`for`循环和`marks`数组的元素数量无关。

### 02：存储和访问数组值

在这一节中，我们会更深入地研究数组。

数组能够存0个及以上的元素。

```java
jshell> int[] marks = {1, 2, 3 };
marks ==> int[3]{ 1,2,3 }
jshell> int[] marks = {1, 2, 3, 4, 5};
marks ==> int[5]{ 1,2,3,4,5 }
jshell> int[] marks = {1};
marks ==> int[1]{ 1 }
jshell> int[] marks = {};
marks ==> int[0]{  }
```

数组同样也能通过`new`操作符创建。但是你必须指定数组的大小。

```java
jshell> int[] marks2 = new int[5];
marks2 ==> int[5]{ 0,0,0,0,0 }
```

你可以通过数组下标赋值。

`marks2[0] = 10`语句让`marks2`数组的第一个位置存储了10这个值。

```java
jshell> marks2[0]
$1 ==> 0
jshell> marks2[0] = 10;
$2 ==> 10
jshell> marks2[0]
$3 ==> 10
jshell>
```

下面的代码展示了更多的例子。

```java
jshell> int[] marks2 = new int[5];
marks2 ==> int[5]{ 0,0,0,0,0 }
jshell> marks2[0] = 1;
$1 ==> 1
jshell> marks2[1] = 2;
$2 ==> 2
jshell> marks2[2] = 3;
$3 ==> 3
jshell> marks2[3] = 4;
$4 ==> 4
jshell> marks2[4] = 5;
$5 ==> 5
jshell> marks2
marks2 ==> int[5]{ 1,2,3,4,5 }
```

`length`表示数组中元素的个数。

```java
jshell> marks2.length
$6 ==> 5
jshell> int marks3 = {};
marks3 ==> int[0]{  }
jshell> marks3.length
$7 ==> 0
```

#### Classromm Exercise CE-AA-01

1. 写一个程序，创建一个存了8个`int`类型值的数组`marks`，然后用`for`循环遍历`marks`数组，并打印它的元素值。

提示：使用`marks.length`属性

#### Solution To CE-AA-01

```java
jshell> int[] marks = {1, 2, 3, 4, 5, 6, 7, 8};
marks ==> int[8]{ 1,2,3,4,5,6,7,8 }
jshell> marks.length
$1 ==> 8
jshell> for(int i=0; i < marks.length; i++) {
   ..>> System.out.println(marks[i]);
   ..>> }
1
2
3
4
5
6
7
8
jshell>
```

### 03：数组初始化，数据类型和异常

下面的代码块说明了不同类型的数组如何初始化。

总结 - int - 0，double - 0.0, boolean - false, 任何对象 - null

```java
jshell> int[] marks = new int[5];
marks ==> int[5]{ 0,0,0,0,0 }
jshell> double[] values = new double[5];
values ==> double[5]{ 0.0,0.0,0.0,0.0,0.0 }
jshell> boolean[] tests = new boolean[5];
tests ==> boolean[5]{ false,false,false,false,false }
jshell> class Person {
   ..>>}
| created class Person
jshell> Person[] persons = new Person[5];
persons ==> Person[5]{ null,null,null,null,null }
jshell>
```

让我们看几个数组声明时会改变的部分。

需重点记忆的几个知识点

- 数组定义的声明部分不能包含数组的大小
- 数组定义的赋值部分必须包含数组的大小
- 数组的所有元素必须是相同的类型

```java
jshell> int[5] marks2;
| Error:
| ']' expected
| int[5] marks2;
|____^
jshell> int[] marks2 = new int[];
| Error:
| array dimension missing
| int[] marks2 = new int[];
|____________^========^
jshell> int[] marks2 = new int[5];
marks2 ==> int[5]{ 0,0,0,0,0 }
jshell> marks2[6]
| java.lang.ArrayIndexOutOfBoundsException thrown : 6
| at (#54:1)
jshell> int[] marks3 = {1, 2, 3, 4.0};
| Error:
| incompatible types: possible lossy conversion from double to int
| int[] marks3 = {1, 2, 3, 4.0};
|__________________________^-^ 
jshell>
```

数组的名字是一个引用变量，它存储着在堆里创建这个数组的内存地址。

```java
jshell> int[] marks4 = {1, 2, 3, 4, 5};
marks4 ==> int[5]{ 1,2,3,4,5 }
jshell> System.out.println(marks4);
I@6c49835d
```

内置的`Arrays.toString`方法可以打印数组的所有元素。

### 04：数组的实用程序

看几个例子

- 遍历数组
- 批量修改数组元素
- 数组比较
- 数组排序

##### Snippet-01：数组遍历

使用增强的`for`循环简单直观。

```java
jshell> int[] marks = {100, 99, 95, 96, 100};
marks ==> int[5]{ 100,99,95,96,100 }
jshell> for(int mark:marks) {
..>> System.out.println(mark);
..>> }
100
99
95
96
100
jshell> for(int i=0; i < marks.length; i++) {
..>> System.out.println(marks[i]);
..>> }
100
99
95
96
100
jshell>
```

##### Snippet-02：填充 & 比较数组

`Array.fill`方法用一个指定的值填充整个数组。

```java
jshell> int[] marks = new int[5];
marks ==> int[5]{ 0,0,0,0,0 }
jshell> Arrays.fill(marks, 100);
jshell> marks
marks ==> int[5]{ 100,100,100,100,100 }
```

`Array.equals`比较两个给定的数组，只在下面两种情况下返回布尔值为`true`

- 两个数组长度相同
- 所有索引，每个对应索引的元素都是相等的

```java
jshell> int[] array1 = {1, 2, 3};
array1 ==> int[3]{ 1,2,3 }
jshell> int[] array2 = {1, 2, 3};
array2 ==> int[3]{ 1,2,3 }

jshell> Arrays.equals(array1, array2);
$1 ==> true

jshell> int[] array3 = {3, 2, 3};
array3 ==> int[3]{ 3,2,3 }
jshell> Arrays.equals(array1, array3);
$2 ==> false

jshell> int[] array4 = {1, 2};
array4 ==> int[2]{ 1,2 }
jshell> Arrays.equals(array1, array4);
$3 ==> false
```

`Array.sort`通过每次比较两个元素进行位置排序。

```java
jshell> Arrays.sort(array3);
jshell> array3
array3 ==> int[3]{ 2,3,3 }
jshell>
```

### 05：Classroom Exercise CE-AA-02

#### 练习

我们已经掌握了Java数组和它内置的实用方法，现在来解决本节开始的挑战。

```java
Student student - new Student(name, list-of-marks);
int number = student.getNumberOfmarks();
int sum = student.getTotalSumOfMarks();
int maximumMark = student.getMaximumMark();
int minimumMark = student.getMinimumMark();
BigDecimal average = student.getAverageMarks();
```

我们可以把`list-of-marks`当做一个数组。

#### CE-AA-02 解答

***StudentRunner.java***

```java
package com.in28minutes.arrays;

public class StudentRunner {
  public static void main(String[] args) {
    int[] marks = {99, 98, 100};
    Student student = new Student("Ranga", marks);

    int number = student.getNumberOfmarks();		
    System.out.println("Number of marks : " + number);	
    int sum = student.getTotalSumOfMarks();
    System.out.println("Sum of marks : " + sum);

    int maximumMark = student.getMaximumMark();
    System.out.println("Maximum of marks : " + maximumMark);
    int minimumMark = student.getMinimumMark();
    System.out.println("Minimum of marks : " + minimumMark);

    BigDecimal average = student.getAverageMarks();
    System.out.println("Average of marks : " + average);
    student.addMark(35);
    student.removeMarkAtIndex(5);
  }
}
```

***Student.java***

```java
package com.in28minutes.arrays;
import java.math.BigDecimal;

public class Student {
  private String name;
  private int[] marks;

  public Student(String name, int[] marks) {
    this.name = name;
    this.marks = marks;
  }

  public int getNumberOfMarks() {
    return marks.length;
  }

  public int getTotalSumOfMarks() {
    int sum = 0;
    for(int mark:marks) {
      sum += mark;
    }
    return sum;
  }

  public BigDecimal getAverageOfMarks() {
    int sum = getTotalSumOfMarks();
    BigDecimal average = new BigDecimal(sum).divide(new 					  		BigDecimal(marks.length), 3, RoundingMode.UP);
  }

  public int getMaximumMark() {
    int max = Integer.MIN_VALUE;
    for(int mark:marks) {
      if(mark > max) {
        max = mark;				
      }
    }
    return max;
  }

  public int getMinimumMark() {	
    int min = Integer.MAX_VALUE;
    for(int mark:marks) {
      if(mark < min) {
        min = mark;
      }
    }
    return min;
  }
}
```

### 06：可变参数 - 基础

如果你想要写一个能够接受可变数量参数的方法，该怎么办？

看一个例子。最关键的部分时参数`int... values`。

```java
jshell> class Something {
   ..>> public void doSomething(int... values) {
   ..>> System.out.println(Arrays.toString(values));
   ..>> }
   ..>> };
| created class Something
```

典型的参数是`int values`。这样允许我们给方法传递一个参数。

在`int... values`里的3个点`...`和上面有什么区别。

```java
jshell> Something thing = new Something();
thing ==> Something@2e465f6a
jshell> thing.doSomething(1);
[1]
jshell> thing.doSomething(1, 2);
[1, 2]
jshell> thing.doSomething(1, 2, 3);
[1, 2, 3]
jshell>
```

你可以看到`doSomething`可以用一个，两个和三个参数调用。

看另外一个例子：

```java
jshell> void sum(int... values) {
   ..>>   int sum = 0;
   ..>>   for(value: values) {
   ..>>     sum += value;
   ..>>   }
   ..>>   System.out.println(sum);
   ..>> }
| created method sum(int...)
```

我们创建了一个可变参数的`sum`方法。看看怎么使用它。

```java
jshell> sum(1, 2)
3
jshell> sum(1, 2, 3)
6
jshell> sum(1, 2, 3, 4)
1
jshell> sum(1, 2, 3, 4, 5, 6)
21
jshell>
```

在这一节中，我们初步了解了可变参数。可变参数允许我们向方法传递可变数量的参数。

### 07：Student 类的可变参数方法

让我们为`Student`类添加几个可接受可变参数的方法。

***Student.java***

```java
package com.in28minutes.arrays;
import java.math.BigDecimal;

public class Student {
  private String name;
  private int[] marks;

  public Student(String name, int...  marks) {
    this.name = name;
    this.marks = marks;
  }

  public int getNumberOfMarks() {
    return marks.length;
  }

  public int getTotalSumOfMarks() {
    int sum = 0;
    for(int mark:marks) {
      sum += mark;
    }
    return sum;
  }

  public BigDecimal getAverageOfMarks() {
    int sum = getTotalSumOfMarks();
    BigDecimal average = new BigDecimal(sum).divide(new BigDecimal(marks.length), 3, RoundingMode.UP);
  }

  public int getMaximumMark() {
    int max = Integer.MIN_VALUE;
    for(int mark:marks) {
      if(mark > max) {
        max = mark;
      }
    }
    return max;
  }

  public int getMinimumMark() {
    int min = Integer.MAX_VALUE;
    for(int mark:marks) {
      if(mark < min) {
        min = mark;
      }
    }
    return min;
  }
}
```

***StudentRunner.java***

```java
package com.in28minutes.arrays;
public class StudentRunner {
  public static void main(String[] args) {
    //int[] marks = {99, 98, 100};
    Student student = new Student("Ranga", 97, 98, 100);

    int number = student.getNumberOfmarks();
    System.out.println("Number of marks : " + number);
    int sum = student.getTotalSumOfMarks();
    System.out.println("Sum of marks : " + sum);

    int maximumMark = student.getMaximumMark();
    System.out.println("Maximum of marks : " + maximumMark);
    int minimumMark = student.getMinimumMark();
    System.out.println("Minimum of marks : " + minimumMark);
    BigDecimal average = student.getAverageMarks();
    System.out.println("Average of marks : " + average);

    student.addMark(35);
    student.removeMarkAtIndex(5);
  }
}
```

#### 小提示

可变参数列表必须在传递给方法所有参数列表的最后。下面的方法定义不会编译通过：

```java
void process(int... values, String name) {

}
```

### 08：数组 - 问题和练习

让我们来看一下数组的几个问题和练习。

当创建对象数组时，对象最后保存的是对创建的对象的引用。

```java
jshell> class Person {
   ..>> }
| created class Person
jshell> Person[] persons = new Person[5];
persons ==> Person[5]{ null,null,null,null,null }
```

我们可以将新的Person对象分配给数组的不同元素。

```java
jshell> persons[1] = new Person();
$1 ==> Person@394e1a0f
jshell> persons
persons ==> Person[5]{ null,Person@394e1a0f,null,null,null }
jshell> persons[0] = new Person();
$2 ==> Person@1e965684
jshell> persons
persons ==> Person[5]{ Person@1e965684,Person@394e1a0f, null,null,null }
```

你同样也可以在创建数组时初始化值。

```java
jshell> Person[] persons2 = {new Person(), new Person()};
persons2 ==> Person[2]{ Person@3b088d51, Person@1786dec2 }
```

下面是你如何初始化一个`String`类型的数组。

```java
jshell> String[] textValues = {"Apple", "Ball", "Cat"};
textValues ==> String[2]{ "Apple","Ball","Cat" }
jshell>
```

#### Classroom Exercise CE-AA-03

#### 练习

1. 创建一个`String`数组，由每周的日期组成：

   `Sunday`，`Monday`，`Tuesday`，`Wednesday`，`Thursday`，`Friday`，`Saturday`。

2. 找到字母个数最多的那一天。

3. 倒着打印一周的每一天。

#### CE-AA-03 解答

***WeekRunner.java***

```java
package com.in28minutes.arrays;

public class StringRunner {

	public static void main(String[] args) {

		String[] daysOfWeek = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };

		String dayWithMostCharacters = "";

		for (String day : daysOfWeek) {
			if (day.length() > dayWithMostCharacters.length()) {
				dayWithMostCharacters = day;
			}
		}

		System.out.println("Day with Most number of characters " + dayWithMostCharacters);

		for (int i = daysOfWeek.length - 1; i >= 0; i--) {
			System.out.println(daysOfWeek[i]);
		}

	}

}
```

### 09：数组的一些问题

看一下我们对于之前挑战的实现。

我们已经实现了大部分功能，除了`addMark()`和`removeMarkAtIndex()`方法

```java
Student student = new Student(name, <list-of-marks>);
int number = student.getNumberOfmarks();
int sum = student.getTotalSumOfMarks();
int maximumMark = student.getMaximumMark();
int minimumMark = student.getMinimumMark();
BigDecimal average = student.getAverageMarks();
student.addMark(35);	
student.removeMarkAtIndex(5);
```

我们想要对一个数组新增和移除元素。我们能实现吗？

在编译时，定义一个数组的大小是固定的。这意味着一旦我们定义了一个数组，比如：

`String[] textValues = {"Apple", "Ball", "Cat"};`

`textValues`数组的大小固定为3。你可以改变数组中的值。但是大小不能改变。

如何在数组中新增元素？

其中一个选择是

- 创建一个带有几个额外元素空间的新数组，用于插入新增元素
- 把已有数组元素拷贝到新数组的起始位置
- 在这个数组的尾部增加额外的元素

如果需要从数组中删除元素：

- 新建一个尺寸相对较小的数组
- 将现有的数组元素(不包括要删除的元素)复制到新数组的开头

```java
jshell> int[] marks = {12, 34, 45};
marks ==> int[3] { 12, 34, 45 }

jshell> int[] newMarks = new int[marks.length+1];
newMarks ==> int[4] { 0, 0, 0, 0 }

jshell> System.arraycopy(marks, 0, newMarks, 0, marks.length);

jshell> newMarks
newMarks ==> int[4] { 12, 34, 45, 0 }

jshell> newMarks[3] = 100
$27 ==> 100

jshell> newMarks
newMarks ==> int[4] { 12, 34, 45, 100 }
```

显然，这样非常麻烦。我们怎么解决它？

### 10：ArrayList 介绍

`ArrayList`比数组更加动态。它提供了增加和删除元素的操作。

让我们先创建一个`ArrayList`，然后添加几个值。

```java
jshell> ArrayList arrayList = new ArrayList();
arrayList ==> []
jshell> arrayList.add("Apple");
| Warning:
| unchecked call to add(E) as a member of the raw type java.util.ArrayList
| arrayList.add("Apple");
|_^---------------------^
$1 ==> true
jshell> arrayList.add("Ball");
| Warning:
| unchecked call to add(E) as a member of the raw type java.util.ArrayList
| arrayList.add("Ball");
|_^---------------------^
$2 ==> true
jshell> arrayList.add("Cat");
| Warning:
| unchecked call to add(E) as a member of the raw type java.util.ArrayList
| arrayList.add("Cat");
|_^---------------------^
$3 ==> true
jshell> arrayList
arrayList ==> ["Apple", "Ball", "Cat"]
```

你可以使用`remove`方法删除值。

```java
jshell> arrayList.remove("Cat");
$4 ==> true
jshell> arrayList
arrayList ==> ["Apple", "Ball"]
```

`ArrayList`的示例`arrayList`能够用来存储几乎任何类型的对象，甚至是基本数据类型。同样，也可以是不同的类型。

> 显示的警告消息提示程序员不要这样做。

```java
jshell> arrayList.add(1);
| Warning:
| unchecked call to add(E) as a member of the raw type java.util.ArrayList
| arrayList.add(1);
|_^---------------------^
$3 ==> true
jshell> arrayList
arrayList ==> ["Apple", "Ball", 1]
jshell>
```

假设我们只想在`ArrayList`中存`String`类型的值。我们该怎么办？

我们可以指定`ArrayList`可以容纳的元素的类型。

```java
jshell> ArrayList<String> items = new ArrayList<String>();
items ==> []
```

在上面的代码块中，我们创建了一个只能存储`String`类型值的`ArrayList`。

```java
jshell> items.add("Apple");
$1 ==> true
jshell> items
items ==> ["Apple"]
jshell> items.add(1);
| Error
| no suitable method found for add(int)
|...
jshell> items.add("Ball");
$2 ==> true
jshell> items.add("Cat");
$3 ==> true
jshell> items
items ==> ["Apple", "Ball", "Cat"]
```

其余的操作和普通的`ArrayList`类似。

```java
jshell> items.remove("Cat");
$4 ==> true
jshell> items
items ==> ["Apple", "Ball"]
jshell> items.remove(0);
$5 ==> "Apple"
jshell> items
items ==> ["Ball"]
jshell>
```

### 11：使用ArrayList重构Student类

现在再看一次之前的`Student`类练习。这一次我们使用`ArrayList`

```java
Student student = new Student(name, <list-of-marks>);
int number = student.getNumberOfmarks();
int sum = student.getTotalSumOfMarks();
int maximumMark = student.getMaximumMark();
int minimumMark = student.getMinimumMark();	
BigDecimal average = student.getAverageMarks();
```

##### Snippet-01：重构Student类

***StudentRunner.java***

```java
package com.in28minutes.arrays;

public class StudentRunner {
  public static void main(String[] args) {
    Student student = new Student("Ranga", 97, 98, 100);
    int number = student.getNumberOfmarks();			
    System.out.println("Number of marks : " + number);
    int sum = student.getTotalSumOfMarks();
    System.out.println("Sum of marks : " + sum);

    int maximumMark = student.getMaximumMark();
    System.out.println("Maximum of marks : " + maximumMark);
    int minimumMark = student.getMinimumMark();
    System.out.println("Minimum of marks : " + minimumMark);

    BigDecimal average = student.getAverageMarks();
    System.out.println("Average of marks : " + average);
    System.out.println(student);
  }	
}
```

***Student.java***

```java
package com.in28minutes.arrays;
import java.math.BigDecimal;
import java.math.RoundingMode;
import java.util.ArrayList;

public class Student {
  private String name;
  private ArrayList<Integer>  marks = new ArrayList<Integer>();

  public Student(String name, int...  marks) {
    this.name = name;
    for(int mark: marks) {
      this.marks.add(mark);
    }
  }

  public int getNumberOfMarks() {
    return marks.size();
  }

  public int getTotalSumOfMarks() {
    int sum = 0;
    for(int mark:marks) {
      sum += mark;
    }			
    return sum;
  }

  public BigDecimal getAverageOfMarks() {
    int sum = getTotalSumOfMarks();
    BigDecimal average = new BigDecimal(sum).divide(new BigDecimal(marks.size()), 3, RoundingMode.UP);
  }

  public int getMaximumMark() {
    return Collections.max(marks);
  }

  public int getMinimumMark() {
    return Collections.min(marks);
  }

  public String toString() {
    return name + marks;
  }
}
```

`ArrayList`和数组一样，也能使用增强的`for`循环，

`Collections.max()`和`Collections.min()`方法能找到数组列表中的最大值和最小值。

### 12：进一步加强Student类

现在给`Student`类添加新增分数和删除分数的功能。

```java
package com.in28minutes.arrays;

public class StudentRunner {
  public static void main(String[] args) {
    Student student = new Student("Ranga", 97, 98, 100);
    int number = student.getNumberOfMarks();
    System.out.println("Number of marks : " + number);
    int sum = student.getTotalSumOfMarks();			
    System.out.println("Sum of marks : " + sum);

    int maximumMark = student.getMaximumMark();
    System.out.println("Maximum of marks : " + maximumMark);
    int minimumMark = student.getMinimumMark();
    System.out.println("Minimum of marks : " + minimumMark);

    BigDecimal average = student.getAverageOfMarks();
    System.out.println("Average of marks : " + average);
    System.out.println(student);

    student.addMark(35);			
    System.out.println(student);
    student.removeMarkAtIndex(1);
    System.out.println(student);
  }
}
```

***Student.java***

```java
package com.in28minutes.arrays;
import java.math.BigDecimal;
import java.math.RoundingMode;
import java.util.ArrayList;

public class Student {
  private String name;
  private ArrayList<Integer>  marks = new ArrayList<Integer>();

  public Student(String name, int...  marks) {
    this.name = name;
    for(int mark: marks) {
      this.marks.add(mark);
    }
  }

  public int getNumberOfMarks() {
    return marks.size();
  }

  public int getTotalSumOfMarks() {
    int sum = 0;
    for(int mark:marks) {
      sum += mark;
    }		
    return sum;
  }

  public BigDecimal getAverageOfMarks() {
    int sum = getTotalSumOfMarks();
    BigDecimal average = new BigDecimal(sum).divide(new BigDecimal(marks.size()), 3, RoundingMode.UP);
    return average;
  }

  public int getMaximumMark() {
    return Collections.max(marks);
  }

  public int getMinimumMark() {
    return Collections.min(marks);
  }

  public String toString() {
    return name + marks;
  }

  public void addMark(int mark) {
    marks.add(mark);
  }

  public void removeMarkAtIndex(int index) {
    marks.remove(index);
  }
}
```

***控制台输出***（译者注：原文输出结果有误）

*Number of marks : 3*

*Sum of marks : 295*

Average of marks : 98.334

*Maximum of marks : 100*

*Minimum of marks : 97*

*Ranga[97,98,100]*

*Ranga[97,98,100,35]*

*Ranga[97,100,35]*

