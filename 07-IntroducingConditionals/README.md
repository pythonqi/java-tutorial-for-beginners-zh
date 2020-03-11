# 条件语句介绍 - if, switch等

决策是我们日常生活的一部分。计算机为人类执行任务，所以即使是程序也需要做决定。它们通过检查逻辑条件做到这一点，逻辑条件的值是布尔值。

在接下来的章节中，我们将研究下面的**条件**语句：

- `if`
- `if` - `else`
- `if` - `else if` - `else`
- `switch`

要掌握这些基础知识，还有什么比用它们来解决编程挑战更好的方法呢?

我们开始吧！

#### 编程挑战：设计菜单（*菜单挑战*）

- 要求用户输入：
  - 输入两个数字
  - 选择要做的算术
    - 加
    - 减
    - 乘
    - 除
  - 执行操作
  - 输出结果

***举个例子：***

输入第一个数

2

输入第二个数

4

1 - 加

2 - 减

3 - 乘

4 - 除

输入你选择的操作

3

结果为：8

#### 总结

在本小节中，我们：

- 讨论了如何通过输入影响程序的控制流
- 列出了Java中可用的条件语句
- 选择一个编程实战来帮助我们学习条件语句

### 01：`if`和`if`-`else`条件语句

`if`语句是在程序中管理控制流最基本的方式。测试了布尔条件，如果发现条件为真，则将执行一些代码。 否则，该代码将不会运行。

- ***“当条件为真时执行一些操作”***

从概念上讲，`if`语句如下所示：

```java
if(condition) {
  <if-body>
}
```

`if`-`else`语句可归结为以下内容

```java
if(condition) {
  <if-body>
} else {
  <else-body>
}
```

如果`condition`为`true`时，执行`<if-body>`语句块，否则运行`<else-body>`语句块

让我们看一些使用这些条件语句的示例。

##### Snippet-01 : `if`

本例中：

- 我们使用了复合比较运算符，例如`<=`和`> =`，它们也可以计算为布尔值/
- 还使用诸如`&&`和`||`之类的逻辑运算符，它们都接受并返回布尔值。

```java
jshell> int i = 3;
i ==> 3
jshell> if(i==3) {
   ..>> System.out.println("True");
   ..>> }
True
jshell> if(i<2) {
   ..>> System.out.println("True");
   ..>> }

jshell> if(i<=3 || i >= 35) {
   ..>> System.out.println("True");
   ..>> }
True
jshell> if(i<=3 && i >= 35) {
   ..>> System.out.println("True");
   ..>> }
```

`if`-`else`允许我们指定条件为`false`时要执行的代码。

```java
jshell> if(i==3) {
   ..>> System.out.println("True");
   ..>> } else {
   ..>> System.out.println("i is not 3");
   ..>> }
True
jshell> i = 5;
i ==> 5
jshell> if(i==3) {
   ..>> System.out.println("True");
   ..>> } else {
   ..>> System.out.println("i is not 3");
   ..>> }
i is not 3
jshell>
```

##### Snippet-02：链式`if`-`else` - v1

***IfStatementRunner.java***

```java
com.in28minutes.ifstatement.examples;

public class IfStatementRunner {
  public static void main(String[] args) {
    //int i=25;
    int i=26;
    if(i == 25) {
      System.out.println("i = 25");
    } else {		
      System.out.println("i != 25");
    }
  }
}
```

***控制台输出***

*i != 25*

##### Snippet-03：链式 `if`-`else` - v2

我们将测试三种条件 - `i的值为24`，`i的值为25` 或者 `i的值既不是24也不是25`。思考下面这个例子的代码。

***IfStatementRunner.java***

```java
com.in28minutes.ifstatement.examples;

public class IfStatementRunner {
  public static void main(String[] args) {
    // if i is 25, print i = 25
    //if i is 24, print i = 24
    //otherwise, print i != 25 and i != 24

    int i=25;
    if(i == 25) {
      System.out.println("i = 25");
    }
    if(i == 24) {
      System.out.println("i = 24"); 
    } else {			
      System.out.println("i != 25 and i != 24");
    }
  }
}
```

***控制台输出***

*i = 25*

*i != 25 and i != 24*

##### Snippet-03 说明

刚刚发生了什么？在程序中，`i`的值被设置为`25`，因此与前面的例子一样，应该只输出***i = 25***。

为什么有额外的打印？

我们开始尝试检查3种可能性:`i`等于`25` ，`i`等于`24` ，或者都不相等。

我们得到了错误的输出，因为在第一个`if`中的`i == 25`与在接下来的`if`-`else`中的`i == 24`之间是相互独立的。

我们的决策不是连续的。我们需要一个更严格的条件来处理两个以上的选择。我们将在下一小节中探讨这个问题。

#### 总结

在本节中，我们：

- 学习了`if`和`if`-`else`条件语句
- 尝试了几个例子来看看它们如何使用的

