# 并发：高级主题
让我们创建一个简单的计数器

##### Snippet-1：原子性操作：Counter

***Counter.java***

```java
package com.in28minutes.concurrency;

public class Counter {
  private int i = 0;

  public void increment() {
    i++;
  }

  public int getI() {
    return i;
  }
}
```

***ConcurrencyRunner.java***

```java
package com.in28minutes.concurrency;

public class ConcurrencyRunner {
  public static void main(String[] args) {
    Counter counter = new Counter();
    counter.increment();
    counter.increment();
    counter.increment();			
    System.out.println(counter.get());
  }
}
```

##### Snippet-1 说明

很简单！

#### Counter`increment()`方法非原子性的！

它似乎只涉及一个操作。

```java
public void increment() {
  i++;
}
```

`i++`操作实际上涉及到下面的步骤：

- 步骤1 将`i`的值从内存读入CPU寄存器
- 步骤2 增加CPU寄存器中的值
- 步骤3 将增加后的值存回`i`的内存位置

`i++`不是一个原子性操作。

##### 如果`increment`不是原子性的怎么办？

让我们以两个线程为例，在`ConcurrencyRunner`中运行的`T1`和`T2`两个线程访问同一个`Counter`对象实例。

假设两个线程并发调用`increment`方法和`getI`方法。

假定`i`初始值为`15`。让我们仔细思考一下一种可能的情况：

- `T1`先调用`increment()`方法，并且成功完成`i++`的步骤1。得到15这个值。
- 调度器切换到`T2`线程。
- `T2`先调用`increment()`方法，并且成功完成`i++`的步骤1。得到15这个值。
- 调度器切回到`T1`。`T1`继续执行`increment()`方法，并完成了`i++`的步骤2和3。`increment()`执行结束。`i`的值被`16`覆盖。
- 调度器切回到`T2`。在它的CPU寄存器上下文中，`i = 15`，不是`16`。`T2`继续执行`increment()`，并完成了`i++`的步骤2和3。`increment()`执行结束。这个`Counter`实例的`i`值被`16`覆盖。

理想情况下，执行了两次`increment()`方法后的`i`值应该是`17`。当操作一个接一个地连续执行时，才会出现这种情况。

