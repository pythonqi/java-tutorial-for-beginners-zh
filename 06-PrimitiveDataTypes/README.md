# 基本数据类型

在前面，我们研究了基本的Java类型(包括`int`、`double`和`boolean`)，并对它们有了一些了解。

我们使用文字值、声明变量并使用它们形成表达式。

Java **基本数据类型**包括：

- 整型
  - `byte`
  - `short`
  - `int`
  - `long`
- 浮点型
  - `float`
  - `double`
- 字符型
  - `char`
- 逻辑型
  - `boolean`

在本节中，让我们分别研究一下这些类型，更进一步了解它们。

### 01：整型

整数并不是什么神秘的东西。自上学以来，它们就是我们的一部分，我们通常更喜欢它们，而不是其他数字(它们不会让我们那么害怕！)。

Java很好地支持了它们，我们已经编写了许多使用它们的示例。

Java对于每个整型有一个**包装类**，使得它们更好用。包装类：

- `Byte` - `byte`
- `Short`- `short`
- `Integer` - `int`
- `Long` - long

让我们看看如何使用它们。

##### Snippet-01：整数大小

看看这些小类提供的所有信息！俗话说，“**有备无患**”。根据程序处理的数据(范围和大小)，你可以决定使用哪种类型来存储它们。

```java
jshell> Byte.SIZE
$1 ==> 8
jshell> Byte.BYTES
$2 ==> 1
jshell> Byte.MAX_VALUE
$3 ==> 127
jshell> Byte.MIN_VALUE
$4 ==> -128
jshell> Short.BYTES
$5 ==> 2
jshell> Integer.BYTES
$6 ==> 4
jshell> Long.BYTES
$7 ==> 8
jshell> Short.MAX_VALUE
$8 ==> 32767
jshell> Integer.MAX_VALUE
$8 ==> 2147483647
jshell> int i = 100000;
i ==> 100000
jshell> long l = 50000000000;
| Error:
| integer number too large: 50000000000
| long l = 50000000000;
|_________^
jshell> long l = 50000000000l;
l ==> 50000000000
jshell>
```

##### 整数类型转换

如果我们试图将大数据用小的数据类型存储时，问题就会（也应该）出现。编译器通过标记错误来警告程序员这些问题。然而，如果程序员意识到这些风险并打算继续下去，那么显式强制类型转换就是使代码通过编译的工具。

另一个方向的操作(将较小的数据值存储在较大的容器中)，对于编译器来说是小菜一碟。这样的转换称为隐式强制转换。

##### Snippet-02 : 整型转换

尝试存储一个`long`值到`int`中将得到一个编译器错误。但是，可以使用强制类型转换，比如`i = (int) l;`。

```java
jshell> int i = 100000;
i ==> 100000
jshell> long l = 50000000000l;
l ==> 50000000000
jshell> i = l;
| Error :
| incompatible types: possible lossy conversion from long to int
| i = l;
|_____^
jshell> i = (int) l;
i ==> -1539607552
jshell> l = i;
l ==> -1539607552
jshell>
```

**编译器不负责此语句的类型安全。责任在我这个程序员身上。**

还记得我们前面关于可能的不正确程序行为的陈述吗？可以看到，`i`中存储了一个不同的值。

#### 总结

在这一小节中，我们：

- 研究了为基本整数类型提供的包装器类
- 了解这些类型的不同容量和数据范围
- 研究了如何使用显式和隐式强制类型转换

### 02：整数的表示

在十进制中，允许的数字是从0到9。当遇到10时，位数增加1，表示为“10”。

熟悉数字系统的人都知道，十进制不是计算机能理解的唯一进制。

Java支持8进制和16进制。

在八进制中，允许的数字是0到7，值8用“010”表示。添加前导0只是为了区分八进制格式和十进制格式。

在十六进制中，允许的数字是0到9，然后是a到f(或a到f)， 16的值由“0x10”表示。这里，添加了一个前导0x来帮助编译器识别十六进制表示。

