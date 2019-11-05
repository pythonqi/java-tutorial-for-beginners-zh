# 线程与并发

目前为止，我们只看到过像一匹马一样在跑道上奔跑的程序。

但是把一个程序的主任务切分成更小的任务（我们称它们为子任务）通常是很有用的。

想想一个蚁群，在那里有大量的工蚁协同工作，完成蚁后让它们做的事。每一群蚂蚁都是独立任务的一部分，各自完成自己的工作。

编程中**并发**的概念与蚁群的本质非常相似。

### 01：并发任务：继承Thread

在Java中，可以使用线程并行地运行任务。先写个简单的程序。

##### Snippet-1

***ThreadBasicsRunner.java***

```java
public class ThreadBasicsRunner {
  public static void main(String[] args) {
    //Task1
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\n Task1 Done");

    //Task2
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");
    }

    System.out.println("\n Task2 Done");
    //Task3
    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");			
    }
    System.out.println("\n Task3 Done");

    System.out.println("Main Done");
  }
}
```

***控制台输出***

*101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199*

*Task1 Done*

*201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297 298 299*

*Task2 Done*

*301 302 303 304 305 306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399*

*Task3 Done*

*Main Done*

##### Snippet-1 说明

正如你所看到的的，这三个`for`循环（实际上独立的任务）的执行是连续的。到目前为止，我们所有的代码都是这样运行。

### 线程创建

在一个程序中，有两种方法可以创建线程来表示子任务。它们是：

- 定义你自己的线程类作为**`Thread`**类的子类
- 定义你自己的实现了**`Runnable`**接口的线程类

在这一节中，我们将集中讨论第一种选择。

##### Snippet-01：一个简单的Java线程类

***ThreadBasicsRunner.java***

```java
class Task1 extends Thread {
  public void run() {
    System.out.println("Task1 Started ");
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask1 Done");
  }	
}

public class ThreadBasicsRunner {
  public static void main(String[] args) {
    //Task1
    Task1 task1 = new Task1();
    task1.start();

    //Task2
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask2 Done");

    //Task3
    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask3 Done");
    System.out.println("\nMain Done");
  }	
}
```

***控制台输出***

```
Task1 Started 
201 101 202 102 203 103 204 104 105 205 206 106 207 107 208 108 209 109 210 110 211 111 212 112 213 113 214 114 215 115 216 116 217 218 117 219 118 220 119 221 120 222 121 122 223 123 224 124 225 125 226 126 227 127 228 128 229 129 230 130 231 131 232 132 233 133 234 134 235 135 236 136 237 137 238 138 239 139 240 140 241 141 242 142 243 143 244 144 245 145 246 247 146 248 147 249 148 250 149 251 150 252 151 253 152 254 153 255 154 256 155 257 156 258 157 259 158 260 159 261 160 262 161 263 162 264 163 265 164 266 165 267 166 268 167 269 168 270 169 271 170 272 171 273 172 274 173 275 174 276 175 277 278 279 176 280 177 281 178 179 282 180 181 182 283 183 284 184 285 185 286 186 287 187 288 289 188 290 189 291 190 292 191 293 192 294 193 194 295 195 196 296 197 297 298 299 198 
Task2 Done
301 199 302 
Task1 Done
303 304 305 306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399 
Task3 Done

Main Done
```

##### Snippet-01 说明

我们定义了一个`Task1`类来表示子任务，这个类中定义了`run()`方法。虽然我们在`main()`方法中创建了它的一个线程，但我们似乎没有以任何方式调用`run()`方法。这里发生了什么呢？

可以通过调用名为`start()`的通用方法来创建和使用线程。调用`start()`方法将会调用线程的`run()`方法。

通过控制台输出，我们看到*Task1*的输出与标记为*Task2*和*Task3*任务的输出重叠。运行`Task1`线程和运行`Task2`，`Task3`的主线程并行运行。

#### 总结

在这一节中，我们：

- 发现了如何通过继承`Thread`类来定义子线程类
- 演示了如何运行线程

