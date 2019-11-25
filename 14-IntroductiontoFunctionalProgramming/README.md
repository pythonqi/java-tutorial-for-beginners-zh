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

### 03：过滤结果

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