让我们看看Java如何支持这三种进制。

##### Snippet-01：用整数类型存储八进制和十六进制

Java中没有特定于数字系统的整数类型！使用相同的`int`类型存储十进制、八进制和十六进制值。

如果我们坚持关于有效数字的数字系统约定，并理解编译器提示，就不会感到惊讶。

```java
jshell> int eight = 010;
eight ==> 8
jshell> int sixteen = 0x10;
sixteen ==> 16
jshell> int fifteen = 0xf;
fifteen ==> 15
jshell> int eight = 08;//8 is invalid octal digit
| Error:
| integer number too large : 08
| int eight = 08;
|___________^
jshell> int big = 0xbbaacc;
big ==> 12298956
jshell>
```

##### Snippet-02 : 更多的整型转换

有两种赋值：

- 字面量到值赋值：`short s = 123456;`，数据显然超出了范围（在编译时可知）。编译器报错。
- 值到值赋值：看一下`sh = in;`。存在`int in`里的值是`4567`，这完全在`short`类型范围内。编译器选择不冒险并报错。可以使用一个显示强制转换`sh = (short) in`来代替。

```java
jshell> byte b = 128;
| Error:
| incompatible types: possible lossy conversion from int to byte
| byte b = 128;
|_________^--^
jshell> short s = 123456;
| Error:
| incompatible types: possible lossy conversion from int to short
| short s = 123456;
|__________^-------^
jshell> short sh = 3456;
sh ==> 3456
jshell> int in = 4567;
in ==> 3456
jshell> sh = in;
| Error:
| incompatible types: possible lossy conversion from int to short
| sh = in;
|______^
jshell> sh = (short) in;
sh ==> 4567
jshell> int num = sh;
num ==> 4567
jshell>
```

##### 整型的内置运算符

我们已经大致了解了整数类型的算术运算符：

- `+`
- `-`
- `*`
- `/`
- `%`
- `++`（前++和后++）
- `--`（前--和后--）

递增和递减操作符有点意思，因为它们实际上是多个语句的短指针。当我们使用它们的前缀和后缀版本时，需要注意它们的副作用。

##### Snippet-03：加减运算符

对于后++，例如`int j = i++;`，增量发生在赋值后。`j`得到增量之前的值。

```java
jshell> int i = 10;
i ==> 10
jshell> int j = i++;
j ==> 10
jshell> i
i ==> 11
```

对于前++，比如`int n = ++m;`，增量发生在赋值前。`n`得到的是增量后的值。

```java
jshell> int m = 10;
m ==> 10
jshell> int n = ++m;
n ==> 11
jshell> m
m ==> 11
```

对于后--，比如`int l = k--`，减量发生在赋值后。对于前--，比如`int q = --p;`，减量发生在赋值前。

```java
jshell> int k = 10;
k ==> 10
jshell> int l = k--;
l ==> 10
jshell> k
k ==> 9
jshell> int p = 10;
p ==> 10
jshell> int q = --p;
q ==> 9
jshell> p
p ==> 9
jshell>
```

#### 总结：

在这一小节中，我们：

- 研究了Java支持的整数进制
- 研究了前缀和后缀版本如何对递增和递减操作符起作用

### 03：课堂练习 CE-01（带答案）

#### 练习集

1. 创建一个Java类`BiNumber`，该类存储一对整数，并具有以下功能：
   - 可以通过传递存储最初两个数字实例化
   - 必须支持对存储的整数的加法和乘法运算
   - 将两个数字的值翻倍的操作
   - 单独访问每个数字

简而言之，我们必须能在运行类中的`main`方法中编写这样的代码：

```java
BiNumber numbers = new BiNumber(2, 3);
System.out.println(numbers.add());
System.out.println(numbers.multiply);
numbers.double();
System.out.println(numbers.getNumber1());
System.out.println(numbers.getNumber2());
```

##### CE-01的解答过程