并发计算（涉及到一系列操作）的结果取决于多个线程执行这些操作的相对顺序的情形叫**竞争条件**。（译者注：[竞争冒险](https://zh.wikipedia.org/wiki/%E7%AB%B6%E7%88%AD%E5%8D%B1%E5%AE%B3)）

这是一句流行的英语谚语：“事情往往功败垂成。” 这指的是这样一个事实，在我们手里拿着一杯茶到喝一口茶的这段时间里，任何事情都有可能发生。

这绝对是真的。

递增操作实际上并不像看上去那么顺利。因为它是非原子性的，所以经常会出现错误。这就引出了**线程安全**这个概念。

如果一个方法可以在没有竞争条件的并发环境(涉及多个独立线程的并发调用)中运行，那么这个方法就是线程安全的。

#### 回顾：synchronized 关键字

在一个`class`方法的签名中添加`synchronized`关键字可以使它成为线程安全的。

##### Snippet-2

***Counter.java***

```java
package com.in28minutes.concurrency;

public class Counter {
  private int i = 0;

  synchronized public void increment() {
    i++;
  }

  public int getI() {
    return i;
  }
}
```

##### Snippet-2 说明

在给`increment()`方法添加了`synchronized`关键字后，在同一时刻只有一个线程能执行这个方法。所以避免了竞争条件。

##### Snippet-3 更少的并发性

`synchronized`关键字保证了代码的线程安全。但是，它会让所有其他的线程等待。这会导致性能问题。让我们看一个例子：

***BiCounter.java***

```java
package com.in28minutes.concurrency;

public class BiCounter {
  private int i = 0;
  private int j = 0;

  synchronized public void incrementI() {
    i++;
  }

  synchronized public void incrementJ() {
    j++;
  }

  public int getI() {
    return i;
  }

  public int getJ() {
    return j;
  }
}
```

***ConcurrencyRunner.java***

```java
package com.in28minutes.concurrency;

public class ConcurrencyRunner {
  public static void main(String[] args) {
    BiCounter counter = new BiCounter();
    counter.incrementI();
    counter.incrementJ();
    counter.incrementI();
    System.out.println(counter.get());
  }
}
```

##### Snippet-3 说明

`BiCounter`类的`incrementI()`和`incrementJ()`方法都是`synchronized`的。所以，在任何时间段，最多只有一个线程去执行这两个方法的其中之一。这意味着，当线程`T1`在`ConcurrencyRunner.main()`中执行`counter.incrementI()`方法时，另外一个线程`T2`不允许执行`counter.incrementJ()`！

简单地想一下，总共有`12`个线程想要执行`counter`的递增方法。当一个线程在运行时，其他`11`个线程不得不等待。

#### 用锁同步

让我们看看另一个同步选择 - `Locks`

##### Snippet-4：BiCounter 使用 Locks

***BiCounterWithLocks.java***

```java
package com.in28minutes.concurrency;
import java.util.concurrent.locks.ReentrantLock;

public class BiCounterWithLocks {
  private int i = 0;
  private int j = 0;
  private Lock LockForI = new ReentrantLock();
  private Lock LockForJ = new ReentrantLock();

  public void incrementI() {
    lockForI.lock();
    i++;
    lockForI.unlock();
  }

  public void incrementJ() {
    lockForJ.lock();
    j++;
    lockForJ.unlock();
  }

  public int getI() {
    return i;
  }

  public int getJ() {
    return j;
  }
}
```

##### Snipper-4 说明

`i++`和`j++`是一段需要保护的代码。我们使用了两个锁`lockForI`和`lockForJ`。如果一个线程想要执行`i++`，它首先需要获得一把锁 - 通过使用`lockForI.lock()`实现。一旦执行了这个操作，它能使用`lockForI.unlock()`释放这把锁。

`lockForI`和`lockForJ`相互之间完全独立。所以，线程`T2`可以执行`incrementJ()`中的`j++`，同时，线程`T1`可以执行`incrementI()`中的`i++`。

#### 原子类

`i++`这个操作虽然看起来很简单，确实让我们有点头疼！

一个看似微小的操作可能需要考虑很多东西，想象一下，编写并发数据结构，用多个链接操作操作链表。

如果有人能帮我们处理这些微小的操作就好了，否则我们将很难找出哪些代码必须锁定，哪些代码不需要锁定!

Java通过提供了一些本质上线程安全的类， 为基本数据类型解决了这个问题。`AtomicInteger`是一个好例子，它是`int`基本类型的装饰器。

##### Snippet-5：AtomicInteger

***BiCounterWithAtomicInteger.java***

```java
package com.in28minutes.concurrency;
import java.util.concurrent.atomic.AtomicInteger;

public class BiCounterWithAtomicInteger {
  private AtomicInteger i = new AtomicInteger();
  private int AtomicInteger = new AtomicInteger();

  public void incrementI() {
    i.incrementAndGet();
  }

  public void incrementJ() {
    j.incrementAndGet();
  }

  public int getI() {
    return i.get();
  }

  public int getJ() {
    return j.get();
  }
}
```

##### Snippet-5 说明

`incrementAndGet`是原子性的。所以，`BiCounterWithAtomicInteger`不需要担心同步问题。

#### 并发集合

Java为我们提供了现成的基本数据类型线程安全解决方案，通过使用类似`AtomicInteger`的装饰器。这种方法对`int`有用的原因是：

- 简单，小型的基本类型
- 广泛的使用可能性

集合该怎么办呢？

Java提供了线程安全的`Vector`类（`ArrayList`的同步版）。但它仍有使用`synchronized`的问题。

还有其他选择吗？

##### Snippet-6：需要使用ConcurrentMap 

下面代码的`for`循环做了一次`get`然后做了一次`put`。这样是线程不安全的。

***MapRunner.java***

```java
package com.in28minutes.collections;
import java.util.HashMap;

public class MapRunner {
  public static void main(String[] args) {
    String str = "Hello World";
    Map<Character, Integer> occurrences = new HashMap<>();
    char[] characters = str.toCharArray();
    for(char character:characters) {
      Integer count = occurrences.get(character);
      if(count == null) {
        occurrences.put(character, 1);
      } else {
        occurrences.put(character, count + 1);
      }
    }
  }
}
```

并发集合提供了上述操作的原子版本。

- 如果条目不存在，那就创建和初始化条目
- 如果条目存在，那就更新条目

#### ConcurrentMap 接口

`CouncurrentMap`接口有实现复合操作的方法。这些操作包括：

```
V putIfAbsent(K key, V value);

V computeIfPresent(K key,
            BiFunction<? super K, ? super V, ? extends V> remappingFunction)
```

##### Snippet-7：ConcurrentHashMap 逻辑-阶段1

`LongAdder`提供了原子性`increment`方法，使用这个方法让代码的线程变得更安全一些。

***ConcurrentMapRunner.java***

```java
package com.in28minutes.concurrency;
import java.util.Map;
import java.util.Hashtable; // (译者注，原文错误，HashTable)
import java.util.concurrent.atomic.LongAdder;

public class ConcurrentMapRunner {
  public static void main(String[] args) {
        String str = "ABCD ABCD ABCD";
    		Map<Character, LongAdder> occurances = new Hashtable<>(); // （译者注：原文漏写）
        for(char character:str.toCharArray()) {
          LongAdder longAdder = occurances.get(character);
          if(longAdder == null) {
            longAdder = new LongAdder();
          }
          longAdder.increment();
          occurances.put(character, longAdder);
        }
    		System.out.println(occurances); // (译者注：原文漏写)
  }
}
```

***控制台输出***

*[ =2, A=3, B=3, C=3, D=3]* (译者注，原文D=2是错误的)

##### Snippet-8：ConcurrentHashMap 逻辑-阶段2

我们可以用`ConcurrentHashMap`集合中的`computeIfAbsent()`方法将代码简化成单一原子性操作。

***ConcurrentMapRunner.java***

```java
package com.in28minutes.concurrency;
import java.util.concurrent.ConcurrentMap;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.atomic.LongAdder;

public class ConcurrentMapRunner {
  public static void main(String[] args) {
      ConcurrentMap<Character, LongAdder> occurances = new ConcurrentHashMap<>();

      String str = "ABCD ABCD ABCD";

      for(char character:str.toCharArray()) {
        occurances.computeIfAbsent(character, ch -> new LongAdder()).increment();
      }

      System.out.println(occurances);
  }
}
```

***控制台输出***

*[ =2, A=3, B=3, C=3, D=3]* （译者注：原文D=2是错误的）

#### ConcurrentHashMap

`Hashtable`中所有的方法都是同步的。

`ConcurrentHashMap`中的数据结构被设计成是互不相交的区域。访问方法为不同的区域使用了不同的`Locks`，以此减少在并发访问这些区域时对性能的影响。

#### 并发集合：写时拷贝优化

所有写时拷贝集合的值都存在一个内部不可变的数组中。如果集合有任何改变，就会创建一个新的数组。

读操作不是同步的。只有写操作才是同步的。

写时拷贝方法用在当一个集合的读操作次数远大于写操作时的情况。

`CopyOnWriteArrayList` & `CopyOnWriteArraySet`实现了这个方法。

写时拷贝集合通常用于观察者模式，观察者很少改变。最频繁的操作是遍历观察者并通知他们。

##### Snippet-9：CopyOnWriteArrayList

***CopyOnWriteArrayListRunner.java***

```java
package com.in28minutes.concurrency;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteArrayListRunner {
  public static void main(String[] args) {
    List<String> list = new CopyOnWriteArrayList<>();
    // Total of 3 threads doing add()'s, maybe in a separate method
    list.add("Ant");
    list.add("Bat");
    list.add("Cat");

    //Total of 10000 threads looping on get(), again, in a separate method
    for(String element:list) {
      System.out.println(element);
    }
  }
}
```

##### Snippet-9 说明

`CopyOnWriteArrayList.add()`是一个同步方法。而且写时拷贝算法保证了是以线程安全的方式进行拷贝的，然后在另一个副本上进行写操作，而`add()`(译者注：原文为`get()`，应该是不对的)继续处理原始数组。一旦`add()`方法结束，集合开始使用新数组，然后把就数组丢弃。这种策略将在程序的生命周期中持续。

`CopyOnWriteArrayList.get()`方法是非同步的，由于读操作在数组中起作用，所以不会直接通过`add()`进行写操作。

写时复制集合应该只用于特定的使用场景，即与更改(数据元素插入/删除/修改)相比，需要进行大量的数据结构（数据元素只读）遍历。通过这种方式，遍历可以实现高并发性。

