# 集合介绍

数组非动态数据结构，只能存储固定大小的一系列元素。
对一个数组进行插入或者删除元素并非易事。
在Java中内置的集合(Collections)能够支持动态数据结构。常用的集合基于列表，树和哈希表。
Java提供了非常棒的集合实现。
为了便于理解所有的集合，我们先从这些接口开始，比如`List`，`Set`, `Queue`，`Map`等等。
在那之后，我们将打算实现这些接口，比如`LinkedList`，`HashTable`和`TreeMap`等等。

## 集合接口
让我们先从`List`接口开始

### List 接口
`List interface`在Java中被用于实现一个有序集合。有序集合就是一个程序员能够控制一个元素插入的位置，或者从该集合中访问某个元素。
如果一个元素的插入位置没有确定，它会被放到`List`的末尾。
`List`一般是允许*重复*元素的。

##### Snippet-1: 创建一个列表
下面是一个创建列表和访问元素的例子：
```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]
jshell> words.size()
$1 ==> 3
jshell> words.isEmpty()
$2 ==> false
jshell> words.get(0)
$3 ==> Apple
jshell> words.contains("Dog")
$4 ==> false
jshell> words.contains("Cat")
$5 ==> true
jshell> words
words ==> [Apple, Bat, Cat]
jshell> words.indexOf("Cat")
$6 ==> 2
jshell> words.indexOf("Dog")
$7 ==> -1
jshell>
```
#### List 的不变性
仔细看看上面代码块中的`List words`
`List<String> words = List.of("Apple", "Bat", "Cat");`
使用静态方法`of`创建的列表是不可变的。

```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]
jshell> words.add("Dog");
| java.lang.UnsupportedOperationExcetion thrown:
| at ImmutableCollections.uoe (ImmutableCollections.java:71)
| at ImmutableCollections$AbstractImmutableList.add (ImmutableCollections.java:77)
| at (#15:1)
jshell>
```
#### 创建可变的 List
创建一个可以随时更新数据的`List`的方法是实例一个实现了`List`接口的内置`Collection`类。
比如`ArrayList`，`LinkedList`和`Vector`.

##### Snippet-3: 可变列表
让我们看几个例子:
```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]

jshell> List<String> wordsArrayList = new ArrayList<String>(words);
wordsArrayList ==> [Apple, Bat, Cat]

jshell> List<String> wordsLinkedList = new LinkedList<String>(words);
wordsLinkedList ==> [Apple, Bat, Cat]

jshell> List<String> wordsVector = new Vector<String>(words);
wordsVector ==> [Apple, Bat, Cat]

jshell> wordsArrayList.add("Dog");
$1 ==> true

jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Cat, Dog]

jshell>
```
#### ArrayList vs LinkedList
`ArrayList` 使用一个数组存储元素。
- 根据位置访问和修改元素效率高，常数时间算法复杂度。
- 元素的插入或者删除效率低。在20个元素的列表中的第0个位置插入一个元素，需要移动20个元素。

实现`LinkedList`的是一种串行的数据结构，有一组内存插槽组成。
- 插入删除元素效率高。这是因为在一个块链中，每个链接只是对下一个块的引用。插入只涉及到将这些链接指向新的值，不需要大量复制和移动已存在的元素。
- 根据位置访问和修改元素效率低于`ArrayList`，因为访问元素总是需要遍历链表。

优化：`LinkedList`底层数据结构实际上是双向链表，每一个元素都有正向和反向链接。

#### Vector vs ArrayList

`Vector`从jdk1.0就存在于Java中了，`ArrayList`在稍后的jdk1.2被添加到Java中。它们的底层数据结构用的都是数组。

`Vector`是线程安全的。在`Vector`中，所有的方法都是同步（`synchronized`）的。

> 和其他线程安全的`List`实现比较，`Vector`并发度低。

#### List 操作

我们将在一个`ArrayList`上研究`List`公有的方法。在`LinkedList`和`Vector`同样可以实现相似的操作。

##### Snippet-4: 列表插入

我们来看一些例子

- 插入元素到末尾（默认）
- 具体位置插入
- 允许插入重复数据
- 将另外一个列表的所有元素添加到当前的列表中
  - 放在最后
  - 具体位置插入同样也可以，就像插入单个元素一样