### 02：并行任务 - 实现 Runnable

##### Snippet-01：实现Runnable

在**小节01**中，我们告诉你在Java程序中线程有两种方式表示子任务。一种方式是继承`Thread`，另一种方式是实现`Runnable`接口。我们刚才看到了第一种方式，现在是时候探索第二种方式了。下面的示例向你展示是如何实现的。

***ThreadBasicsRunner.java***

```java
class Task1 extends Thread {
  public void run() {
    System.out.println("Task1 Started ");
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask1 Done");
  }
}

class Task2 implements Runnable {
  @Override
  public void run() {
    System.out.println("Task2 Started ");
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");		
    }
    System.out.println("\nTask2 Done");
  }
}

public class ThreadBasicsRunner {
  public static void main(String[] args) {
    System.out.print("\nTask1 Kicked Off\n");
    Task1 task1 = new Task1();
    task1.start();

    System.out.print("\nTask2 Kicked Off\n");
    Task2 task2 = new Task2();
    Thread task2Thread = new Thread(task2);
    task2Thread.start();

    System.out.print("\nTask3 Kicked Off\n");
    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask3 Done");

    System.out.println("\nMain Done");
  }
}
```

***控制台输出***

```
Task1 Kicked Off
Task1 Started 
101 102 103 104 105 106 107 108 109 110 111 
Task2 Kicked Off
112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 
Task1 Done

Task3 Kicked Off
Task2 Started 
201 202 203 204 205 206 207 208 209 210 211 212 213 301 214 215 216 217 218 302 219 220 221 222 223 224 225 226 227 228 303 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 304 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 305 287 288 289 290 291 292 293 294 295 296 297 298 299 
Task2 Done
306 307 308 309 310 311 312 313 314 315 316 317 318 319 320 321 322 323 324 325 326 327 328 329 330 331 332 333 334 335 336 337 338 339 340 341 342 343 344 345 346 347 348 349 350 351 352 353 354 355 356 357 358 359 360 361 362 363 364 365 366 367 368 369 370 371 372 373 374 375 376 377 378 379 380 381 382 383 384 385 386 387 388 389 390 391 392 393 394 395 396 397 398 399 
Task3 Done

Main Done
```

##### Snippet-01 说明

在本示例中，我们通过实现`Runnable`接口中的`run()`方法实现了`Runnable`接口。

为了运行已实现`Runnable`接口的`Task2`，我们使用了下面的代码。我们将`Task2`类的实例传递给了`Thread`构造器。

```java
Task2 task2 = new Task2();
Thread task2Thread = new Thread(task2);
task2Thread.start();
```

你可以从输出结果看出所有的三个任务都是并行运行的。

#### 总结

在这一节中，我们：

- 学习了另外一种创建线程的方式，通过实现`Runnable`接口
- 学习了运行使用`Runnable`接口创建的线程

### 03：线程的生命周期

Java线程在其存活时间中经历一系列状态。使用**生命周期**这个术语来描述这个事实，并明确地定义了线程在不同时间点的具体状态。

让我们思考下面这段刚刚在**小节02**中探究的示例：

```java
class Task1 extends Thread {
  public void run() {
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
  }	
}

class Task2 implements Runnable {
  @Override
  public void run() {
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");
    }
  }
}

public class ThreadBasicsRunner {
  public static void main(String[] args) {
    Task1 task1 = new Task1();
    task1.start();
    Task2 task2 = new Task2();
    Thread task2Thread = new Thread(task2);
    task2Thread.start();
    for(int i=301; i<=399; i++) {			
      System.out.print(i + " ");
    }
  }
}
```

线程的不同状态：

- **NEW**：线程一创建就处于这种状态，但是它还没有调用`start()`方法。
  - 对于 *Task1* 来说：执行`Task1 task1 = new Task1();`之后
  - 对于 *Task2* 来说：执行`Task2 task2 = new Task2(); task2Thread = new Thread(task2);`之后
