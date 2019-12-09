# 函数式编程

函数式编程究竟是什么？

让我们来看看。

函数式编程视频

- Part 1 - https://www.youtube.com/watch?v=aFCNPHfvqEU
- Part 2 - https://www.youtube.com/watch?v=5Xw1_IREXQs

### 01: 函数式编程介绍

让我们看一个典型的程序，遍历并打印一个列表的内容。

##### OOP List 遍历

***FunctionalProgrammingRunner.java***
```java
package com.in28miutes.functionalprogramming;
import java.util.List;

public class FunctionalProgrammingRunner {
    public static void main(String[] args) {
        List<String> list = List.of("Apple", "Banana", "Cat", "Dog");
        for (String str:list) {
            System.out.println(str);
        }
    }
}
```

***控制台输出***

*Apple*

*Banana*

*Cat*

*Dog*

##### Snippet-01 说明
上面的方法着重于**怎么样**。
我们遍历了这个列表，访问了列表的每个元素并用`System.out.println()`打印了它们。
函数式编程让我们可以专注于**什么**。

##### Snippet-02：printBasic() 和 printFunctional()

***FunctionalProgrammingRunner.java***

```java
package com.in28minutes.functionalprogrammin;
import java.util.List;

public class FunctionalProgrammingRunner {
  public static void main(String[] args) {
    List<String> list = List.of("Apple", "Banana", "Cat", "Dog");
    //printBasic(list);
    printFunctional(list);
  }
  
  public static void printBasic(List<String> list) {
    for(String str:list) {
      System.out.println(str);
    }
  }
  
  public static void printFunctional(List<String> list) {
    list.stream().forEach(element -> System.out.println(element));
  }
  
}
```

***控制台输出***

*Apple*

*Banana*

*Cat*

*Dog*

##### Snippet-02 说明
`list.stream().forEach(element -> System.out.println(element))` - 打印在list流中的每个元素。
`element -> System.out.println(element)`称为**lambda表达式**。

### 02：遍历`List`

在之前的小节中，我们使用了一段代码 - `list.strem().forEach(element -> System.out.println(element))`

我们**将函数当做方法参数传递**。

让我们用JShell来进一步理解。

让我们试着打印一组数字。

##### Snippet-01 : 使用FP遍历

```java
jshell> List<Integer> list = List.of(1, 4, 7, 9);
list ==> [1, 4, 7, 9]
jshell> list.stream().forEach(elem -> System.out.println(elem));
1
4
7
9
jshell>
```

##### Snippet-01 注释

`elem -> System.out.println(elem)` 是一个lambda表达式。列表流中的每个元素都会执行这个lambda表达式。

### 03：过滤

流是一种值序列。`filter()`方法可以基于一定的逻辑来过滤流元素。

##### Snippet-01 : 使用 `filter()`

`printBasicWithFiltering`表示一般的过滤方法。`printFPwithFiltering`表示函数式过滤方法。

```java
package com.in28minutes.functionalprogramming;
import java.util.List;

public class FunctionalProgrammingRunner {
  public static void main(String[] args) {
    List<String> list = List.of("Apple", "Bat", "Cat", "Dog");
    //printBasicWithFiltering(list);
    printFPWithFiltering(list);
  }

  public static void printBasicWithFiltering(List<String> list) {
    for(String str:list) {
      if(str.endsWith("at")) {
        System.out.println(str);
      }
    }
  }

  public static void printFPWithFiltering(List<String> list) {
    list.stream()
      .filter(elem -> elem.endsWith("at"))
      .forEach(element -> System.out.println(element));

  }	
}
```

***控制台输出***

*Bat*

*Cat*

##### Snippet-02 : 打印奇偶数

让我们看看如何过滤数字。

```java
jshell> List<Integer> list = List.of(1, 4, 7, 9);
list ==> [1, 4, 7, 9]
jshell> list.stream().forEach(elem -> System.out.println(elem));
1
4
7
9
jshell> list.stream().filter(num -> num%2 == 1).forEach(elem -> System.out.println(elem));
1
7
9
jshell> list.stream().filter(num -> num%2 == 0).forEach(elem -> System.out.println(elem));
4
jshell>
```

##### Snippet-02 注释

通常，这是我们写的条件

- `num`是奇数：`if(num % 2 == 1) { /* */ }`
- `num`是偶数：`if(num % 2 == 0) { /* */ }`

在上面的例子中，我们使用lambda表达式定义相同的条件。

- `num`是奇数: `num -> num%2 == 1`
- `num` 是偶数: `num -> num%2 == 0`

### 04：流 - 聚合

有时我们想把数据聚合为一个结果。比如，我们想把从`1`到`10`之间的所有数字加起来。或者我们想计算我们城市一个月来平均最大温度。

##### Snippet-01：序列和

让我们看一下如何使用`reduce`方法计算和。

***FPNumberRunner.java***