```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]
jshell> List<String> wordsArrayList = new ArrayList<String>(words);
wordsArrayList ==> [Apple, Bat, Cat]
jshell> wordsArrayList.add("Dog");
$1 ==> true
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Cat, **Dog**]
jshell> wordsArrayList.add("Elephant");
$2 ==> true
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Cat, Dog, **Elephant**]
jshell> wordsArrayList.add(2, "Ball");
*jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, **Ball**, Cat, Dog, Elephant]
jshell> wordsArrayList.add("Ball");
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Ball, Cat, Dog, Elephant, **Ball**]
jshell> List<String> newList = List.of("Yak", "Zebra");
newList ==> [Yak, Zebra]
jshell> wordsArrayList.addAll(newList);
$3 ==> true
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Ball, Cat, Dog, Elephant, Ball,  **Yak**, **Zebra**]
jshell>
```

##### Snippt-5: 元素修改

让我们看一些例子

- 修改指定位置的元素
- 删除元素

```java
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Ball, Cat, Dog, Elephant, Ball,  Yak, Zebra]
jshell> wordsArrayList.set(6, "Fish");
$4 ==> "Ball"
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Ball, Cat, Dog, Elephant, **Fish**,  Yak, Zebra]
jshell> wordsArrayList.remove(2);
$5 ==> "**Ball**"
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Cat, Dog, Elephant, Fish,  Yak, Zebra]
jshell> wordsArrayList.remove("Dog");
$6 ==> true
jshell> wordsArrayList
wordsArrayList ==> [Apple, Bat, Cat, Elephant, Fish,  Yak, Zebra]
jshell> wordsArrayList.remove("Dog");
$6 ==> false
jshell>
```

##### Snippet-5: 遍历ArrayList

现在，让我们来看一下如何遍历一个`List`中的内容

基本的for循环：

```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]
jshell> for(int i=0; i<words.size(); i++) {
...> System.out.println(words.get(i));
...> }
Apple
Bat
Cat
```

使用增强的for循环：

```java
jshell> for(String word:words) {
...> System.out.println(word);
...> }
Apple
Bat
Cat
```

使用迭代器：

```java
jshell> Iterator wordsIterator = words.iterator();
wordsIterator ==> java.util.AbstractList$Itr@3712b94
jshell> while(wordsIterator.hasNext()) {
...> System.out.println(wordsIterator.next());
...> }
Apple
Bat
Cat
```

#### 迭代模式的选择

------

- 对于不可变的遍历，增强的`for`循环最方便
- 对于可变的遍历：
  - 元素删除的情况：不推荐增强的`for`循环，下面的例子中可以看到。`"Bat"`被删除了，但是`"Cat"`并没有被删除，由于遍历本身被影响了。
  - 迭代器可以用于此类迭代。

##### Snippet-6

```java
jshell> List<String> words = List.of("Apple", "Bat", "Cat");
words ==> [Apple, Bat, Cat]
jshell> List<String> wordsAL = new ArrayList<>(words);
wordsAL ==> [Apple, Bat, Cat]
jshell> for(String word:words) {
  ...> if(word.endsWith("at"))
   ...> System.out.println(word);
   ...> }
   ...> }
Bat
Cat
jshell> for(String word:wordsAL) {
   ...> if(word.endsWith("at"))
   ...> wordsAL.remove(word);
   ...> }
   ...> }
jshell> wordsAL
wordsAL ==> [Apple, Cat]
jshell> Iterator wordsIterator = wordsAL.iterator();
wordsIterator ==> java.util.AbstractList$Itr@3712b94
jshell> while(wordsIterator.hasNext()) {
   ...> if(wordsIterator.next().endsWith("at")){
   ...> wordsIterator.remove();
   ...> }
   ...> }
jshell> wordsAL
wordsAL ==> [Apple]
jshell>
```

#### List: 类型安全

`List`类型的集合不存储基本数据类型。它只存储对象引用。当我们试图存储基本数据类型时，如`int`，`char`或者`double`，它们隐式地转化成了各自对应的包装类型，分别叫做`Integer`，`Character`和`Double`。基本数据类型*自动装箱*

##### Snippet-7: 类型安全

`ArrayList.indexOf()`方法没有重载，它只有一个版本。所以，当传递一个`int`类型的实参，它会自动装箱成为一个`Integer`对象，然后该方法执行。

- 然而，`ArrayList.remove()`方法有两个重载版本：
  - `ArrayList.remove(int index)`：删除`ArrayList`中特定下标的元素
  - `ArrayList.remove(Object o)`：删除一个特定的元素，如果它在`ArrayList`中存在