***BiNumber.java***

```java
package com.in28minutes.primitive.datatypes;

public class BiNumber {
  private int number1;
  private int number2;
  
  public BiNumber(int number1, int number2) {
    this.number1 = number1;
    this.number2 = number2;
  }
  
  public int add() {
    return number1 + number2;
  }
  
  public int multiply() {
    return number1 * number2;
  }
  
  public void doubleValue() {
    number1 *= 2;
    number2 *= 2;
  }
  
  public int getNumber1() {
    return number1;
  }
  
  public int getNumber2() {
    return number2;
  }
  
	public void setNumber1(int number1) {
    this.number1 = number1;
  }

  public void setNumber2(int number2) {
    this.number2 = number2;
  }
}
```

***BiNumberRunner.java***

```java
package com.in28minutes.primitive.datatypes;

public class BiNumberRunner {
  public static void main(String[] args) {
    BiNumber numbers = new BiNumber(2, 3);
    System.out.println(numbers.add());
    System.out.println(numbers.multiply());
    numbers.doubleValue();
    System.out.println(numbers.getNumber1());
    System.out.println(numbers.getNumber2());
  }
}
```

***控制台输出***

*5*

*6*

*4*

*6*

### 04：浮点类型

你应该记得在Java中有两种支持浮点数的类型：

- `double`：浮点数的默认类型，大小8字节
- `float`：一种更窄、更不精确的浮点数表示。它的大小为4字节。

让我们用一些代码片段快速地回忆一下我们所了解的内容。

##### Snippet-01 : double & float

在Java中默认的浮点类型是`double`。`float`类型必须带有后缀`f`或者`F`。

```java
jshell> float f = 34.5;
| Error:
| incomaptible types: possible lossy conversion from double to float
| float f = 34.5;
|_________^---^
jshell> float f = 34.5f;
f ==> 34.5
jshell> float fl = 34.5F;
fl ==> 34.5
jshell> double d = 34.5678;
d ==> 34.5678
jshell> float flo = d;
| Error:
| incomaptible types: possible lossy conversion from double to float
| float flo = d;
|__________^
jshell> float flo = (float) d;
flo ==> 
```

##### Snippet-02 : double类型相关操作符

你可以对double类型数据使用`++`，`--`和`%`操作符。

```java
jshell> double dbl = 34.5678;
dbl ==> 34.5678

jshell> dbl++
$3 ==> 34.5678

jshell> dbl
dbl ==> 35.5678

jshell> dbl--
dbl ==> 35.5678
jshell> dbl % 5
dbl ==> 4.567799999999998
```

需要显式强制转换才能将浮点数转换为整数值`int i = (int)f`。

```java
jshell> float f = 34.5678f;
f ==> 34.5678
jshell> int i = f;
| Error:
| incomaptible types: possible lossy conversion from float to int
| int i = f;
|_______^
jshell> int i = (int)f;
i ==> 34
jshell> float fl = i;
fl ==> 34.0
jshell>
```

#### 总结

在这一小节中，我们：

- 了解了如何创建浮点类型的字面量和变量
- 学习了`double`和`float`之间的区别

### 05：BigDecimal

虽然`double`和`float`很接近了，但它们并不是浮点数非常精确的表示。

事实上，它们并不用于需要高精确度的计算，比如科学实验和金融应用。下面这个示例说明了原因。

```java
jshell> 34.56789876 + 34.2234
$1 ==> 68.79129875999999
```

常量表达式`34.56789876 + 34.2234`应该等于`68.79129876`。上面的结果并不准确。

这是由于浮点表示法的缺陷造成的，在`double`和`float`类型中都使用了浮点表示法。

在Java中引入了`BigDecimal`类来解决这些问题。

只有在使用`String`常量构建`BigDecimal`表示时，才会保留其准确性。

```java
jshell> BigDecimal number1 = new BigDecimal("34.56789876");
number1 ==> 34.56789876
jshell> BigDecimal number2 = new BigDecimal("34.2234");
number2 ==> 34.2234
```