- **TERMINATED/DEAD**：当一个线程`run()`方法里的所有语句执行完毕，称这个线程结束。

在一个线程调用了`start()`方法以后，它可以处于其余三种状态的任何一种。

- **RUNNING**：如果线程当前正在运行。
- **RUNNABLE**：如果线程当前没有运行，但是已经准备好可以随时运行。
- **BLOCKED/WAITING**：如果线程没在处理器上运行，也没有准备好运行。如果它正在等待外部资源(例如用户的输入)或另一个线程，可能会出现这种情况。

#### 总结

在这一节中，我们：

- 通过一个示例讨论了线程的不同状态

### 04：线程优先级

Java允许你请求线程调度程序，以改变线程的优先级。所有线程的优先级总是处于一个固定的范围中 - `MIN_PRIORITY = 1` 到 `MAX_PRIORITY = 10`。任何线程默认的优先级是`NORM_PRIORITY = 5`。

可以通过`Thread`类的静态方法`setPriority(int)`请求改变线程的优先级。这个请求可能会得到响应，也可能不会得到响应，所以要做好准备!

### 05：线程通信

任何没有显式创建线程的程序都是单线程应用程序。我们这里指的线程是*主线程*，用来执行程序的`main()`方法。

看一下**小节02**中的例子。我们增加一个条件 — *Task3* 在 *Task1* 结束之后执行。

***ThreadBasicsRunner.java***

```java
class Task1 extends Thread {
  public void run() {
    System.out.println("Task1 Started ");
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
  }
}

class Task2 implements Runnable {
  @Override
  public void run() {
    System.out.println("Task2 Started ");
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask2 Done");
  }
}

public class ThreadBasicsRunner {
  public static void main(String[] args) {
    System.out.print("\nTask1 Kicked Off\n");
    Task1 task1 = new Task1();		
    task1.start();
    System.out.print("\nTask2 Kicked Off\n");
    Task2 task2 = new Task2();
    Thread task2Thread = new Thread(task2);
    task2Thread.start();

    task1.join();

    System.out.print("\nTask3 Kicked Off\n");
    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask3 Done");
    System.out.println("\nMain Done");
  }
}
```

##### Snippet-5 说明

`task1.join()`会一直等待直到`task1`完成。所以，在`task.join()`后面的代码只有在`task1`完成后才会执行。

如果我们要 *Task3* 在 *Task1* 和 *Task2* 都完成后执行，在`main()`方法里的代码需要写成下面这样：

##### Snippet-6：Task3 在 Task1 和 Task2 后执行

***ThreadBasicsRunner.java***

```java
public static void main(String[] args) {
  System.out.print("\nTask1 Kicked Off\n");
  Task1 task1 = new Task1();
  task1.start();

  System.out.print("\nTask2 Kicked Off\n");
  Task2 task2 = new Task2();
  Thread task2Thread = new Thread(task2);
  task2Thread.start();

  task1.join();
  task2Thread.join();

  System.out.print("\nTask3 Kicked Off\n");
  for(int i=301; i<=399; i++) {
    System.out.print(i + " ");
  }
  System.out.println("\nTask3 Done");
  System.out.println("\nMain Done");

}
```

##### Snippet-6 说明

需要注意的是，*Task1*和*Task2*仍然是独立的子任务。线程调度器自由地交错执行它们。但是，*Task3*只有它们都结束之后才开始执行。

#### 总结

在这一节中，我们：

- 了解了线程间需要通信
- 了解到Java为线程提供了相互等待的机制
- 观察到如何使用`join()`方法对线程执行顺序排序

### 07：synchronized 方法，与线程的实用程序

当一个线程感到累了，你可以把它放到床上。见鬼，你甚至可以在它处于新生状态和渴望运行状态时那么做。它由你控制，记住了吗？

`Thread`类提供了一些方法：

- `public static native void sleep(int millis)`：调用这个方法会导致线程出现问题，进入*阻塞/等待*状态**至少**`millis`毫秒。
- `public static native void yield()`：请求线程调度器去执行其他的线程。调度器可以忽略这些请求。