```java
jshell> List values = List.of("A", 'A', 1, 1.0);
values ==> ["A", 'A', 1, 1.0]
jshell> values.get(2)
$1 ==> 1
jshell> values.get(2) instanceof Integer
$2 ==> true
jshell> values.get(1) instanceof Character
$3 ==> true
jshell> values.get(3) instanceof Double
$4 ==> true
jshell> List<String> textValues = List.of("A", 'A', 1, 1.0);
| Error
| Error
| List<String> textValues = List.of("A", 'A', 1, 1.0);
|___________________________^------------------------^
jshell> List<Integer> numbers = List.of(101, 102, 103, 104, 105);
numbers ==> [101, 102, 103, 104, 105]
jshell> numbers.indexOf(101)
$5 ==> 0
jshell> List<Integer> numbersAL = new ArrayList<>(numbers);
numbersAL ==> [101, 102, 103, 104, 105]
jshell> numbersAL.indexOf(101)
$6 ==> 0
jshell> numbersAL.remove(101)
java.lang.IndexOutOfBoundsException!!
jshell> numbersAL.remove(Integer.valueOf(101))
$7 ==> true
jshell> numbersAL
numbersAL ==> [102, 103, 104, 105]
jshell>
```

#### List排序

通过`List.of()`获得的`List`是不可变的，所以它自身无法被排序。所以，需要创建一个可变的`ArrayList`。

`ArrayList.sort()`方法定义一个`Comparator`对象。简单点的操作是可以使用`Collections.sort()`代替。

```java
jshell> List<Integer> numbers = List.of(123, 12, 3, 45);
numbers ==> [123, 12, 3, 45]
jshell> List<Integer> numbersAL = new ArrayList<>(numbers);
numbersAL ==> [123, 12, 3, 45]
jshell> numbersAL.sort();
| Error:
| required: java.util.Comparator<? super java.lang.Integer>
| numbersAL.sort();
|^-------------^
jshell> Collections.sort(numbersAL);
jshell> numbersAL
numbersAL ==> [3, 12, 45, 123]
jshell>
```

#### List 排序

##### Snippet-8: 排序列表

让我们创建一个Student类并尝试使用`Collection.sort()`排序

***Student.java***

```java
package collections;

public class Student {
  private int id;
  private String name;

  public Student(int id, String name) {
    super();
    this.id = id;
    this.name = name;
  }

  public int getId() {
    return id;
  }

  public void setId(int id) {
    this.id = id;
  }

  public String getName() {
    return name;		
  }

  public void setName(String name) {
    this.name = name;
  }

  public String toString() {
    return id + " " + name;
  }
}
```

***StudentsCollectionRunner.java***

```java
package collections;
import java.util.Collections;
import java.util.List;
import java.util.ArrayList;

public class StudentsCollectionRunner {
  public static void main(String[] args) {
    List<Student> students = List.of(new Student(1, "Ranga"),
                    new Student(100, "Adam"),
                    new Student(2, "Eve"));
    ArrayList<Student> studentsAl = new ArrayList<>(students);
    System.out.println(studentsAl);
    Collections.sort(studentsAl);
    System.out.println(studentsAl);
  }
}
```

***控制台输出***

***COMPILER ERROR（编译错误）***

##### Snippet-9 解释

对于`Collections.sort()`方法来说，它只接受这些列表，其中的列表元素类型`T`实现了 `Comparable<? super T>`接口

`Student`类没有实现这个接口。结果 - 编译错误。

##### Snippet-10: 实现Comparator接口

***StudentsCollection.java***

```java
package collections;
import java.util.Comparable;

public class Student implements Comparable<Student> {
  // Same as earlier
  @Override
  public int compareTo(Student that) {
    return Integer.compare(this.id, that.id);
  } 
}
```

***StudentsCollectionRunner.java***

```java
package collections;
import java.util.Collections;
import java.util.List;
import java.util.ArrayList;

public class StudentsCollectionRunner {
  public static void main(String[] args) {
    List<Student> students = List.of(new Student(1, "Ranga"),
                    new Student(100, "Adam"),
                    new Student(2, "Eve"));
    ArrayList<Student> studentsAl = new ArrayList<>(students);
    System.out.println(studentsAl);			
    Collections.sort(studentsAl);
    System.out.println(studentsAl);
  }
}
```

***Console Output***

*[1 Ranga, 100 Adam, 2 Eve]*

