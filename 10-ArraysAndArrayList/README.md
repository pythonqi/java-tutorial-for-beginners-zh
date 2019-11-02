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

```shell
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

```shell
jshell> int[] marks = {75, 60, 56};
marks ==> int[3]{ 75,60,56 }
```

在上面的示例代码中

- `marks`是一个数组
- `marks`存了多个`int`类型的值
- `marks`数组长度为3

在数组中，下标从0到数组长度-1.在上面的示例代码中，下标范围是0到2。

你可以用下标找到数组中的指定元素。用下标操作符（`[]`）完成。表达式`marks[0]`表示数组`marks`的第一个元素，它的下标为`0`。

```shell
jshell> marks[0]
$20 ==> 75

jshell> marks[1]
$21 ==> 60

jshell> marks[2]
$22 ==> 56
```

如果要求`marks`数组所有元素值的和，该怎么写代码？

```shell
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



