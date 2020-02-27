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

##### 总结

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

##### 总结：

在这一小节中，我们：

- 研究了Java支持的整数进制
- 研究了前缀和后缀版本如何对递增和递减操作符起作用

### 03：课堂练习 CE-01（带解题过程）

##### 练习集

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