*[1 Ranga, 2 Eve, 100 Adam]*

##### Snippet-10 解释

`Integer.compare(x, y)`，如果`x == y`，返回0；如果`x < y`，返回小于0的值；如果`x > y`，返回大于0的值。

如果你改变形参的顺序:

```java
@Override
public int compareTo(Student that) {
  return Integer.compare(that.id, this.id);
}
```

输出改变成：

*[100 Adam, 2 Eve, 1 Ranga]*

#### Comparator 接口

如果需要对学生进行多种方式排序，该怎么办？如果我们想要在某些情形下对学生递增排序，在另外一些情形下对学生递减排序该怎么办？

`Collection.sort`有一个重载版本，用法如下：

```java
@SuppressWarnings({"unchecked", "rawtypes" })
public static <T> sort(List<T> list, Comparator<? super T> c)
  list.sort(c);
}
```

为了能调用它，我们需要定义一个合适的对`Student`有作用的`Comparator`实现。

也许你已经猜到了，我们需要定义两个不同的`Comparator`实现：一种递增排序，另一种递减排序。

##### Snippet-11: 实现`Student Comparators`

```java
package collections;
import java.util.Collections;
import java.util.List;
import java.util.ArrayList;
import java.util.Comparator;

class DescStudentComparator implements Comparator<Student> {
  @Override
  public int compare(Student student1, Student student2) {
    return Integer.compare(student2.getId(), student1.getId());		
  }
}
```

```java
public class StudentsCollectionRunner {
  public static void main(String[] args) {
    List<Student> students = List.of(new Student(1, "Ranga"),
                    new Student(100, "Adam"),
                    new Student(2, "Eve"));
    ArrayList<Student> studentsAl = new ArrayList<>(students);
    System.out.println(studentsAl);			
    Collections.sort(studentsAl);
    System.out.println("Ascending : " + studentsAl);
    Collections.sort(studentsAl, new DescStudentComparator());
    System.out.println("Descending : " studentsAl);
  }
}
```

***控制台输出***

*[1 Ranga, 100 Adam, 2 Eve]*

*Ascending : [1 Ranga, 2 Eve, 100 Adam]*

*Descending : [100 Adam, 2 Eve, 1 Ranga]*

#### List 的 sort 方法

你可以传递一个`Comparator`实现来调用`sort`方法 - `studentAl.sort(new AscStudentComparator())` （译者注：原作者应该是忘记在Snippet-11中的第一个代码块里写`AscStudentComparator`了）

##### Snippet-12: ArrayList.sort()的Comparator

```java
package collections;
import java.util.Collections;
import java.util.List;
import java.util.ArrayList;
import java.util.Comparator;

public class StudentsCollectionRunner {
  public static void main(String[] args) {
    List<Student> students = List.of(new Student(1, "Ranga"),
                    new Student(100, "Adam"),
                    new Student(2, "Eve"));

    ArrayList<Student> studentsAl = new ArrayList<>(students);
    System.out.println(studentsAl);
    studentsAl.sort(new AscStudentComparator());
    System.out.println("Asc : " + studentsAl);			
    studentsAl.sort(new DescStudentComparator());
    System.out.println("Desc : " + studentsAl);
  }
}
```

***Console Output***

*[1 Ranga, 100 Adam, 2 Eve]*

*Asc : [1 Ranga, 2 Eve, 100 Adam]*

*Desc : [100 Adam, 2 Eve, 1 Ranga]*

### Set 接口

数学中的`set`是一个由一系列唯一元素组成的集合。相似的，Java中的`Set`接口同样为拥有唯一元素的集合指定了一个标准。

- 如果`object1.equals(object2)`返回`true`，那么`object1`和`object2`在`Set`中只能存在一个。

`Set`不提供访问指定位置元素的方法。

##### Snippet-13: Set

让我们看一些例子：

通过`Set.of()`返回的集合是不可变的，所以不支持`add()`方法。

```java
jshell> Set<String> set = Set.of("Apple", "Banana", "Cat");
set ==> [Banana, Apple, Cat]
```

创建`HashSet`集合替代，它支持`add()`，为了测试`Set`的唯一性。

```java
jshell> set.add("Apple");
| java.lang.UnsupportedOperationException thrown:
jshell> Set<String> hashSet = new HashSet<>(set);
hashSet ==> [Apple, Cat, Banana]
```

`HashSet.add()`操作返回`false`，表示插入一个重复的"Apple"失败了。