`BigDecimal`类型只能用于创建**不可变**的对象。不可变对象中的值在创建后不能更改。

可以看到`number1`的值在执行`number1.add(number2)`时没有改变。为了得到相加的结果，我们创建了一个新的变量`sum`。

```java
jshell> number1.add(number2);
$2 ==> 68.79129876
jshell> number1
number1 ==> 34.56789876
jshell> BigDecimal sum = number1.add(number2);
sum ==> 68.79129876
```

#### 总结

在这一小节中，我们：

- 学习了`double`和`float`不是非常精确的数据类型
- 介绍了内置的`BigDecimal`数据类型
- 知道了`BigDecimal`是不可变的
- 当使用字符串常量构造`BigDecimal`数据时，可以保证精确性

### 06：BigDecimal 运算

让我们看一下`BigDecimal`类中定义的其他一些操作。

##### Snippet-01: 算术运算

所有`BigDecimal`运算仅支持`BigDecimal`运算对象。

```java
jshell> BigDecimal number1 = new BigDecimal("11.5");
number1 ==> 11.5 (原文此处为 34.95678，作者笔误)
jshell> BigDecimal number2 = new BigDecimal("23.45678");
number2 ==> 23.45678
jshell> number1.add(number2);
$1 ==> 34.95678
```

`BigDecimal`不能和基本数据类型进行运算。

```java
jshell> int i = 5;
i ==> 5
jshell> number1.add(i);
| Error:
| incompatible types: int cannot be converted to java.math.BigDecimal
| number1.add(i);
|_____________^
```

我们可以对`BigDecimal`值加减乘除。

```java
jshell> number1.add(new BigDecimal(i));
$2 ==> 16.5
jshell> number1.multiply(new BigDecimal(i));
$3 ==> 67.5
jshell> number1.divide(new BigDecimal(100));
$4 ==> 0.115
jshell>
```

#### 总结

这一小节中，我们：

- 学习了`BigDecimal`类用于一些基本算术的方法
- 发现了`BigDecimal`类的构造函数可以接受大多数基本的Java数字类型

### 07：课堂练习 CE-02

#### 练习集

编写一个程序，对本金金额进行单利计算。 这种计算的公式是：

`Total amount (TA) = Principal Amount (PA) + ( PA * Simple Interest (SI) Rate * Duration In Years (N))`

本质上，就是写一个`SimpleInterestCalculator`类能够按下面的方式使用：

```java
SimpleInterestCalculator calculator = new SimpleInterestCalculator("4500.00", "7.5");
BigDecimal totalValue = calculator.calculateTotalValue(5); //5 year duration
System.out.println(totalValue);
```

#### CE-02 答案

***SimpleInterestCalculatorRunner.java***

```java
package com.in28minutes.primitive.datatypes;
import java.math.BigDecimal;

public class SimpleInterestCalculatorRunner {
  public static void main(String[] args) {
    SimpleInterestCalculator calculator = new SimpleInterestCalculator("4500.00", 7.5");
    BigDecimal totalValue = calculator.calculateTotalValue(5); //5 year duration
    System.out.println(totalValue);
  }
}
```

***SimpleInterestCalculator.java***

```java
package com.in28minutes.primitive.datatypes;
import java.math.BigDecimal;

public class SimpleInterestCalculatorRunner {
  BigDecimal principal;
  BigDecimal interest;

  public SimpleInterestCalculator(String principal, String interest) {
    this.principal = new BigDecimal(principal);
    this.interest = new BigDecimal(interest).divide(new BigDecimal(100));
  }

  public BigDecimjal calculateTotalValue(int noOfYears)
    //Total Value = Principal  + Principal * Interest* Years
    BigDecimal totalValue = prinipal.add(principal.multiply(interest).multiply(new BigDecimal(noOfYears)));
    return totalValue;
  }	
}
```