```java
package com.in28minutes.functionalprogramming;
import java.util.List;

public class FPNumberRunner {
  public static void main(String[] args) {
    List<Integer> numbers = List.of(4, 6, 8, 13, 3, 15);
    //System.out.println(printBasicSum(numbers));
    int sum = numbers.stream().reduce(0, (num1, num2) -> num1 + num2);
    System.out.println(sum);
  }

  void printBasicSum(List<Integer> numbers) {
    int sum=0;
    for(int num:numbers) {
      sum += num;
    }		
    System.out.println(sum);
  }
}
```

***控制台输出***

*49*

##### Snippet-01 注释

`reduce()`方法每次作用于一对元素。*初始值*为`0`。lambda表达式`(num1, num2) -> num1 + num2`作用与元素列表，每次一对。

#### Classroom Exercise CE-01

1. 给定一个列表`(4, 6, 8, 13, 3, 15)`，计算：
   - 该列表所有偶数和
   - 该列表所有奇数和

#### Solution To CE-01

***FPNumberRunner.java***

```java
package com.in28minutes.functionalprogramming;
import java.util.List;

public class FPNumberRunner {
  public static void main(String[] args) {
    List<Integer> numbers = List.of(4, 6, 8, 13, 3, 15);
    printFPEvenSum(numbers);			
    printFPOddSum(numbers);
  }

  void printFPEvenSum(List<Integer> numbers) {
    int sum = numbers.stream()
             .filter(elem -> elem %2 == 0)
             .reduce(0, (num1, num2) -> num1 + num2);
    System.out.println("Even Numbers Sum: " + sum);
  }

  void printFPOddSum(List<Integer> numbers) {
    int sum = numbers.stream()
             .filter(elem -> elem %2 == 1)
             .reduce(0, (num1, num2) -> num1 + num2);
    System.out.println("Odd Numbers Sum: " + sum);
  }
}
```

***控制台输出***

*Even Numbers Sum: 18*

*Odd Numbers Sum: 31*

### 05：函数式编程 vs 结构化编程

回顾一下上一节中的***FPNumberRunner.java***。我们写了两种不同的方法计算同一个列表的和：

- `basicSum()`: 使用传统的方法。
- `fpSum()`：使用函数式编程方案。

把它们作为参考来看一下*SP*和*FP*的最大的不同。

1. **Structured Programming (SP)**

```java
public int basicSum(List<Integer> numbers) {
  int sum=0;
  for(int num:numbers) {
    sum += num;
  }
  return sum;
}
```

2. **Functional Programming (FP)**

```java
public int  fpSum(List<Integer> numbers) {
  int sum = numbers.stream()
           .reduce(0, (num1, num2) -> num1 + num2);
  return sum;
}
```

有什么不同？

- **可变性** （修改程序数据）：

  i. *SP*：在`basicSum()`中，`sum`变量（一种工作者变量）初始值为`0`，它在`for`循环中发生改变。

  ii. *FP*：我们只是为`reduce()`方法设置了一个初始值。没有发生任何改变。

- 计算的**内容**和**方式**：

  i. *SP*：我们指定了做什么和怎么做。代码使用了`for`来遍历列表元素，同时还更新`sum`的值。

  ii. *FP*：我们主要关注做什么，不太管怎么做。`reduce()`知道要从流中累加哪些数字，而你不必担心如何从流中选择它们。

### 06：一些函数式编程术语

让我们更正式地了解一些FP术语。

#### Lambda 表达式

```java
(num1, num2) -> num1 + num2
```

与下面这个方法等效

```java
int basicSum(int num1, int num2) {	
		return num1 + num2;
}
```

lambda表达式也可以有多行代码：

```java
(num1, num2) -> {
  System.out.println(num1 + " " + num2);
  return num1 + num2;
}
```

让我们把这些代码放到IDE中运行看看。

##### Snippet-01：Lambda表达式

***FPNumberRunner.java***

```java
package com.in28minutes.functionalprogramming;
import java.util.List;

public class FPNumberRunner {
  public static void main(String[] args) {
    List<Integer> numbers = List.of(4, 6, 8, 13, 3, 15);
    System.out.println(numbers);
    printFPSum(numbers);
  }

  void printFPSum(List<Integer> numbers) {
    int sum = numbers.stream()
             .reduce(0,
                 (num1, num2) -> {
                          System.out.println(num1 + " " + num2);
                          return num1 + num2;
                         }
    System.out.println("Even Numbers Sum: " + sum);		
  }
}
```

**控制台输出**

*[4, 6, 8, 13, 3, 15]*

*0 4*

*4 6*

*10 8*

*18 13*

*31 3*

*34 15*

*49*

#### Stream（流）

流是一系列元素。你可以在流上执行各种操作。

- **中间操作**：例如，在流上应用一个lambda表达式—并生成另一个元素流作为其结果。

- **最终操作**：例如，在留上应用一个lambda表达式—并返回单一的结果（单一的基本类型值/对象，或者一个单一的对象集合）。`reduce()`和`forEach()`就是这样一类操作。