```java
jshell> hashSet.add("Apple");
$1 ==> false
jshell> hashSet
hashSet ==> [Apple, Cat, Banana]
```

注意，当使用`set`构造`hashSet`时，元素的顺序改变了 。同样地，当我们通过`Set.of()`创建的`set`，打印出来的顺讯与初始化顺序也不同。说明`Set`集合不重视元素的顺序，所以不支持位置访问。所以，调用`hashSet.add(int, String)`时编译器报错。

```java
jshell> hashSet.add(2, "Apple");
| Error:
| no suitable method found for add(int, java.lang.String)
| hashSet.add(2, "Apple");
|^----------^
jshell>
```

#### 理解数据结构

##### Hash Table

- Hash Table（哈希表）：一种试图结合以下两种特性的数据结构
  - 高效查找元素
  - 高效插入与删除元素
- Buckets（桶）：它们是哈希表中的槽，将元素插入其中并链接在一起。正如你所看到的，哈希表实际上是一个大的bucket数组，每个bucket都包含一个小的链表。
- Hashing（哈希）：构造哈希表的过程称作哈希。术语哈希通常意味着打乱元素的顺序。
- Hashing Function（哈希函数）：用于确定/计算某个特定元素被插入到哪个bucket中的公式。说明：`hash(elem)`能够用数学方法计算`elem mod 13`，并使用该值作为表的索引，以定位桶的插入。`Object.hashCode()`是用了哈希函数。
- Collisions（冲突）：由于bucket中的链表会增加。表越大，哈希函数越好，哈希碰撞的可能性越小。

##### Tree

- Tree（树）：能有序地存储元素。对于树每个节点来说，其左子树中所有节点的元素都小于这个节点包含的元素。相反地，其右子树中所有节点的元素都大于这个节点包含的元素。
- 插入：对于给定的任何节点，我们都可以通过比较新元素和节点的元素来确定插入的位置，从而保持有序性。
- 查找：比链表更高效。

#### Set 的几种实现

- HashSet
- LinkedHashSet
- TreeSet

##### Snippet-14: HashSet

在`HashSet`中，元素既不是按插入顺序存储，也不是按排序顺序存储。

```java
jshell> Set<Integer> numbers = new HashSet<>();
numbers ==> []
jshell> numbers.add(765432);
$1 ==> true
jshell> numbers.add(76543);
$2 ==> true
jshell> numbers.add(7654);
$3 ==> true
jshell> numbers.add(765);
$4 ==> true
jshell> numbers.add(76);
$5 ==> true
jshell> numbers
numbers ==> [765432, 7654, 76, 765, 76543]
jshell>
```

##### Snippet-15: LinkedHashSet

在`LinkedHashSet`中，元素按插入顺序存储

```java
jshell> Set<Integer> numbers = new LinkedHashSet<>();
numbers ==> []
jshell> numbers.add(765432);
$1 ==> true
jshell> numbers.add(76543);
$2 ==> true
jshell> numbers.add(7654);
$3 ==> true
jshell> numbers.add(765);
$4 ==> true
jshell> numbers.add(76);
$5 ==> true
jshell> numbers
numbers ==> [765432, 76543, 7654, 765, 76]
jshell> numbers.add(7654321);
$5 ==> true
jshell> numbers
numbers ==> [765432, 76543, 7654, 765, **7654321**]
jshell>
```

##### Snippet-16: TreeSet

在`TreeSet`中，元素按排序顺序存储。

```java
jshell> Set<Integer> numbers = new TreeSet<>();
numbers ==> []
jshell> numbers.add(765432);
$1 ==> true
jshell> numbers.add(76543);
$2 ==> true
jshell> numbers.add(7654);
$3 ==> true
jshell> numbers.add(765);
$4 ==> true
jshell> numbers.add(76);
$5 ==> true
jshell> numbers
numbers ==> [76, 765, 7654, 76543, 765432]
jshell> numbers.add(7);
$5 ==> true
jshell> numbers
numbers ==> [**7**, 76, 765, 7654, 76543, 765432]
jshell>
```

#### 练习 Set

1. 创建一个字符类型的`List`，比如：

   `List<Character> list = List.of('A', 'Z', 'A', 'B', 'Z', 'F');`

   - 写一个程序列出这个列表中的唯一字符
   - 写一个程序有序列出这个列表中的唯一字符
   - 写一个程序，按照这些它们在原始列表中的顺序列出唯一字符

#### 解题过程