***控制台输出***

*6187.50000*

#### 提示：`import`语句

每个使用另一个包中的类的源文件中都需要Java的`import`语句。所以，***SimpleInterestCalculator.java***（定义的类）和***SimpleInterestCalculatorRunner.java***（定义的运行类）都需要导入`java.math.BigDecimal`类。

默认导入了`package java.lang.*`。

后缀`.*`表示所有在`java.lang`包中的类都被导入了。

#### 总结

这一小节中，我们：

- 在独立的`Java`程序中使用了`BigDecimal`
- 学习了怎样通过`import`语句来使用内置的Java包

### 08：`boolean`，关系运算符和逻辑运算符

Java中的布尔数据类型中的值只包含`true`或者`false`。两者都是大小写敏感的。我们已经看到了内置比较运算符的示例，例如`==`，`!=`和`>`，它们对表达式进行求值得到布尔结果。 让我们快速回顾一下其中的一部分。

##### Snippet-01 : 回顾关系运算符

关系运算符主要用于比较。 它们接受非布尔的基本数据类型的操作数，并返回布尔值。

```java
jshell> int i = 7;
i ==> 7
jshell> i > 7;
$1 ==> false
jshell> i >= 7;
$2 ==> true
jshell> i < 7;
$3 ==> false
jshell> i <= 7;
$4 ==> true
jshell> i == 7;
$5 ==> true
jshell> i == 8;
$6 ==> false
jshell>
```

#### 逻辑运算符

Java还有用在表达式中的逻辑运算符。逻辑运算符接受布尔操作数。这些表达式用于在代码中形成布尔条件，包括`if`，`for`和`while`语句内。几个重要的逻辑运算符为：

- `&&`：逻辑与
- `||`：逻辑或
- `!`：逻辑非

让我们学习一下如何在代码中使用它们。

##### Snippet-02 : 逻辑运算符

我们想看看`i`是否在`15`到`25`之间。可以使用表达式`i> = 15 && i <= 25`。详细信息如下。

```java
jshell> int i = 17;
i ==> 17
jshell> i >= 15
$1 ==> true
jshell> i <= 25
$2 ==> true
jshell> i >= 15 && i <= 25
$3 ==> true
jshell> i == 30;
i ==> 30
jshell> i >= 15 && i <= 25
$4 ==> false
jshell> i == 5;
i ==> 30
jshell> i >= 15 && i <= 25
$5 ==> false
```

只有当带有`&&`的表达式的两个布尔操作数都为`true`，整个表达式才为`true`。

```java
jshell> true && true
$6 ==> true
jshell> true && false
$7 ==> false
jshell> false && true
$8 ==> false
jshell> false && false
$9 ==> false
jshell>
```

##### Snippet-02 说明

下一个示例帮助我们可视化主要的逻辑运算符的真值表。

```java
	jshell> true || true
	$1 ==> true
	jshell> true || false
	$2 ==> true
	jshell> false || true
	$3 ==> true
	jshell> false || false
	$4 ==> false
	jshell> true ^ true
	$5 ==> false
	jshell> true ^ false
	$6 ==> true
	jshell> false ^ true
	$7 ==> true
	jshell> false ^ false
	$8 ==> false
	jshell> !true
	$9 ==> false
	jshell> !false
	$10 ==> true
	jshell> int x = 6;
	x ==> 6
	jshell> !(x > 7)
	$11 ==> true
	jshell>
```

#### 总结

这一小节中，我们：

- 我们引入了`boolean`基本数据类型
- 学习了在哪里使用逻辑运算符
- 学习了常用逻辑运算符的真值表

### 09：短路求值（带疑问）

思考下面这段代码。表达式`j > 15 && i++ > 5`为值应该为`false`。因为`j`的值为`15`，所以`j>15`。

```java
jshell> int j = 15;
j ==> 15
jshell> int i = 10;
i ==> 10
jshell> j > 15 && i++ > 5
$1 ==> false
jshell> j
j ==> 15
jshell> i
i ==> 10
```