##### Snippet-7：线程实用程序

```java
jshell> Thread.sleep(1000)

jshell> Thread.sleep(10000)

jshell>
```

##### Snippet-7 说明

- `Thread.sleep(1000)`导致`jshell`提示符在*至少*延迟了1秒后出现。当执行`Thread.sleep(10000)`，这个延迟更加明显。

### 08：前面方法的缺点

我们在`Thread`类中看到的几个同步方法：

- `start()`
- `join()`
- `sleep()`
- `wait()`

上面的方法有几点不足：

- **无粒度控制**：假设，比如我们要 *Task3* 在 *Task1* 和 *Task2* 任意一个完成后执行。我们该怎么做？
- **难以维护**：想象一下用前面例子中写的代码去管理5-10个线程。这会很难维护。
- **没有子任务返回机制**：使用`Thread`类或`Runnable`接口，都无法从子任务中获得结果。

### 09：ExecutorService 介绍

为了解决`Thread`API的严重限制，Java SE 5添加了新的`Executor Service`。

`ExecutorService`是一个框架，你可以用它更好地管理代码中的线程。它的内置方法用来：

- 更直观地创建和启动线程
- 更方便地管理线程状态和它的生命周期
- 控制线程间同步
- 更简洁地处理线程组

`ExecutorService`提供了实用程序来实现它们。让我们以线程创建开始，下一个示例将处理线程创建。

##### Snippet-01 : 创建线程