***SetRunner.java***

```java
package collections;
import java.util.List;
import java.util.Set;
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.TreeSet;

public class SetRunner {
  public static void main(String[] args) {
    List<Character> characters = List.of('A', 'Z', 'A', 'B', 'Z', 'F');
    Set<Character> hashSetChars = new HashSet<>(characters);
    System.out.println("Unique Characters: " + hashSetChars);
    Set<Character> treeSetChars = new TreeSet<>(characters);
    System.out.println("Sorted Order: " + treeSetChars);			
    Set<Character> linkedSetChars = new LinkedHashSet<>(characters);
    System.out.println("Inserted Order: " + linkedSetChars);  
  }	
}
```

***Console Output***

*Unique Characters: [A, B, F, Z]*

*Sorted Order: [A, B, F, Z]*

*Inserted Order: [A, Z, B, F]*

#### 解题说明

在这个示例中，遍历`hashSetChars`元素的顺序碰巧和`treeSetChars`相同。正如我们在前面例子中所看到的一样，这样的顺讯并不是总能够得到保证。

#### TreeSet 深度

- 超类接口
  - Set
  - NavigableSet

##### Snippet-16: 操作 NavigableSet

让我们看一些例子：

```java
jshell> TreeSet<Integer> numbers = new TreeSet<>(Set.of(65, 54, 34, 12, 99));
numbers ==> [12, 34, 54, 65, 99]
jshell> numbers.floor(40);
$1 ==> 34
```

`floor()`方法返回小于等于给定元素的最大元素，`lower()`方法返回严格小于给定元素的最大元素

```java
jshell> numbers.floor(34);
$2 ==> 34
jshell> numbers.lower(34);
$3 ==> 12
```

`ceiling()`方法返回大于等于给定元素的最小元素，`higher()`方法返回严格大于给定元素的最小元素

```java
jshell> numbers.ceiling(36);
$4 ==> 54
jshell> numbers.ceiling(34);
$5 ==> 34
jshell> numbers.higher(34);
$6 ==> 54
```

`subSet(Object, Object)`方法不包含边界。所以，左边界类似`lower()`,右边界类似`higher()`。重载的`subSet(Object, boolean, Object, boolean)方法能够决定返回的子集合的左右是否包含边界。

```java
jshell> numbers.subSet(20, 80);
$7 ==> [34, 54, 65]
jshell> numbers.subSet(34, 54);
$8 ==> [34]
jshell> numbers.subSet(34, 65);
$9 ==> [34, 54]
jshell> numbers.subSet(34, true, 65, true);
$10 ==> [34, 54, 65]
jshell> numbers.subSet(34, false, 65, false);
$11 ==> [54]
```

`headSet()`返回严格小于所给元素值的子集合。`tailSet()`返回严格大于所给元素值的子集合。

```java
jshell> numbers.headSet(50);
$12 ==> [12, 34]
jshell> numbers.tailSet(50);
$13 ==> [54, 65, 99]
jshell>
```

### Queue 接口

继承自`Collection`接口

- 元素按照处理顺序排序，就像*To-Do List*

#### PriorityQueue 集合

`PriorityQueue`是Java中的一个内置类，它实现了`Queue`接口。元素默认以自然顺序存储。我们也能指定一个不同的自定义排序，称作*优先级*排序（由程序员定义）

##### Snippet-17: PriorityQueue

`PriorityQueue`队列默认以字母升序存储字符串。

- `queue.poll()`抛出自然顺序的第一个元素

```java
jshell> Queue<String> queue = new PriorityQueue<>();
numbers ==> [12, 34, 54, 65, 99]
jshell> queue.poll();
$1 ==> null
jshell> queue.offer("Apple");
$2 ==> true
jshell> queue.addAll(List.of("Zebra", "Monkey", "Cat"));
$3 ==> true
jshell> queue
queue ==> [Apple, Cat, Monkey, Zebra]
jshell> queue.poll();
$4 ==> "Apple"
jshell> queue
queue ==> [Cat, Monkey, Zebra]
jshell> queue.poll();
$5 ==> "Cat"
jshell> queue.poll();
$6 ==> "Monkey"
jshell> queue.poll();
$7 ==> "Zebra"
jshell> queue.poll();
$8 ==> null
jshell>
```

##### Snippet-18: 自定义优先级的PriorityQuque

通过给`PriorityQueue`构造器传递一个实现了`Comparator<? super T>`接口的对象，可以得到一个自定义优先级的`PriorityQueue`。

让我们来实现`StringLengthComparator`

***QueueRunner.java***

```java
package collections;
import java.util.Comparator;
import java.util.List;
import java.util.Queue;
import java.util.PriorityQueue;

