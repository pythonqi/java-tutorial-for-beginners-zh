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