你也可以发现`i`的值保持不变为`10`。

为什么？因为`i++ > 5`甚至都没有执行。为什么？`&&`是惰性的。当`j > 15`为`false`时。无论第二个表达式的结果如何，这个`&&`的结果都是`false`。所以它不计算第二个表达式的值。

***更详细的解释***

从左至右扫描表达式`j > 15 && i++ > 5`。当第一个操作数到`&&`被赋值为`false`时，编译器变懒了。`&&`避免计算不影响最终结果的表达式。这种优化有一个名字：**短路求值**，也叫**延迟求值**。

逻辑运算符`&`是逻辑与操作，它消除了延迟计算。

`&`两边的操作数都会进行计算。

```java
jshell> j > 15 & i++ > 5
$1 ==> false
jshell> j
j ==> 15
jshell> i
i ==> 11
jshell>a
```

同样，**或**运算符也有两个版本：

- 之前看到的`||`运算符。表现为延迟求值。
- `|`运算符，非延迟求值。

对于我们的代码而言，依赖于编译器的延迟求值不是好的编程习惯。 它使代码的可读性降低，并且可能隐藏难以修复的bug。 这显然增加了代码维护工作，所以别这么做，除非你想被你的同行厌恶。

#### 总结

在这一小节中，我们：

- 验证了涉及到逻辑运算的条件会有延迟求值
- 发现了延迟求值取决于操作符的真值表
- 看了没有延迟求值的运算符版本
- 知道了依赖于延迟求值的代码具有更差的可读性

### 10：字符类型

之前，我们讨论了如何存储基本的键盘字符（称为**ascii码**字符），比如：