class StringLengthComparator implements Comparator<String> {
  @Override
  public int compare(String left, String right) {
    return Integer.compare(left.length(), right.length());
  }
}

public class QueueRunner {
  public static void main(String[] args) {
    Queue<String> queue = new PriorityQueue<>(new StringLengthComparator());
    queue.addAll(List.of("Zebra", "Monkey", "Cat"));
    queue.poll();
    queue.poll();
    queue.poll();
    queue.poll();
  }
}
```

***控制台输出***

*Cat*

*Zebra*

*Monkey*

*null*

### Map 接口

`Map`接口规定了集合中元素的格式为`(key, value)`（键值对）

假设您想要存储一个字符在一个字符序列中重复的次数。

- 假设序列：`{'A', 'C', 'A', 'C', 'E', 'C', 'M', 'D', 'H', 'A'}`
- map 的内容：`{('A', 3), ('C', 3), ('E', 1), ('M', 1), ('D', 1), ('H', 1)}`

由于存储在map中的元素（键值对）与Java中其他类型的集合不同，`Map`接口是唯一的，它甚至都没有继承`Collection`接口

它接口的定义如下所示：

```java
public interface Map<K, V> {
  //Method Declarations
}
```

- 实现了`Map`接口的Java集合类：
  - `HashMap`
  - `HashTable`
  - `LinkedHashMap`
  - `TreeMap`

#### `Map`集合：概念

- `HashMap`
  - 无序
  - 不可排序
  - 键`hashCode()`的值使用了哈希函数
  - 允许键值为空
- `HashTable`
  - 线程安全版的`HashMap`。它的方法是同步的。
  - 无序
  - 不可排序
  - 键`hashCode()`的值使用了哈希函数
  - 不允许键为`null`
- `LinkedHashMap`
  - 可保持插入元素的顺序（可选的）
  - 无序
  - 遍历很快
  - 插入和删除很慢
- `TreeMap`
  - 额外实现了`NavigableMap`接口
  - 元素以键的顺序排序

#### `Map`接口：基本操作

##### Snippet-19: Map 基本操作

`Map.of()`方法接收一系列对象，这些对象被交替解释为键和值。

- 传入的参数总数应该是一个偶数
- 这个方法创建了不可变的`Map`，它的键值对顺序是无序的。

```java
jshell> Map<String, Integer> map = Map.of("A", 3, "B", 5, "Z", 10);
map ==> {Z=10, A=3, B=5}
jshell> map.get("Z");
$1 ==> 10
jshell> map.get("A");
$2 ==> 3
jshell> map.get("C");
$3 ==> null
jshell> map.size();
$4 ==> 3
jshell> map.isEmpty();
$5 ==> false
jshell> map.containsKey("A");
$6 ==> true
jshell> map.containsKey("F");
$7 ==> false
jshell> map.containsValue(3);
$8 ==> true
jshell> map.containsValue(4);
$9 ==> false
jshell> map.keySet();
$10 ==> [Z, A, B]
jshell> map.values();
$11 ==> [10, 3, 5]
jshell>
```

##### Snippet-20: 可变的Map

为了在一个map中添加值，我们创建一个`HashMap`

```java
jshell> Map<String, Integer> map = Map.of("A", 3, "B", 5, "Z", 10);
map ==> {Z=10, A=3, B=5}
jshell> Map<String, Integer> hashMap = new HashMap<>(map);
hashMap ==> {A=3, Z=10, B=5}
jshell> hashMap.put("F", 5);
$1 ==> null
jshell> hashMap
hashMap ==> {A=3, Z=10, B=5, F=5}
jshell> hashMap.put("Z", 11);
$2 ==> 10
jshell> hashMap
hashMap ==> {A=3, Z=11, B=5, F=5}
jshell>
```

#### Map集合：比较操作

##### Snippet-21: Map 实现

`HashMap`的元素既不是按插入顺序存储，也不是按键的排序顺序存储。

```java
jshell> HashMap<String, Integer> hashMap = new HashMap<>();
hashMap ==> {}
jshell> hashMap.put("Z", 5);
$1 ==> null
jshell> hashMap.put("A", 15);
$2 ==> null
jshell> hashMap.put("F", 25);
$3 ==> null
jshell> hashMap.put("L", 250);
$4 ==> null
jshell> hashMap
hashMap ==> {A=15, F=25, Z=5, L=250}
```

`LinkedHashMap`的元素按插入顺序存储。

```java
jshell> LinkedHashMap<String, Integer> linkedHashMap = new LinkedHashMap<>();
linkedHashMap ==> {}
jshell> linkedHashMap.put("Z", 5);
$5 ==> null
jshell> linkedHashMap.put("A", 15);
$6 ==> null
jshell> linkedHashMap.put("F", 25);
$7 ==> null
jshell> linkedHashMap.put("L", 250);
$8 ==> null
jshell> linkedHashMap
hashMap ==> {Z=5, A=15, F=25, L=250}
```

`TreeMap`元素按键的自然排序顺序存储

#### 练习 Set

1. 对给定的字符串：`"This is an awesom occassion. This has never happened before."`，做如下处理
   - 找出在这个字符串中每个唯一字符的出现次数
   - 找出在这个字符串中每个唯一单词的出现次数

#### 解题

***MapRunner.java***

```java
package collections;
import java.util.Map;
import java.util.HashMap;