***ExecutorServiceRunner.java***

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Task1 extends Thread {
  public void run() {
    System.out.println("Task1 Started ");
    for(int i=101; i<=199; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask1 Done");
  }
}

class Task2 implements Runnable {
  @Override
  public void run() {
    System.out.println("Task2 Started ");
    for(int i=201; i<=299; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask2 Done");
  }
}


public class ExecutorServiceRunner {
  public static void main(String[] args) {
    ExecutorService executorService = Executors.newSingleThreadExecutor();
    executorService.execute(new Task1());
    executorService.execute(new Thread(new Task2()));
  }
}
```

***控制台输出***

*Task1 Started*

*101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199*

*Task1 Done*

*Task2 Started*

*201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 267 268 269 270 271 272 273 274 275 276 277 278 279 280 281 282 283 284 285 286 287 288 289 290 291 292 293 294 295 296 297 298 299*

*Task2 Done*

##### Snippet-01 说明

`ExecutorService executorService = Executors.newSingleThreadExecutor()`创建了一个单线程执行服务。这就是为什么任务一个接一个地串行运行的原因。

##### Snippet-02：main 并行运行

更新main方法来做更多的事：

```java
public class ExecutorServiceRunner {
  public static void main(String[] args) {
    ExecutorService executorService = Executors.newSingleThreadExecutor();
    executorService.execute(new Task1());
    executorService.execute(new Thread(new Task2()));
    System.out.print("\nTask3 Kicked Off\n");

    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask3 Done");
    System.out.println("\nMain Done");
    executorService.shutdown();
  }
}
```

***控制台输出***

```
Task1 Started 
101 
Task3 Kicked Off
102 301 103 302 104 303 105 304 106 305 107 306 108 109 110 111 112 307 113 114 115 116 117 118 119 120 121 122 308 123 309 124 310 125 311 126 312 127 313 128 314 129 315 130 316 131 132 133 317 134 318 135 319 136 137 320 138 321 139 322 140 323 141 324 142 325 143 326 144 145 146 147 327 148 149 328 150 329 151 330 152 331 332 153 154 155 156 157 158 159 160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 180 181 182 183 184 185 186 187 188 189 190 191 192 193 333 194 334 195 196 335 197 198 199 336 
Task1 Done
337 338 Task2 Started 
339 201 202 203 204 205 206 207 340 341 208 209 210 211 212 213 214 215 216 217 218 219 220 342 221 222 223 224 225 343 344 226 345 346 227 347 348 228 229 349 230 231 232 350 233 351 352 234 235 236 237 238 239 240 241 242 243 244 245 246 247 248 353 249 354 355 250 356 251 357 358 252 359 253 360 254 255 361 256 362 363 257 258 364 259 365 366 260 367 261 262 368 263 264 369 265 370 266 371 267 268 372 269 373 270 374 375 271 376 377 272 378 273 379 274 380 275 381 382 276 277 383 278 384 279 385 386 280 387 281 388 282 283 284 389 285 390 391 286 392 287 393 288 394 395 289 396 290 397 291 398 399 
Task3 Done

Main Done
292 293 294 295 296 297 298 299 
Task2 Done
```

##### Snippet-02 说明

我们在这个混乱的结果中看到唯一有序的是：*Task2*在*Task1*完成后开始执行。

由`ExecutorService`管理的线程与`main`方法并行运行。

### 10：Excutor - 自定义线程数

使用`ExecutorService`，可以创建线程池。

##### Snippet-03：并发线程执行器

***ExecutorServiceRunner.java***

```java
public class ExecutorServiceRunner {
  public static void main(String[] args) {
    ExecutorService executorService = Executors.newFixedThreadPool(2);
    executorService.execute(new Task1());
    executorService.execute(new Thread(new Task2()));
    System.out.print("\nTask3 Kicked Off\n");

    for(int i=301; i<=399; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask3 Done");
    System.out.println("\nMain Done");
    executorService.shutdown();
  }
}
```

***控制台输出***

```
Task1 Started 

Task3 Kicked Off
301 101 302 303 304 Task2 Started 
305 306 102 307 103 201 104 308 105 202 106 309 107 203 108 310 109 110 204 111 311 112 205 113 312 114 206 115 313 116 207 117 314 118 208 119 315 120 209 121 316 122 210 317 211 123 212 318 213 124 125 126 127 128 319 129 320 214 321 130 322 215 323 131 324 216 325 132 326 217 327 133 328 218 329 134 330 219 331 135 332 220 333 136 334 221 335 137 336 222 337 138 338 223 339 139 340 224 341 140 342 225 343 141 344 226 345 142 346 227 347 143 228 348 144 349 229 350 145 351 230 352 146 353 231 354 147 355 232 356 148 357 233 358 149 359 234 360 150 361 235 362 151 363 236 364 237 152 238 365 239 153 240 366 241 242 154 243 367 244 155 245 368 246 156 157 247 369 248 158 249 370 250 159 251 252 253 254 255 256 257 258 259 260 261 262 263 264 265 266 371 267 372 373 374 268 269 160 270 271 375 376 377 378 379 380 381 382 383 161 162 163 164 165 384 166 272 167 168 169 170 171 172 385 173 386 387 273 388 389 174 390 391 274 392 175 393 275 394 176 395 276 396 397 177 398 178 179 277 180 399 181 278 182 183 
Task3 Done

Main Done
184 185 279 280 281 282 283 186 187 284 285 286 188 189 287 288 289 190 191 290 192 291 193 292 194 293 195 196 294 295 296 297 298 299 
Task2 Done
197 198 199 
Task1 Done
```

##### Snippet-03 说明

我们用`Executors.newFixedThreadPool(2)`创建了`ExecutorService`。所以`ExecutorService`最多可使用两个并行线程。

- *Task1* 和 *Task2* 作为`ExecutorService`的一部分，并发执行
- 运行`main()`的线程与这个由`ExecutorService`创建的线程池并发执行

##### Snippet-04：All-Executor 执行任务

看一个关于`ExecutorService`的例子

***ExecutorServiceRunner.java***

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Task extends Thread {
  private int number;

  public Task(int number) {
    this.number = number;
  }

  public void run() {
    System.out.println("Task " + number + " Started");
    for(int i=number*100; i<=number*100+99; i++) {
      System.out.print(i + " ");
    }
    System.out.println("\nTask " + number +" Done");
  }
}

public class ExecutorServiceRunner {
  public static void main(String[] args) {
    ExecutorService executorService = Executors.newFixedThreadPool(2);
    executorService.execute(new Task(1));
    executorService.execute(new Task(2));
    executorService.execute(new Task(3));
    executorService.shutdown();
  }
}
```

##### Snippet-04 说明

`Executors.newFixedThreadPool(2)` - 两个线程并发运行。`new Task(3)`线程只会在`new Task(1)`和`new Task(2)`中的任意一个执行完毕后才会运行。

##### Snippet-05 更大的线程池

```java
public class ExecutorServiceRunner {
  public static void main(String[] args) {
    ExecutorService executorService = Executors.newFixedThreadPool(3);
    executorService.execute(new Task(1));
    executorService.execute(new Task(2));
    executorService.execute(new Task(3));
    executorService.execute(new Task(4));
    executorService.execute(new Task(5));
    executorService.execute(new Task(6));
    executorService.execute(new Task(7));
    executorService.shutdown();
  }
}
```

##### Snippet-05 说明

我们将线程池增大到3：

- 一开始Task `1`，`2`，`3`被加到`ExecutorService`中并开始执行
- 一旦其中任何一个线程结束，就会执行线程池中的另一个任务，以此往复。关于`ExecutorService`线程池中可用的线程，一个典型的音乐椅案例！

#### 总结

在这一节中，我们：

- 探究了如何使用`ExecutorService`创建同类线程池
- 说明了如何指定线程池的大小

### 11：ExecutorService：返回值的任务

##### Snippet-01：返回一个Future对象

到目前为止，我们只看到了基本独立的子任务，它们不会向启动它们的主程序返回任何结果。

为了能让线程返回值，Java提供了`Callable<T>`接口。

下一个示例告诉你如何实现`Callable<T>`接口，并将其与`ExecutorService`一起使用。

***ExecutorServiceRunner.java***

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Callable;

class CallableTask implements Callable<String> {
  private String name;

  public CallableTask(String name) {
    this.name = name;
  }

  @Override
  public String call() throws Exception {
    Thread.sleep(1000);
    return "Hello " + name;
  }
}

public class CallableRunner {
  public static void main(String[] args) throws InterruptedException, ExecutionException {
    ExecutorService executorService = Executors.newFixedThreadPool(1);
    Future<String> welcomeFuture = executorService.submit(new CallableTask("in28Minutes"));
    System.out.println("CallableTask in28Minutes Submitted");
    String welcomeMessage = welcomeFuture.get();
    System.out.println(welcomeMessage);
    executorService.shutdown();
  }
}
```

***控制台输出***

*CallableTask in28Minutes Submitted*

*Hello in28Minutes*

##### Snippet-01 说明

- `class CallableTask implements Callable<String>` - 实现了`Callable`接口。返回`String`类型
- `public String call() throws Exception {` - 实现了`call`方法并返回了一个`String`类型的值
- `executorService.submit(new CallableTask(String))`在线程池中增加了一个可调用的任务，让任务线程处于**RUNNABL**状态。随后，程序继续调用它的`call()`方法。
- `welcomeFuture.get()` - 确保`main`线程等待操作的结果。

#### 总结

在这一节中，我们：

- 了解了创建返回值的子任务机制的需求
- 发现了Java确实有一个`Callable<T>`接口来满足这个需求
- 知道了`ExecutorService`能管理`Callable`线程

### 12：Executors - 等待多个Callable任务完成

`ExecutorService`框架也允许你创建`Callable`线程池。不仅如此，你能一起收集它们的返回值。

##### Snippet-01：等待多个Callable线程

***MultipleCallableRunner.java***

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Callable;

class CallableTask implements Callable<String> {
  private String name;

  public CallableTask(String name) {
    this.name = name;
  }

  @Override
  public String call() throws Exception {
    Thread.sleep(1000);
    return "Hello " + name;
  }
}

public class MultipleCallableRunner {
  public static void main(String[] args) throws InterruptedException, ExecutionException {
    ExecutorService executorService = Executors.newFixedThreadPool(1);
    List<CallableTask> tasks = List.of(new CallableTask("in28Minutes"),
                      new CallableTask("Ranga"),
                      new CallableTask("Adam"));
    List<Future<String>> welcomeAll = executorService.invokeAll(tasks);
    for(Future<String> welcomeFuture : welcomeAll) {
      System.out.println(welcomeFuture.get());
    }
    executorService.shutdown();
  }
}
```

***控制台输出***

*Hello in28Minutes*

*Hello Ranga*

*Hello Adam*

##### Snippet-01 说明

`ExecutorService`的 `invokeAll()`方法允许在线程池中启动`Callable`任务列表。另外，可以使用`Future`对象的列表来保存返回值，每个返回值对应一个`Callable`线程。

只有当所有的线程结束并且已经返回了它们的结果，才能访问这个返回值列表。

可以在控制台输出验证。所有计划好的欢迎信息都是一次性打印出来的，但是需要至少等待`3000`毫秒。

现在，让我们看看使用更大的线程池会出现什么情况。

##### Snippet-02：使用更大的线程池完成Callable任务列表

```java
public class MultipleCallableRunner {
  public static void main(String[] args) throws InterruptedException, ExecutionException {
    ExecutorService executorService = Executors.newFixedThreadPool(3);
    List<CallableTask> tasks = List.of(new CallableTask("in28Minutes"),
                      new CallableTask("Ranga"),
                      new CallableTask("Adam"));
    List<Future<String>> welcomeAll = executorService.invokeAll(tasks);
    for(Future<String> welcomeFuture : welcomeAll) {
      System.out.println(welcomeFuture.get());
    }
    executorService.shutdown();
  }
}
```

***控制台输出***

*Hello in28Minutes*

*Hello Ranga*

*Hello Adam*

##### Snippet-02 说明

所有的欢迎信息再次批量打印，但是等待它们的时间缩短了。这是由于：

- 线程池的大小现在是`3`，而不是之前的`2`（译者注：之前是`1`）。这意味着三个任务可以同时处于**RUNABLE**状态。
- 然后，它们也几乎同时处于**BLOCKED**状态，这意味着等待它们的时间远小于`3000`毫秒。这是更大的线程池的其中一个优点。

#### 总结

在这一节中，我们：

- 学习了可以一次性收集`Callable`线程池的返回值。
- 这是使用`invokeAll()`方法来完成的，并指定一个`Future`对象列表来保存这些结果。
- 更改这种情况的线程池大小会极大地改变响应时间

### 13：Executor - 只等待最快的任务

让我们看看如何等待这三个任务中的任何一个完成。

##### Snippet-01：只等待最快的任务

```java
public class MultipleAnyCallableRunner {
  public static void main(String[] args) throws InterruptedException, ExecutionException {
    ExecutorService executorService = Executors.newFixedThreadPool(3);
    List<CallableTask> tasks = List.of(new CallableTask("in28Minutes"),
                      new CallableTask("Ranga"),
                      new CallableTask("Adam"));
    String welcomeMessage = executorService.invokeAny(tasks);
    System.out.println(welcomeMessage);
    executorService.shutdown();
  }
}
```

（译者注：多次运行，结果不同）

***控制台输出***

*Hello Ranga*

***控制台输出***

*Hello in28Minutes*

***控制台输出***

*Hello Ranga*

***控制台输出***

*Hello Adam*

##### Snippet-01 说明

`invokeAny()`方法在第一个子任务完成后就返回。此外，返回的值不再是`Future`对象，而是`call()`方法的返回值。

我们可以看到，在不同的执行过程中，控制台输出的顺序发生了变化。这是由于：

- 三个任务都是在一个大小为`3`的线程池中一起创建的
- 所以，这些都是独立的线程，几乎同时进入**RUNABLE**状态。

#### 总结

在这一节中，我们：

- 了解到`ExecutorService`有一种方法可以从**RUNABLE**线程的轮询中返回第一个结果