- 大小写字母
- 数字
- 标点符号和其他特殊字符（比如  ‘,’, ‘$’, ‘{’ 等）

事实证明Java支持更大的字符编码集，称为**Unicode**。所有的Unicode字符都可以输入到代码中，有代码理解和出来，以及从代码中输出。

##### Snippet-01： Unicode字符

不是所有的Unicode字符都可以从键盘输入。但是如果正确处理它们的格式，Java允许你从代码中处理它们的值。

```java

jshell> char ch = '"';
ch ==> '"'
jshell> char c = '\u0022';
c ==> '"'
```

整数值可以存储在`char`变量中。如果值在有意义的范围内，它也对应于键盘字符的**ascii**值。

```java
jshell> char cn = 65;
cn ==> 'A'
```

整数运算可以用在`char`数据上。

```java
jshell> cn++
$1 ==> 'A'
jshell> cn
$2 ==> 'B'
jshell> ++cn
$3 ==> 'C'
jshell> cn + 5
$4 ==> 72
jshell> cn
cn ==> 'C'
jshell> (int)cn
cn ==> 67
jshell>
```

#### 总结

在这一小节中，我们：

- 引入了`char`数据类型
- 学习了Unicode将字符集扩展到键盘之外
- ascii字符是`char`值，用一个整数值编码

### 11：编程练习 PE-02

#### 练习集

1. 编写一个Java类`Mychar`，它是一种特殊`char`类型。将围绕输入`char`数据元素创建`MyChar`类型的对象，并具有以下功能：
   - 检查输入字符是否为：
     - 数字
     - 字母
     - 元音字母（大写或小写）
     - 辅音字母（大写或小写）注：如果不是元音，则字母是辅音
   - 打印所有字母
     - 大写
     - 小写

实质上，`MyChar`的运行类的`main`方法运行代码类似于：

```java
MyChar myChar = new MyChar('c');
System.out.println(myChar.isDigit());
System.out.println(myChar.isAlphabet());
System.out.println(myChar.isVowel());
System.out.println(myChar.isConsonant());
myChar.printLowerCaseAlphabets();
myChar.printUpperCaseAlphabets();
```

### 12：PE-02答案，Part 1 - `isVowel()`

***MyCharRunner.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyCharRunner {
  public static void main(String[] args) {
    MyChar myChar = new MyChar('c');
    System.out.println(myChar.isVowel());
  }
}
```

***MyChar.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyChar {
  private char ch;

  public MyChar(char ch) {
    this.ch = ch;
  }

  public boolean isVowel() {
    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
      return true;
    } 
    if(ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U') {
      return true;
    }
    return false;
  }
}
```

***控制台输出*** :

*false*

### 13：PE-02答案，Part 2 - `is Digit()`

***MyCharRunner.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyCharRunner {
  public static void main(String[] args) {
    MyChar myChar = new MyChar('c');
    System.out.println(myChar.isDigit());
    System.out.println(myChar.isVowel());
  }
}
```

***MyChar.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyChar {
  private char ch;

  public MyChar(char ch) {
    this.ch = ch;
  }

  public boolean isVowel() {
    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
      return true;
    } 

    if(ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U') {
      return true;
    }
    return false;
  }

  public boolean isDigit() {
    if(ch >= 48 && ch <= 57) {
      return true;
    }
    return false;
  }

}
```

***控制台输出*** :

*false*

*false*

### 14：PE-02答案，Part 3 - 其他方法

***MyCharRunner.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyCharRunner {
  public static void main(String[] args) {
    MyChar myChar = new MyChar('c');
    System.out.println(myChar.isDigit());
    System.out.println(myChar.isAlphabet());
    System.out.println(myChar.isVowel());
    System.out.println(myChar.isConsonant());
    myChar.printLowerCaseAlphabets();
    myChar.printUpperCaseAlphabets();
  }
}
```

***MyChar.java***

```java
package com.in28minutes.primitive.datatypes;

public class MyChar {
  private char ch;

  public MyChar(char ch) {
    this.ch = ch;
  }

  public boolean isVowel() {
    if(ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
      return true;
    } 
    if(ch == 'A' || ch == 'E' || ch == 'I' || ch == 'O' || ch == 'U') {
      return true;
    }
    return false;
  }

  public boolean isConsonant() {
    if(isAlphabet() && !(isVowel())) {
      return true;
    }
    return false;
  }

  public boolean isDigit() {
    if(ch >= 48 && ch <= 57) {
      return true;
    }
    return false;
  }

  public boolean isAlphabet() {
    if(ch >= 97 && ch <= 122) {
      return true;
    }
    if(ch >= 65 && ch <= 90) {
      return true;
    }
    return false;
  }

  public void printLowerCaseAlphabets() {
    for(char ch='a'; ch <= 'z'; ch++) {
      System.out.println(ch);
    }
  }

  public void printUpperCaseAlphabets() {
    for(char ch='A'; ch <= 'Z'; ch++) {
      System.out.println(ch);
    }
  }
}
```

***控制台输出*** :

*false*

*true*

*false*

*true*

a

b

c

d

e

f

g

h

i

j

k

l

m

n

o

p

q

r

s

t

u

v

w

x

y

z

A

B

C

D

E

F

G

H

I

J

K

L

M

N

O

P

Q

R

S

T

U

V

W

X

Y

Z

### 15：基本数据类型 - 复习

在本节中，我们了解了Java基本数据类型。

- 我们首先熟悉整数类型的内置包装器，它存储有用的类型信息。
- 从整数类型到浮点类型，我们研究了类型兼容性，以及编译器如何警告常见的陷阱。 我们使用显式强制转换来强制类型转换，并了解到隐式类型转换非常普遍。
- 我们使用了`BigDecimal`类，这是一种具有更高精度和准确性的浮点类型。
- 接下来是`boolean`，建立在我们所知道的逻辑表达式上。我们主要关注逻辑运算符，更侧重于对它们表达式的短路求值。
- 我们了解了依赖于副作用和延迟求值不是一个好的编程习惯。
- 最后，我们学习了`char`类型，发现了远远不止键盘上所限的字符。