public class MapRunner {
  public static void main(String[] args) {
    String str = "This is an awesome occassion. This has never happened before.";
    char[] characters = str.toCharArray();
    Map<Character, Integer> occurrences = new HashMap<>();
    for(char character:characters) {
      Integer count = occurrences.get(character);			
      if(count == null) {
        occurrences.put(character, 1);
      } else {
        occurrences.put(character, count+1);
      }
    }
    System.out.println(occurrences);
    String words = text.split(" ");
    Map<String, Integer> frequency = new HashMap<>();
    for(String word:words) {
      Integer number = frequency.get(word);
      if(number == null) {
        frequency.put(word, 1);
      } else {
        frequency.put(word, number+1);
      }
    }
    System.out.println(frequency);
  }
}
```

#### 回顾 TreeMap

让我们看看基于`TreeMap`数据结构的一些更有趣的操作。

##### Snippet-22: 操作 TreeMap

`TreeMap`中的元素总是排好序的。

```java
jshell> TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap ==> {}
jshell> treeMap.put("F", 25);
$1 ==> null
jshell> treeMap.put("Z", 5);
$2 ==> null
jshell> treeMap.put("L", 250);
$3 ==> null
jshell> treeMap.put("A", 15);
$4 ==> null
jshell> treeMap.put("B", 25)
$5 ==> null
jshell> treeMap.put("G", 25);
$6 ==> null
jshell> treeMap
treeMap ==> {A=15, B=25, F=25, G=25, L=250, Z=5}
```

`TreeMap`也实现了`NavigableMap`接口

```java
jshell> treeMap.higherKey("B");
$7 ==> "F"
jshell> treeMap.higherKey("C");
$8 ==> "F"
jshell> treeMap.ceilingKey("B");
$9 ==> "B"
jshell> treeMap.ceilingKey("C");
$10 ==> "F"
jshell> treeMap.lowerKey("B");
$11 ==> "A"
jshell> treeMap.floorKey("B");
$12 ==> "B"
jshell> treeMap.firstEntry();
$713 ==> A=15
jshell> treeMap.lastentry();
$14 ==> Z=5
jshell> treeMap.subMap("C", "Y");
$7 ==> {F=25, G=25, L=250}
jshell> treeMap.subMap("B", "Z");
$7 ==> {B=25, F=25, G=25, L=250}
jshell> treeMap.subMap("B", true, "Z", true);
$7 ==> {B=25, F=25, G=25, L=250, Z=5}
jshell>
```

### Java 集合：结论与建议

我们研究过的集合接口及其它们的实现类：

- `List`
- `Set`
- `Queue`
- `Map`

让我们快速复习一下之前学习的：

- 当你使用一个Java的“Hashed”集合（基于哈希表），比如`HashMap`或`HashSet`，它是无序的，不可排序的，也不会以特定顺序遍历元素
- 当你遇到一个Java的"Linked"集合（基于链表），比如`LinkedHashSet`或`LinkedHashMap`，它将会按插入顺序存储，但是不可排序。
- 当我们使用一个Java的"Tree"集合（以树的数据结构存储），比如`TreeSet`或`TreeMap`。它总是以自然顺序存储，实现了一个可导航类的接口，比如`NavigableSet`或`NavigableMap`