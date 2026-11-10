# 1 快速入门

## 1.1 java项目基础

### 1.1.1 项目结构

项目是最大的一层结构，接下来是模块，再接下来是包，再接下来是一类，类是写代码的地方

![image.png](images/image.png)

此处只是因为学习代码的需要，所以我就没有在模块下面再新建包，直接再模块下的src内进行新建java类

### 1.1.2 第一个java代码

输出hello world

```java
public class HelloWorld {
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

简单剖析一下一个完整的java程序，基本结构是什么

```java
public class Hello {
 public static void main(String[] args) {
 // 向屏幕输出文本:
 System.out.println("Hello, world!");
 /* 多行注释开始
注释内容
注释结束 */
 }
 } // class定义结束
```

java是面向对象的语言，一个程序的基本单位是`class`

，`class` 是关键字，以最上面的输出helloworld为例，这里的类名就是`HelloWorld`

类名要求：

- 类名必须以英文母开头，后接字母，数字和下划线的组合
- 习惯以大写字母开头

public是访问修饰符，表示该class是公开的

不写`public`，也能正常编译，但是这个类将无法从命令行执行

在`class`内部，可以定义若干方法

```java
public class Hello {
 public static void main(String[] args) { // 方法名是main
 // 方法代码...
 } // 方法定义结束
}
```

方法定义了一组执行语句，方法内部的代码将会被依次顺序执行

此处方法名是`main`，返回值为`void`

<aside>
💡

注意到
`void` ，表示没有任何返回值。
`public` 除了可以修饰
`class` 外，也可以修饰方法。而关键字
`static` 是另一个修饰
符，它表示静态方法，后面我们会讲解方法的类型，目前，我们只需要知道，Java入口程序规定的
方法必须是静态方法，方法名必须为
`main` ，括号内的参数必须是String数组

</aside>

在方法内部，语句才是真正的执行代码。Java的每一行语句，必须以分号结束

### 1.1.3 变量和数据类型

**基本类型的变量**

```java
public class A {
    public static void main(String[] args){
        int a=100;
        int b=6000;
        int c=a+b;
        System.out.println("Sum of a and b is:"+c);
    }
}

"D:\SYshiyu-EF6\network security\java environment\bin\java.exe" "-javaagent:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\lib\idea_rt.jar=58048:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath D:\MINE\projects\java_projects\study\out\production\code_1 A
Sum of a and b is:6100

进程已结束，退出代码为 0

```

```java
public class A {
    public static void main(String[] args){
        int a=100;
        int b=6000;
        int c;
        c=a;
        a=b;
        b=c;
        System.out.println(a);
        System.out.println(b);

    }
}

"D:\SYshiyu-EF6\network security\java environment\bin\java.exe" "-javaagent:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\lib\idea_rt.jar=59048:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath D:\MINE\projects\java_projects\study\out\production\code_1 A
6000
100

进程已结束，退出代码为 0
```

基本数据类型是CPU可以直接进行运算的类型。Java定义了以下几种基本数据类型：

**整数类型**：byte，short，int，long
**浮点数类型**：float，double
**字符类型**：char
**布尔类型**：boolean

![image.png](images/image%201.png)

**整形**

```java
public class B {
    public static void main(String[] args){
        int i=2147483647;
        int i2=-214783647;
        int i3=2_000_000_000;//加下划线更容易识别
        int i4=0xff0000;//十六进制
        int i5=0b1000000000;//二进制
        
        long n1=9000000000000000000L;//long型的结尾需要加L
        long n2=900;//没有加L,此处900为int，但int类型可以赋值给long
        int i6=900L;//错误，不能把long型赋值给int类型
    }

}

```

特别注意：同一个数的不同进制的表示是完全相同的

**浮点型**

就是小数，因为小数用科学计数法表示的时候，小数点是可以浮动的

![image.png](images/image%202.png)

```java
float f1 = 3.14f;
 float f2 = 3.14e38f; // 科学计数法表示的3.14x10^38
 float f3 = 1.0; // 错误：不带f结尾的是double类型，不能赋值给float
 double d = 1.79e308;
 double d2 = -1.79e308;
 double d3 = 4.9e-324; // 科学计数法表示的4.9x10^-324
```

**布尔型**

`boolean`只有`true`和`false`两个值，布尔类型总是关系运算的计算结果

```java
boolean b1 = true;
 boolean b2 = false;
 boolean isGreater = 5 > 3; // 计算结果为true
 int age = 12;
 boolean isAdult = age >= 18; // 计算结果为false
```

**字符类型**

```java
public class Main {
 public static void main(String[] args) {
 char a = 'A';
 char zh = '中';
 System.out.println(a);
 System.out.println(zh);
 }
 }
```

`char` 类型使用单引号`'`，且仅有一个字符，要和双引号`"`的字符串类型区分开。

---

剩下的都是引用类型

引用类型的变量类似于C语言的指针，她的内部存储一个“地址”，指向某个对象在内存的位置

---

### 1.1.4 运算

**整数运算**

遵循四则运算规则

这里不需要多说了

整数由于存在范围限制，如果计算结果超出了范围，就会产生溢出，而溢出不会出错，却会得到一个奇怪的结果

<aside>
💡

整数运算的结果永远是精确的；运算结果会自动提升；可以强制转型，但超出范围的强制转型会得到错误的结果；应该选择合适范围的int或long

</aside>

**浮点数运算**

浮点数是会出现运算误差的，所以比较两个浮点数是否相等，正确的比较方法是判断连个浮点数之差的绝对值是否小于一个很小的数

```java
 double r = Math.abs(x - y);
 // 再判断绝对值是否足够小:
 if (r < 0.00001) {
 // 可以认为相等
} else {
 // 不相等
}
```

溢出，整数运算在除数为0的时候会报错，但浮点数运算在除数为0时，不会报错，但会返回几个特殊值

`NaN` 表示`Not a Number`
`Infinity` 表示无穷大

`-Infinity` 表示负无穷

**布尔运算**

示例

```java
boolean isGreater = 5 > 3; // true
 int age = 12;
 boolean isZero = age == 0; // false
 boolean isNonZero = !isZero; // true
 boolean isAdult = age >= 18; // false
 boolean isTeenager = age >6 && age <18; // true
```

布尔运算其实就是一个对后面表达式的真假值判断

**三元运算**

`b ? x : y`  

和C语言一样

```java
public class B {
    public static void main(String[] args){
        int n = -100;
        int x = n >=0?n:-n;
        System.out.println(x);
    }

}
"D:\SYshiyu-EF6\network security\java environment\bin\java.exe" "-javaagent:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\lib\idea_rt.jar=59550:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath D:\MINE\projects\java_projects\study\out\production\code_1 B
100

进程已结束，退出代码为 0
```

### 1.1.5 字符和字符串

字符就不写了

---

字符串

```java
public class C {
    public static void main(String[] args){
        String s1="hello";
        String s2="wolrd";
        String s=s1+" "+s2+"!";
        System.out.println(s);
    }
}
"D:\SYshiyu-EF6\network security\java environment\bin\java.exe" "-javaagent:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\lib\idea_rt.jar=63813:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath D:\MINE\projects\java_projects\study\out\production\code_1 C
hello wolrd!

进程已结束，退出代码为 0

```

```java
public class C {
    public static void main(String[] args){
        int age = 25;
        String s = "age is " + age;
        System.out.println(s);
    }
}
"D:\SYshiyu-EF6\network security\java environment\bin\java.exe" "-javaagent:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\lib\idea_rt.jar=63839:D:\SYshiyu-EF6\IDEA\IntelliJ IDEA Community Edition 2024.2.3\bin" -Dfile.encoding=UTF-8 -Dsun.stdout.encoding=UTF-8 -Dsun.stderr.encoding=UTF-8 -classpath D:\MINE\projects\java_projects\study\out\production\code_1 C
age is 25

```

多行字符串

```java
public class Main {
 public static void main(String[] args) {
 String s = """
 SELECT * FROM
 users
 WHERE id > 100
 ORDER BY name DESC
 """;
 System.out.println(s);
 }
 }
```

![image.png](images/image%203.png)

**字符串的不可变性**

Java的字符串除了是一个引用变量外，字符串不可变

```java
public class Main {
 public static void main(String[] args) {
 String s = "hello";
 System.out.println(s); // 显示 hello
 s = "world";
 System.out.println(s); // 显示 world
 }
 }
```

变的不是字符串，而是变量s的指向，这里提到了指向，和C语言里面的指针很像

再举一个例子

```java
public class C {
    public static void main(String[] args) {
        String s = "hello";
        String t = s;
        s = "world";
        System.out.println(t); 
    }
}
```

![image.png](images/image%204.png)

**空值null**

```java
String s1 = null; // s1是null
 String s2 = s1; // s2也是null
 String s3 = ""; // s3指向空字符串，不是null
```

<aside>
💡

基本类型的变量是“持有”某个数值，引用类型的变量是“指向”某个对象

</aside>

### 1.1.5 数组类型

// 数组默认初始化值的规律
// 整数类型，默认初始化值为0
// 小数类型，默认初始化值为0.0
// 字符类型默认初始化值为，‘/u0000’ 空格
// 布尔类型，默认初始化值 false
// 引用数据类型：默认初始化值 null

![image.png](images/image%205.png)

![image.png](images/image%206.png)

也可以直接再定义数组时指定初始化元素

编译器会自动推算数组大小

```java
// 数组
public class Main {
    public static void main(String[] args) {
        // 5位同学的成绩:
        int[] ns;
        ns = new int[] { 68, 79, 91, 85, 62 };
        System.out.println(ns.length); // 5
        ns = new int[] { 1, 2, 3 };
        System.out.println(ns.length); // 3
    }
 }
```

既然数组也是引用类型，那么我们看上面这段代码，对于ns来说，执行上面那条语句时，ns指向的是一个5个元素的数组

执行下面的时候，ns指向的是一个新的3个元素的数组

**字符串数组**

```java
String[] names={
"abs","xys","zoo"};
```

数组变量names包含三个元素，每个元素都指向某个字符串对象

```java
public class Main {
    public static void main(String[] args) {
        String[] names = {"ABC", "XYZ", "zoo"};
        String s = names[1];
        names[1] = "cat";
        System.out.println(s); // s是"XYZ"还是"cat"?
    }
    最后s时cat
```

<aside>
💡

数组是统一数据类型的集合，数组一旦创建后，大小就不可变；

可以通过索引访问数组元素，但索引超出范围将报错；

数组元素可以是值类型或者引用类型，但数组本身是引用类型

</aside>

**数组动态初始化和静态初始化的区别**
- 动态初始化：手动指定数组长度，由系统给出默认初始化值
     只明确元素个数，不明确具体数值，推荐使用动态初始化
- 动态初始化：手动指定数组元素，系统会根据元素个数，计算出数组的长度
      明确了要操作的具体数据 ，直接静态初始化即可
### 1.1.6 流程控制

**输出**

`System.out.println()` 是输出并换行

如果不想换行可以用`System.out.print()`

**格式化输出**

```java
// 格式化输出
public class Main {
 public static void main(String[] args) {
 double d = 3.1415926;
 System.out.printf("%.2f\n", d); // 显示两位小数3.14
 System.out.printf("%.4f\n", d); // 显示4位小数3.1416
 }
 }
```

这里就和C语言中的很像了，就不多写了

由于%表示占位符，因此表示%本身

**输入**

```java
import java.util.Scanner;
 public class Main {
 public static void main(String[] args) {
 Scanner scanner = new Scanner(System.in); // 创建Scanner对象
System.out.print("Input your name: "); // 打印提示
String name = scanner.nextLine(); // 读取一行输入并获取字符串
System.out.print("Input your age: "); // 打印提示
int age = scanner.nextInt(); // 读取一行输入并获取整数
System.out.printf("Hi, %s, you are %d\n", name, age); // 格式化输出
}
 }
```

首先，通过import导入java.util.Scanner

import是导入某个类的语句，必须放到java源代码的开头

创建Scanner对象并传入System.in,System.out代表标准输出流，而System.in代表标准输入流，直接使用
System.in读取用户输入虽然是可以的，但需要更复杂的代码，而通过Scanner就可以简化后续的代码。

Scanner 会自动转换数据类型，所以不用手动转化

![image.png](images/image%207.png)

![image.png](images/image%208.png)

<aside>
💡

Java提供的输出包括：
格式化输出；
System.out.println() /
print() /
printf() ，其中
printf() 可以
Java提供Scanner对象来方便输入，读取对应的类型可以使用：
scanner.nextLine() /
nextInt() /
nextDouble() / ..

</aside>

接下来的if 循环等都类比C语言

**if选择**

```java
public class Main {
 public static void main(String[] args) {
 int n = 70;
 if (n >= 90) {
 System.out.println("优秀");
 } else if (n >= 60) {
 System.out.println("及格了");
 } else {
 System.out.println("挂科了");
 }
 System.out.println("END");
 }
 }
```

值类型是否相等和C语言一样，但是引用类型，虽然也是使用==，但是它判断的是是否指向同一个对象

例如

```java
public class Main {
 public static void main(String[] args) {
 String s1 = "hello";
 String s2 = "HELLO".toLowerCase();
 System.out.println(s1);
 System.out.println(s2);
 if (s1 == s2) {
 System.out.println("s1 == s2");
 } else {
 System.out.println("s1 != s2");
 }
 }
 }
```

虽然两个string类型的内容相等，但是指向的是不同的对象，结果为false

想要判断引用类型的变量内容是否相等，必须使用`equals()`

```java
public class Main {
 public static void main(String[] args) {
 String s1 = "hello";
 String s2 = "HELLO".toLowerCase();
System.out.println(s1);
 System.out.println(s2);
 if (s1.equals(s2)) {
 System.out.println("s1 equals s2");
 } else {
 System.out.println("s1 not equals s2");
 }
 }
 }
```

如果s1为null，会报错`NullPointerException` 

为了避免报错，可以利用短路机制

 `if (s1 != null && s1.equals("hello"))` 

也可以把不是null的对象放在前面

**switch选择**

传统的就和C语言一样，但是会有如果不屑break出现滑落的情况

而从java12以后，有了新的语法，不会出现滑落，且不需要break语句

```java
 public class Main {
 public static void main(String[] args) {
 String fruit = "apple";
 switch (fruit) {
 case "apple" -> System.out.println("Selected apple");
 case "pear" -> System.out.println("Selected pear");
 case "mango" -> {
 System.out.println("Selected mango");
 System.out.println("Good choice!");
 }
 default -> System.out.println("No fruit selected");
 }
 }
 }
```

而且新的switch还可以直接返回值

例如

```java
public class Main {
public static void main(String[] args) {
 String fruit = "apple";
 int opt = switch (fruit) {
 case "apple" -> 1;
 case "pear", "mango" -> 2;
 default -> 0;
 }; // 注意赋值语句要以;结束
System.out.println("opt = " + opt);
 }
 }
```

**yield**

在大多数情况下，在switch内部会返回简单的值，但如果需要复杂的语句，最后可以用yield返回一个值作为switch语句的返回值

```java
 public class Main {
 public static void main(String[] args) {
 String fruit = "orange";
 int opt = switch (fruit) {
 case "apple" -> 1;
 case "pear", "mango" -> 2;
 default -> {
 int code = fruit.hashCode();
 yield code; // switch语句返回值
}
 };
 System.out.println("opt = " + opt);
 }
 }
```

**while循环**

**do while**

省略不写

**for** 

for each循环

写法是这样的

```java
public class Main {
 public static void main(String[] args) {
 int[] ns = { 1, 4, 9, 16, 25 };
 for (int n : ns) {
 System.out.println(n);
 }
 }
 }
```

在此处，不需要用到计数器，即可遍历数组，此处n直接对应到数组的每个元素

**break 和 continue**

### 1.1.7 数组操作

**遍历**

特殊一点的就是上面提到过的for each

其他的没什么特殊的

**排序**

拿冒泡排序举个例

```java
import java.util.Arrays;
 public class Main {
 public static void main(String[] args) {
 int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
 // 排序前:
 System.out.println(Arrays.toString(ns));
 for (int i = 0; i < ns.length - 1; i++) {
 for (int j = 0; j < ns.length - i - 1; j++) {
 if (ns[j] > ns[j+1]) {
 // 交换ns[j]和ns[j+1]:
 int tmp = ns[j];
 ns[j] = ns[j+1];
 ns[j+1] = tmp;
 }
 }
 }
 // 排序后:
 System.out.println(Arrays.toString(ns));
 }
 }
```

实际上，java已经内置排序功能，只需要调用

```java
import java.util.Arrays;
 Arrays.sort() 就可以排
public class Main {
 public static void main(String[] args) {
 int[] ns = { 28, 12, 89, 73, 65, 18, 96, 50, 8, 36 };
 Arrays.sort(ns);
 System.out.println(Arrays.toString(ns));
 }
 }
```

28 12 等这些没有变，只是，ns[0]、ns[1]…..这些的指向变了

**多维数组**

数组的数组

这里和C语言在写的时候不太一样

```java
public class Main {
    public static void main(String[] args) {
        int[][] ns = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        System.out.println(ns.length); // 3
    }
 }
```

这儿的ns.length为3

![image.png](images/image%209.png)

如果重新定义一个普通数组arr0,并把ns[0]赋值给它，其实是把第一组的第0个元素给了它，并且arr0可以获取到这一组元素

访问的话ns[0][0]，就是1，这和C一样

**三维数组**

二维数组的数组

```java
int[][][] ns = {
 {
 {1, 2, 3},
 {4, 5, 6},
 {7, 8, 9}
 },
 {
 },
 {
 {10, 11},
 {12, 13}
 {14, 15, 16},
  {17, 18}
    }
 };
```

ns[0][0][0]就是1，很好理解

## 1.2 面向对象编程

面向对象编程，是一种通过对象的方式，把现实世界映射到计算机模型的一中编程方法。

现实世界中，我们定义了“人”这种抽象概念，而具体的人则是

**程序开发：面向过程VS面向对象**

形象点举个例子：

【在家我要吃西红柿炒鸡蛋，我要想好先做什么，再做什么。我要解决的问题是我要吃西红柿炒鸡蛋，我把它按步骤分开来解决。】这是**面向过程**

【我去餐馆点西红柿炒鸡蛋，和上面同样的问题，但此时我考虑的就不是怎么做，按什么步骤做，我此时要考虑的是西红柿炒鸡蛋这个整体，对象是一个提前就封装好的东西。】这是**面向对象**

- 面向过程：面向过程是一种以“整体事件”为中心的编程思想，编程的时候把 解决问题的步骤分析出来，然后用过函数把这些步骤实现，再一步步的具体步骤中再按顺序调用函数

**面型对象**：面向对象是一种以“对象”为中心的编程思想，把要解决的问题分解成各个对象

对象是一个信息及对信息进行处理的描述所组成的整体，是对现实世界的抽象

对象的三个 特征：对象的行为，对象的形态，对象的表示

### 1.1.1 类的定义

**类**是定义了一件事物的抽象特点，它将数据的形式以及这些数据上的操作封装在一起。

对象是具有类类型的变量，是对类的实例

例如：我要买水果，我就和老板讲，“老板，我要点水果”，老板问，”什么水果”，我说，“我就要水果”。

另一个人进来了，“老板，来点苹果”，老板说，“好嘞”。

**水果是“类”，而苹果是“对象”**。苹果是具有水果这个类类型的变量，是水果这个类的实例

### 1.1.2 类的构成

**成员变量（属性）+成员函数（方法）**

- 成员变量（属性）：定义在类内部的变量

该变量的值对外是不可见的，

但是可以通过成员函数访问，

在类被实例化为对象后，

该变量即可成为对象的属性

- 成员函数（方法）：定义在类的内部，可用于访问对象的数据

### 1.1.3 继承

继承性是子类自动共享父类数据结构和方法的机制，是类之间的一种关系

在定义和实现一个累的时候，可以在一个已经存在的类的基础之上来进行,把一个已经存在的类所定义的内容作为自己的内容，并加入若干新的内容

- 父类：一个类被其它类继承，可将该类成为父类，或基类，超类
- 子类：一个类看i成其他类称为子类，也可称为派生类

---

由于寒假在学习php反序列化时已经学习过相关方面的知识，这里就直接用实例来带过

```java
class Person {
 public String name;
 public int age;
 }
 Person ming = new Person();
 
ming.name = "Xiao Ming"; // 对字段name赋值
ming.age = 12; // 对字段age赋值
System.out.println(ming.name); // 访问字段name
```

<aside>
💡

`class`和`instance`时模板和实例的关系

指向`instance`的变量都是引用变量

访问实例字段的方法是`变量名.字段名`

</aside>

### 1.1.4 方法

我们可以看到之前的变量修饰符都是public，外部是可以访问的，但是有时候可能会与外部的变量出现混乱，那么就可以用private来修饰，但是，外部就无法访问对其进行赋值，这时我们就需要方法来让外部代码可以间接修改这些

```java
 public class Main {
 public static void main(String[] args) {
 Person ming = new Person();
 ming.setName("Xiao Ming"); // 设置name
 ming.setAge(12); // 设置age
 System.out.println(ming.getName() + ", " + ming.getAge());
 }
 }
 class Person {
 private String name;
 private int age;
 public String getName() {
 return this.name;
 }
 public void setName(String name) {
 this.name = name;
 }
 public int getAge() {
 return this.age;
 }
 public void setAge(int age) {
 if (age < 0 || age > 100) {
 throw new IllegalArgumentException("invalid age value");
 }
 this.age = age;
 }
 }
```

这里是public方法，那么就有private方法，private方法是只有内部方法可以调用private方法

```java
// private method
 public class Main {
 public static void main(String[] args) {
 Person ming = new Person();
 ming.setBirth(2008);
 System.out.println(ming.getAge());
 }
 }
 class Person {
 private String name;
 private int birth;
 public void setBirth(int birth) {
 this.birth = birth;
 }
 public int getAge() {
 return calcAge(2019); // 调用private方法
}
 // private方法:
 private int calcAge(int currentYear) {
 return currentYear - this.birth;
 }
 }
```

**this变量**

在方法内部，可以使用一个隐含的变量`this`，它始终指向当前实例。

如果没有命名冲突，可以省略`this`

```java
class Person {
 private String name;
 public String getName() {
 return name; // 相当于this.name
 }
 }
```

但，如果有局部变量和字段重名，那么局部变量优先级更高，必须上`this`

```java
class Person {
 private String name;
this ：
public void setName(String name) {
 this.name = name; // 前面的this不可少，少了就变成局部变量name了
}
 }
```

**参数**

一般的参数就不说了

**可变参数**

可变参数其实就是数组

用`类型… 参数名`   来定义

也可以写成`类型[] 参数名` 

但是，调用方需要自己先构造String[] ，比较麻烦。例如

```java
Group g = new Group();
 g.setNames(new String[] {"Xiao Ming", "Xiao Hong", "Xiao Jun"}); // 传入1个
String[]
```

可变参数可以保证，无法传入`null`，因为传入0个参数时，接收到的实际值是一个空数组，而不是`null`

**参数绑定**

基本类型参数的传递时调用方值得复制，双方各自的后续修改，互不影响

引用类型参数的传递，调用方的变量和接收方的参数变量，指向的是同一个对象，双方任意一方对这个对象的修改，都会影响对方，因为指向同一个对象

### 1.1.5 构造方法

构造方法是用来在创建对象实例时将内部字段全部初始化为合适的值

```java
public class Main {
 public static void main(String[] args) {
 Person p = new Person("Xiao Ming", 15);
 System.out.println(p.getName());
 System.out.println(p.getAge());
 }
 }
 class Person {
 private String name;
 private int age;
 public Person(String name, int age) {
 this.name = name;
 this.age = age;
 }
 public String getName() {
 return this.name;
 }
 public int getAge() {
 return this.age;
 }
 }
```

构造方法是特殊的一种方法，构造放法的名称就是类名，构造方法的参数没有限制，在方法内部可以编写任意语句，但是和普通方法相比，构造方法没有返回值，调用构造方法，必须用`new`

<aside>
💡

如果一个类没有定义构造方法，编译器会自动为我们生成一个默认的构造方法，他没有参数，也没有执行语句

但是，如果我们自定义了一个构造放啊，那么编译器就不再自动创建默认的构造方法了

也就是说你自定义构造方法后，就必须按照新定义的构造方法来`new`

如果既要能使用带参数的构造方法，又想要保留不带参数的构造方法，那么只能把两个构造方法都定义出来

</aside>

```java
 class Person {
 private String name;
 private int age;
 public Person() {
 }
 public Person(String name, int age) {
 this.name = name;
 this.age = age;
 }
 public String getName() {
 return this.name;
 }
 public int getAge() {
 return this.age;
 }
 }
```

没有在构造方法中初始化字段时，引用类型的字段默认是`null`，数值类型的字段用默认值`int`为`0`，布尔为`false`

<aside>
💡

构造方法可以定义多个，在new的时候，编译器会根据构造方法的参数数量、位置和类型自动区分

</aside>

### 1.1.6 方法重载

方法名相同，但各自的参数不同，称为方法重载

方法重载的返回值类型通常是相同的

方法重载的目的是，功能类似的方法使用同一的名字，更容易记住，因此调用起来更简单

### 1.1.7 继承

例如以下代码

```java
class Person {
 private String name;
 private int age;
 public String getName() {...}
 public void setName(String name) {...}
 public int getAge() {...}
 public void setAge(int age) {...}
 }
 class Student extends Person {
 // 不要重复name和age字段/方法,
 // 只需要定义新增score字段/方法:
 private int score;
 public int getScore() { … }
 public void setScore(int score) { … }
 }
```

它提高了代码的复用性

Java用`extends`关键字来实现继承

<aside>
💡

Java只允许一个class继承自一个类，一个类有且仅有一个父类

</aside>

**常用访问权限修饰符：**

**public**：公共的，在类的内部，子类中 或者类的外部都可以使用，不受限制；

**projected**：受保护的，在类的内部、子类中可以使用，但不能在类的外部使用；

**private**：私有的，只能在类的内部使用，在类的外部或者子类中都无法使用；

**Super**

`super` 关键字表示父类（超类）。子类引用父类的字段时，可以使用`super.filedName`

这个不是必须的，有时候不用`super`编译器会自动定位到父类`name`字段

但是在有些时候必须用super

在Java中，任何`class`的构造方法，第一句必须是调用父类的构造方法，如果没有明确地调用父类的构造方法，编译器会帮我们自动加一句`super（）` ，有无参数看情况

```java
class Student extends Person {
 protected int score;
 public Student(String name, int age, int score) {
 super(name, age); // 调用父类的构造方法Person(String, int)
 this.score = score;
 }
 }
```

**阻止继承**

正常情况下，只要某个class没有final修饰符，那么任何类都可以从该class继承

我在练习的时候写了这样一段代码

```java
sealed class Person permits Student{
    protected String name;
    protected int age;

    public Person(String name,int age) {
        this.name = name;
        this.age = age;
    }
    public String getName(){
        return this.name;
    }
    public int getAge(){
        return this.age;
    }

}

final class Student extends Person{
    private int score;

    public Student(String name,int age,int score){
        super(name,age);
        this.score = score;
    }
    public int getScore(){
        return this.score;
    }
}
```

<aside>
💡

在过程中我有一个疑问就是，为什么我在用sealed修饰Person类且限制其只能被一个Student继承后，在Student前不屑final就会报错

得到的答案是

Java 规定：**所有被列在 `permits` 里的子类都必须同时用以下三种修饰符之一来“收尾”**，否则编译错误：

- `final`（不能再被继承），
- `sealed`（再指定下一级子类），
- `non-sealed`（重新开放继承）。
</aside>

**向上转型**

如果一个引用变量的类型是Student，那么它可以指向一个Student类型的实例，如果一个引用类型的变量事Person，那么它可以指向一个Person类型的实例。

如果Student是从Person继承下来，那么一个引用类型为Person的变量，是能指向Student，但是反过来就可能会失败

这个可以怎么理解呢，就像是，学生可以被指认成人，但人不一定能被指认成学生

```java
Person p = new Student();
//这样是可以的
```

但是

**向下转型**

```java
Person p1 = new Student(); // upcasting, ok
Person p2 = new Person();
Student s1 = (Student) p1; // ok
Student s2 = (Student) p2; // runtime error! ClassCastException!

```

person类型p1实际指向Student实例，Person类型p2实际指向Person，在向下转型时候，p1转型成Student会成功

，但p2会失败，子类功能比父类多，多的功能无法凭空变出。

所以说为了避免向下转型失败，java提供了instanceof，可以判断某一个实例究竟是不是某种类型或者这个类型的子类

```java
Person p = new Person();
System.out.println(p instanceof Person); // true
System.out.println(p instanceof Student); // false

Student s = new Student();
System.out.println(s instanceof Person); // true
System.out.println(s instanceof Student); // true

Student n = null;
System.out.println(n instanceof Student); // false

```

实际运用会像这样

```java
Person p = new Student();
if (p instanceof Student) {
    // 只有判断成功才会向下转型:
    Student s = (Student) p; // 一定会成功
}

```

### 1.1.8 多态

多态是再 继承/实现 情况下的一中现象，表现为：对象多态、行为多态

多态的前提

- 有 继承/实现 关系；存在父类引用子类对象；存在方法重写

多态的注意事项

- 多态是对象、行为的多态，java中的属性不谈多态

这里我写了一段代码，大概是这么个意思

```java
public class F {
    public static void main(String[] args){
        Animal a = new Dog();
        a.run();
        Animal b = new Cat();
        b.run();
        
    }
}

class Animal{
    public void run(){
        System.out.println("动物在跑");
    }

}

class Dog extends Animal{
    @Override
    public void run(){
        System.out.println("狗在跑");
    }
}

class Cat extends Animal {
    @Override
    public void run() {
        System.out.println("猫在跑");
    }
}

```

这里涉及到一个子类覆写父类方法的知识点

**覆写：**在继承关系中，子类如果定义了一个与父类方法名称完全相同的方法，被称为覆写@Override。

<aside>
💡

方法名相同，方法参数相同，但方法返回值不同，也是不同的方法，在java程序中，出现这种情况，编译器会报错。

加上@Override可以让编译器帮助检查是否进行了正确的覆写；当你希望进行覆写，但是不小心写错了方法签名，编译器会报错。

</aside>

多态有一个特性是，运行的时候，才能动态决定调用的子类方法，在上述代码中，animal类型的a指向了dog类的实例，b指向了cat类，都有run的方法，但在实际运行时会自动调用对应的方法

**调用super**

在子类的覆写方法中，如果要用父类的被覆写的方法，可以通过super来调用

```java
class Person{
    protected String name;
    public String hello(){
        return "Hello,"+name;
    }
}

class Student extends Person{
    @Override
    public String hello(){
        return super.hello()+"!";
    }
}
```

继承可以允许子类覆写父类的方法，如果一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为final，用final修饰的方法不能被Override。

并且被final修饰的类不能被继承，被final修饰的属性不可被重新赋值，可以在构造方法中初始化final字段。这样可以保证一个字段在初始化后不能被修改。

### 1.1.9 抽象类

由于多态的存在，每个子类都可以覆写父类的方法。然后呢，在上面的多态示例代码中可以看到它会自动调用正确的方法

如果说父类中的方法没有实际意义，那么能否去掉方法的执行语句，只声明。

```java
class Person{
    public void run();
}
```

这样是不可以的，因为定义方法的时候，必须实现方法的语句。当然，更不可以去掉父类中的方法。

如果说父类的方法不需要实现任何功能，仅仅是为了定义方法签名，不敌是让子类去覆写它，那么，可以把父类的方法声明为抽象方法

```java
abstract class Person{
    public abstract void run();
}
```

这里因为这个抽象方法本是无法执行，所以，Person类也无法被实例化，必须把Person类本身也声明为abstract才能正确编译它

**抽象类**

如果一个class定义了方法，但没有具体执行代码，这个方法就是抽象方法，抽象方法用abstract修饰，因为无法执行抽象方法，因此这个类也必须声明为抽象类。

抽象类无法实例化，但是它可以强迫子类实现其定义的抽象方法，否则编译会报错。因此，抽象方法实际上相当于定义了“规范”。

这里由此引出了**面向抽象编程**

当定义了抽象类Person，以及具体的Student、Teacher子类的时候，我们可以通过抽象类Person类型与引用具体的子类

```java
Person s = new Student();
Person t = new Teacher();
```

这样的话，我们对其进行方法调用时，不需要关心Person类型变量的具体子类型

```java
// 不关心Person变量的具体子类型:
s.run();
t.run();
```

这种尽量引用高层类型，避免引用实际子类型的方式，称为面向抽象编程

**面向抽象编程的本质就是:**

- 上层代码只是定义规范
- 具体的业务逻辑有不同的子类实现，调用者并不关心

### 1.1.10 接口

在抽象类中，抽象方法本质上时定义接口规范：即规定高层类的接口，从而保证所有子类都有相同的接口实现，这样多态就体现的更加淋漓尽致

如果一个抽象类没有字段，所有方法全部都是抽象方法
``` java
abstract class Person {
    public abstract void run();
    public abstruct String getName();
}
```

就可以把改抽象类改写成接口 `interface`
``` java
interface Person {
    void run();
    String getName();
}
```

接口就是比抽象类还要抽象的的纯抽象接口，因为它链字段都不能又。因为接口定义的所有方法默认都是`public abstract` 
当一个具体的`class` 去实现一个`interface` 时，需要使用`implements` 
```java
class Student implements Person {
    private String name;
    
   
    public Student(Stirng name){
        this.name = name;
    }
    
    @Override
    public void run() {
        System.out.println(name + "跑");
    }
    @Override
    public String getName(){
        return name;
    }
    
}

```
Java中一个类只能继承自另一个类，不能从多个类继承。但是，一个类可以实现多个`interface`
```java
class Student implements Person, Hello { // 实现了两个interface
    ...
}

```

接口可以继承，使用`extends` ,这个相当于在扩展接口
```java
interface Hello {
    void hello();
}

interface Person extends Hello {
    void run();
    String getName();
}

```

合理设计`interface`和`abstract class`的继承关系，可以充分复用代码。一般来说，公共逻辑适合放在`abstract class`中，具体逻辑放到各个子类，而接口层次代表抽象程度。可以参考Java的集合类定义的一组接口、抽象类以及具体子类的继承关系：
![[Pasted image 20251101213730.png]]
在使用的时候，实例化的对象永远只能是某个具体的子类，但总是通过接口去引用它，因为接口比抽象类更抽象
```java
@练习
package dayOne;  
  
public interface Iterface {  
    double getTax();  
}
package dayOne;  
  
public class Income implements Iterface {  
    protected  double income;  
  
    public Income(double income) {  
        this.income = income;  
    }  
  
    public Income() {}  
  
  
    @Override  
    public double getTax() {  
        return income * 0.1;  
    }  
}

package dayOne;  
  
public class SalaryIncome extends Income {  
  
    public SalaryIncome(double income) {  
        super(income);  
    }  
  
    @Override  
    public double getTax() {  
        if(income <= 5000) {  
            return 0;  
        }  
        return (income-5000) * 0.2;  
    }  
}


```
## 1.3 Java核心类

### 1.3.1 String类

**String是一个引用类型**
```java
String s1 = "Hello";
//实际上，在String内部是通过一个char[]数组表示的
String s2 = new String(new char[] {'H','e','l','l','o'});
```
java字符串一个重要特点是就是字符串不可变，这种不可变性事通过内部的private final cha[]字段，以及没有任何修改char[]的方法实现的

**字符串比较**
当我们想要比较两个字符串是否相同时，要特别注意，我们实际上是想比较字符串的内容是否相同。必须使用`equals()`方法而不能用`==`。
```java
// String
public class Main {
    public static void main(String[] args) {
        String s1 = "hello";
        String s2 = "hello";
        System.out.println(s1 == s2);
        System.out.println(s1.equals(s2));
    }
}


```
要忽略大小写比较，使用`equalsIgnoreCase()`方法。

`String`类还提供了多种方法来搜索子串、提取子串。常用的方法有：

```java
// 是否包含子串:
"Hello".contains("ll"); // true

```

**搜索子串的更多的例子：**

```java
"Hello".indexOf("l"); // 2 从头开始寻找
"Hello".lastIndexOf("l"); // 3 从尾部开始寻找
"Hello".startsWith("He"); // true 
"Hello".endsWith("lo"); // true
```

**提取子串的例子：**

```java
"Hello".substring(2); // "llo" 从索引2到尾
"Hello".substring(2, 4);// "ll"  从索引2，到索引4前一位，（包头不包尾）
```

注意索引号是从`0`开始的。

**去除首尾空白字符**

使用`trim()`方法可以移除字符串首尾空白字符。空白字符包括空格，`\t`，`\r`，`\n`：

```java
"  \tHello\r\n ".trim(); // "Hello"
```

注意：`trim()`并没有改变字符串的内容，而是返回了一个新字符串。

另一个`strip()`方法也可以移除字符串首尾空白字符。它和`trim()`不同的是，类似中文的空格字符`\u3000`也会被移除：

```java
"\u3000Hello\u3000".strip(); // "Hello"
" Hello ".stripLeading(); // "Hello "
" Hello ".stripTrailing(); // " Hello"
```

`String`还提供了`isEmpty()`和`isBlank()`来判断字符串是否为空和空白字符串：

```java
"".isEmpty(); // true，因为字符串长度为0
"  ".isEmpty(); // false，因为字符串长度不为0
"  \n".isBlank(); // true，因为只包含空白字符
" Hello ".isBlank(); // false，因为包含非空白字符
```

**替换子串**

要在字符串中替换子串，有两种方法。一种是根据字符或字符串替换：

```java
String s = "hello";
s.replace('l', 'w'); // "hewwo"，所有字符'l'被替换为'w'
s.replace("ll", "~~"); // "he~~o"，所有子串"ll"被替换为"~~"
```

另一种是通过正则表达式替换：

```java
String s = "A,,B;C ,D";
s.replaceAll("[\\,\\;\\s]+", ","); // "A,B,C,D"
```

上面的代码通过正则表达式，把匹配的子串统一替换为`","`。


**分割字符串**

要分割字符串，使用`split()`方法，并且传入的也是正则表达式：

```java
String s = "A,B,C,D";
String[] ss = s.split("\\,"); // {"A", "B", "C", "D"}
```

**拼接字符串**

拼接字符串使用静态方法`join()`，它用指定的字符串连接字符串数组：

```java
String[] arr = {"A", "B", "C"};
String s = String.join("***", arr); // "A***B***C"
```

**格式化字符串**

字符串提供了`formatted()`方法和`format()`静态方法，可以传入其他参数，替换占位符，然后生成新的字符串：

```java
// String
public class Main {
    public static void main(String[] args) {
        String s = "Hi %s, your score is %d!";
        System.out.println(s.formatted("Alice", 80));
        System.out.println(String.format("Hi %s, your score is %.2f!", "Bob", 59.5));
    }
}
```

有几个占位符，后面就传入几个参数。参数类型要和占位符一致。我们经常用这个方法来格式化信息。常用的占位符有：

- `%s`：显示字符串；
- `%d`：显示整数；
- `%x`：显示十六进制整数；
- `%f`：显示浮点数。


**类型转换**

要把任意基本类型或引用类型转换为字符串，可以使用静态方法`valueOf()`。这是一个重载方法，编译器会根据参数自动选择合适的方法：

```java
String.valueOf(123); // "123"
String.valueOf(45.67); // "45.67"
String.valueOf(true); // "true"
String.valueOf(new Object()); // 类似java.lang.Object@636be97c
```

要把字符串转换为其他类型，就需要根据情况。例如，把字符串转换为`int`类型：

```java
int n1 = Integer.parseInt("123"); // 123
int n2 = Integer.parseInt("ff", 16); // 按十六进制转换，255
```

把字符串转换为`boolean`类型：

```java
boolean b1 = Boolean.parseBoolean("true"); // true
boolean b2 = Boolean.parseBoolean("FALSE"); // false
```

**转换为char[]**

`String`和`char[]`类型可以互相转换，方法是：

```java
char[] cs = "Hello".toCharArray(); // String -> char[]
String s = new String(cs); // char[] -> String
```

如果修改了`char[]`数组，`String`并不会改变：

```java
// String <-> char[]
public class Main {
    public static void main(String[] args) {
        char[] cs = "Hello".toCharArray();
        String s = new String(cs);
        System.out.println(s);
        cs[0] = 'X';
        System.out.println(s);
    }
}
```

这是因为通过`new String(char[])`创建新的`String`实例时，它并不会直接引用传入的`char[]`数组，而是会复制一份，所以，修改外部的`char[]`数组不会影响`String`实例内部的`char[]`数组，因为这是两个不同的数组。

### 1.3.2 StringBuilder

Java编译器对`String`做了特殊处理，可以使用`+`来拼接字符串，但是不够高效，例如在下面这段代码中，每次循环都会u创建新的字符串对象，然后扔掉九的字符串
```java
String s = "";
for (int i = 0; i < 1000; i++) {
    s = s + "," + i;
}
```



















# 2 异常处理
## 2.1 Java的异常
在一些计算机程序运行过程中，总是会出现各种各样的错误
有一些错误使用户造成的，比如，希望用户输入一个int类型的年龄，但是用户的输入是abc
还有一些错误是随机出现，并且永远不可能避免的。比如：

- 网络突然断了，连接不到远程服务器；
- 内存耗尽，程序崩溃了；
- 用户点“打印”，但根本没有打印机；
- ……

所以，一个健壮的程序必须处理各种各样的错误。

所谓错误，就是程序调用某个函数的时候，如果失败了，就表示出错。

调用方如何获知调用失败的信息？
方法一：约定返回错误码。

例如，处理一个文件，如果返回`0`，表示成功，返回其他整数，表示约定的错误码：

```java
int code = processFile("C:\\test.txt");
if (code == 0) {
    // ok:
} else {
    // error:
    switch (code) {
    case 1:
        // file not found:
    case 2:
        // no read permission:
    default:
        // unknown error:
    }
}
```

因为使用`int`类型的错误码，想要处理就非常麻烦。这种方式常见于底层C函数。
方法二：在语言层面上提供一个异常处理机制。

Java内置了一套异常处理机制，总是使用异常来表示错误。

异常是一种`class`，因此它本身带有类型信息。异常可以在任何地方抛出，但只需要在上层捕获，这样就和方法调用分离了：

```java
try {
    String s = processFile(“C:\\test.txt”);
    // ok:
} catch (FileNotFoundException e) {
    // file not found:
} catch (SecurityException e) {
    // no read permission:
} catch (IOException e) {
    // io error:
} catch (Exception e) {
    // other error:
}
```
![[Pasted image 20251102145203.png]]
### 2.1.1 捕获异常

捕获异常使用`try...catch`语句，把可能发生异常的代码放到`try {...}`中，然后使用`catch`捕获对应的`Exception`及其子类：

```java
// try...catch
import java.io.UnsupportedEncodingException;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        byte[] bs = toGBK("中文");
        System.out.println(Arrays.toString(bs));
    }

    static byte[] toGBK(String s) {
        try {
            // 用指定编码转换String为byte[]:
            return s.getBytes("GBK");
        } catch (UnsupportedEncodingException e) {
            // 如果系统不支持GBK编码，会捕获到UnsupportedEncodingException:
            System.out.println(e); // 打印异常信息
            return s.getBytes(); // 尝试使用默认编码
        }
    }
}
```



# 3 反射





# 4 注解




# 5 泛型

## 5.1 什么是泛型
是对类型的一种变量，就拿ArrayList来看
```java
public class ArrayList<T> {
    private T[] array;
    private int size;
    public void add(T e) {...}
    public void remove(int index) {...}
    public T get(int index) {...}
}
```
这里的`T`用来接收传入的类，这样ArrayList就能实现不同类型的ArrayList，注意的一点就是，像基本类型的变量这种，要传入的是他们的包装类

简单来说，泛型就是定义一种模板，实现一次编写，万能匹配

**向上转型**
在Java标准库中的`ArrayList<T>`实现了`List<T>`接口，它可以向上转型为`List<T>`：

```java
public class ArrayList<T> implements List<T> {
    ...
}

List<String> list = new ArrayList<String>();
```

即类型`ArrayList<T>`可以向上转型为`List<T>`。

要_特别注意_：不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`或`List<Number>`。

这是为什么呢？假设`ArrayList<Integer>`可以向上转型为`ArrayList<Number>`，观察一下代码：

```java
// 创建ArrayList<Integer>类型：
ArrayList<Integer> integerList = new ArrayList<Integer>();
// 添加一个Integer：
integerList.add(new Integer(123));
// “向上转型”为ArrayList<Number>：
ArrayList<Number> numberList = integerList;
// 添加一个Float，因为Float也是Number：
numberList.add(new Float(12.34));
// 从ArrayList<Integer>获取索引为1的元素（即添加的Float）：
Integer n = integerList.get(1); // ClassCastException!
```

我们把一个`ArrayList<Integer>`转型为`ArrayList<Number>`类型后，这个`ArrayList<Number>`就可以接受`Float`类型，因为`Float`是`Number`的子类。但是，`ArrayList<Number>`实际上和`ArrayList<Integer>`是同一个对象，也就是`ArrayList<Integer>`类型，它不可能接受`Float`类型， 所以在获取`Integer`的时候将产生`ClassCastException`。

用一个图来表示泛型的继承关系，就是`T`不变时，可以向上转型，`T`本身不能向上转型：
![[Pasted image 20251128111049.png]]

## 5.2 使用泛型
### 5.2.1 泛型接口
例如，`Arrays.sort(Object[])`可以对任意数组进行排序，但待排序的元素必须实现`Comparable<T>`这个泛型接口：

```java
public interface Comparable<T> {
    /**
     * 返回负数: 当前实例比参数o小
     * 返回0: 当前实例与参数o相等
     * 返回正数: 当前实例比参数o大
     */
    int compareTo(T o);
}
```

可以对String数组进行排序，因为String等已经实现了那个接口
但是自己写的必须得让类实现`Comparable<T>`接口
```java
package demo_1128;  
  
import java.util.Arrays;  
  
public class Demo1 {  
    public static void main(String[] args) {  
        Person[] ps  = new Person[] {  
                new Person("Bob",61),  
                new Person("Alice",61),  
                new Person("David",61),  
        };  
        Arrays.sort(ps);  
        System.out.println(Arrays.toString(ps));  
    }  
}  
  
class Person implements Comparable<Person>{  
    String name;  
    int score;  
    public Person(String name, int score) {  
        this.name = name;  
        this.score = score;  
    }  
    @Override  
    public int compareTo(Person o) {  
        return this.name.compareTo(o.name);  
    }  
    @Override  
    public String toString() {  
        return this.name + "," +  this.score;  
    }  
}
```

### 5.2.2 编写泛型类

首先按照某种类型来编写
```java
package demo_1128;  
  
public class Demo2 {  
    private String first;  
    private String last;  
  
    public Demo2(String first, String last) {  
        this.first = first;  
        this.last = last;  
    }  
    public String getFirst() {  
        return first;  
    }  
    public void setFirst(String first) {  
        this.first = first;  
    }  
    public String getLast() {  
        return last;  
    }  
    public void setLast(String last) {  
        this.last = last;  
    }  
    }
```

然后标记所有的特定类型，这里是`String`，把特定类型`String`替换为`T`，并申明`<T>`：
```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}

```

静态方法的泛型编写
```java
package demo_1128;  
  
public class Demo3<T> {  
    private T first;  
    private T second;   
public Demo3(T first, T second) {  
        this.first = first;  
        this.second = second;  
    }  
    public static <K> Demo3<K> create(K first, K second) {  
        return new Demo3<K>(first,second);  
    }  
}
```

### 5.2.3 擦拭法
虚拟机对泛型一无所知，所有的工作都是编译器做的，虚拟机认为泛型都是Object
Java的泛型由编译器在编译实行的，在需要转型的时候，百年一起会根据T的类型自动为我们实行安全的强制转型
**java泛型的局限**
- T不能是基本类型，因为实际类型是Object，Object类型无法持有基本类型
- 无法取得带泛型的class
    因为`T`是`Object`，我们对`Pair<String>`和`Pair<Integer>`类型获取`Class`时，获取到的是同一个`Class`，也就是`Pair`类的`Class`。
    换句话说，所有泛型实例，无论`T`的类型是什么，`getClass()`返回同一个`Class`实例，因为编译后它们全部都是`Pair<Object>`。
- 无法判断带泛型的类型：
    例如，`p instanceof Pari<String>`,并不存在`Pari<String>.class`，只有`Pair.class`

局限四：不能实例化`T`类型：

```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair() {
        // Compile error:
        first = new T();
        last = new T();
    }
}
```

上述代码无法通过编译，因为构造方法的两行语句：

```java
first = new T();
last = new T();
```

擦拭后实际上变成了：

```java
first = new Object();
last = new Object();
```

这样一来，创建`new Pair<String>()`和创建`new Pair<Integer>()`就全部成了`Object`，显然编译器要阻止这种类型不对的代码。

要实例化`T`类型，我们必须借助额外的`Class<T>`参数：

```java
public class Pair<T> {
    private T first;
    private T last;
    public Pair(Class<T> clazz) {
        first = clazz.newInstance();
        last = clazz.newInstance();
    }
}
```

上述代码借助`Class<T>`参数并通过反射来实例化`T`类型，使用的时候，也必须传入`Class<T>`。例如：

```java
Pair<String> pair = new Pair<>(String.class);
```

因为传入了`Class<String>`的实例，所以我们借助`String.class`就可以实例化`String`类型。


子类可以获取父类的泛型类型

一个类可以继承自一个泛型类。例如：父类的类型是`Pair<Integer>`，子类的类型是`IntPair`，可以这么继承：

```java
public class IntPair extends Pair<Integer> {
}
```

使用的时候，因为子类`IntPair`并没有泛型类型，所以，正常使用即可：

```java
IntPair ip = new IntPair(1, 2);
```

前面讲了，我们无法获取`Pair<T>`的`T`类型，即给定一个变量`Pair<Integer> p`，无法从`p`中获取到`Integer`类型。

但是，在父类是泛型类型的情况下，编译器就必须把类型`T`（对`IntPair`来说，也就是`Integer`类型）保存到子类的class文件中，不然编译器就不知道`IntPair`只能存取`Integer`这种类型。

在继承了泛型类型的情况下，子类可以获取父类的泛型类型。例如：`IntPair`可以获取到父类的泛型类型`Integer`。获取父类的泛型类型代码比较复杂：

```java
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

public class Main {
    public static void main(String[] args) {
        Class<IntPair> clazz = IntPair.class;
        Type t = clazz.getGenericSuperclass();
        if (t instanceof ParameterizedType) {
            ParameterizedType pt = (ParameterizedType) t;
            Type[] types = pt.getActualTypeArguments(); // 可能有多个泛型类型
            Type firstType = types[0]; // 取第一个泛型类型
            Class<?> typeClass = (Class<?>) firstType;
            System.out.println(typeClass); // Integer
        }
    }
}

class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}

class IntPair extends Pair<Integer> {
    public IntPair(Integer first, Integer last) {
        super(first, last);
    }
}
```

### 5.2.4 extends通配符





# 6 集合



# 7 IO


# 8 多线程
## 8.1 多线程基础
现代操作系统都可以执行多个任务。多任务就是同时运行多个任务，就像我同时开着微信聊天，又同时播放着网易云。
CPU执行代码都是一条一条顺序执行的，但是即时是单核CPU，也可以同时运行多个任务。因为操作系统执行多任务实际上就是让CPU对多个任务轮流交替执行。
假如说，我有三门作业要做，语文、数学、英语，我做一分钟语文，做一分钟数学，再做一分钟英语，循环往复，是不是看起来就像同时在做三门作业一样。

类似的，操作系统让多个任务交替执行的

### 进程
在计算机中，我们把一个任务称为一个进程，浏览器是一个进程，视频播放器是另一个进程。
某些进程内部还需要同时执行多个子任务。例如，我们在使用word时，word可以让我们一边打字，以便进行拼写检查，同时还可以在后台进行打印，我们把子任务称为线程。
进程和线程的关系就是：一个进行可以包含一个或多个线程，但至少会有一个线程。
![[Pasted image 20251207164359.png]]
操作系统导读的最小任务单位其实不是进程，而是线程。如何调度线程完全由操作系统决定，程序自己能决定什么时候执行，以及执行多长时间

因为同一个应用程序，既可以有多个进程，也可以也有多个线程，因此，实现多任务的方法，有以下几种：
多进程模式（每一个 进程只有一个线程）：
![[Pasted image 20251207171330.png]]

多线程模式（一个进程有多个线程）：
![[Pasted image 20251207171405.png]]

多进程+多线程模式（复杂度最高）：
![[Pasted image 20251207171436.png]]

### 进程 vs 线程
和多线程相比，多进程的缺点在于：
- 创建进程比创建线程开销大，尤其在Windows系统上；
- 进程间通信比线程间通信要慢，因为线程间通信就是读写同一个变量，速度很快

多进程的有点子啊与：
多进程稳定性比多线程高，因为多进程的情况下，一个进程崩溃不会影响其他进程，而在多线程下，任何一个线程崩溃会导致整个进程崩溃

### 多线程
Java语言内置了多线程支持：一个Java程序实际上是一个jvm进程，jvm进程用一个主线程来执行main（）方法，在main（）方法内部，我们又可以启动多个线程。此外，jvm还有负责垃圾回收的其他工作线程等。

因此，对于大多数Java程序来说，我们说多任务，实际上是说如何使用多线程实现多任务。

和单线程相比，多线程编程的特点在于：多线程经常需要读写共享数据，并且需要同步。例如，播放电影时，就必须由一个线程播放视频，另一个线程播放音频，两个线程需要协调运行，否则画面和声音就不同步。因此，多线程编程的复杂度高，调试更困难。

Java多线程编程的特点又在于：

- 多线程模型是Java程序最基本的并发模型；
- 后续读写网络、数据库、Web开发等都依赖Java多线程模型。

## 8.2 创建新线程
Java中要创建一个线程，要实例化一个`Thread`实例，然后调用它的`start()`方法：
```java
// 多线程
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread();
        t.start(); // 启动新线程
    }
}

```

![[Pasted image 20251207173652.png]]

整个运行后是什么都没有的，所以我们需要从`Thread`派生一个自定义类，然乎覆写`run（）`方法
![[Pasted image 20251207174325.png]]


或者是创建`Thread`实例时，传入一个`Runable`实例，但是要提前写一个实现`Runnable`接口的实现类，因为那个`Thread`也是实现类`Runnable`接口
![[Pasted image 20251207174745.png]]

![[Pasted image 20251207174753.png]]

```java
// 多线程
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(new MyRunnable());
        t.start(); // 启动新线程
    }
}

class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("start new thread!");
    }
}
```

那么使用线程执行打印语句，和直接在main（）方法执行有什么区别

可以看以下代码
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("main start...");
        Thread t = new Thread() {
            public void run() {
                System.out.println("thread run...");
                System.out.println("thread end.");
            }
        };
        t.start();
        System.out.println("main end...");
    }
}

```

我们再来看线程的执行顺序：

1. `main`线程肯定是先打印`main start`，再打印`main end`；
2. `t`线程肯定是先打印`thread run`，再打印`thread end`。

但是，除了可以肯定，`main start`会先打印外，`main end`打印在`thread run`之前、`thread end`之后或者之间，都无法确定。因为从`t`线程开始运行以后，两个线程就开始同时运行了，并且由操作系统调度，程序本身无法确定线程的调度顺序。

要模拟并发执行的效果，我们可以在线程中调用`Thread.sleep()`，强迫当前线程暂停一段时间：


```java
package demo1208;  
  
public class Demo02 {  
    public static void main(String[] args) {  
        System.out.println("main start");  
        Thread thread1 = new Thread() {  
            @Override  
            public void run() {  
                System.out.println("thread1 run");  
  
                try {  
                    Thread.sleep(10);  
                } catch (InterruptedException e) {  
                    System.out.println("thread1 end");  
                }  
            }  
        };  
        thread1.start();  
  
        try {  
            Thread.sleep(20);  
        } catch (InterruptedException e) {  
            System.out.println("main end");  
        }  
    }  
}
```


## 8.3 线程的状态

在Java程序中，一个线程对象只能调用一次`start()`方法启动新线程，并在新线程中执行`run()`方法，一旦`run()`方法执行完毕，线程就结束了
Java线程状态有以下几种

- New：新创建的线程，尚未执行；
- Runnable：运行中的线程，正在执行`run()`方法的Java代码；
- Blocked：运行中的线程，因为某些操作被阻塞而挂起；
- Waiting：运行中的线程，因为某些操作在等待中；
- Timed Waiting：运行中的线程，因为执行`sleep()`方法正在计时等待；
- Terminated：线程已终止，因为`run()`方法执行完毕。
![[Pasted image 20251208160620.png]]
当线程启动后，它可以在`Runnable`、`Blocked`、`Waiting`和`Timed Waiting`这几个状态之间切换，直到最后变成`Terminated`状态，线程终止。

线程终止的原因有：

- 线程正常终止：`run()`方法执行到`return`语句返回；
- 线程意外终止：`run()`方法因为未捕获的异常导致线程终止；
- 对某个线程的`Thread`实例调用`stop()`方法强制终止（强烈不推荐使用）。

一个线程还可以等待另一个线程直到其运行结束。例如，`main`线程在启动`t`线程后，可以通过`t.join()`等待`t`线程结束后再继续运行：

```java
// 多线程
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            System.out.println("hello");
        });
        System.out.println("start");
        t.start(); // 启动t线程
        t.join(); // 此处main线程会等待t结束
        System.out.println("end");
    }
}
```

当`main`线程对线程对象`t`调用`join()`方法时，主线程将等待变量`t`表示的线程运行结束，即`join`就是指等待该线程结束，然后才继续往下执行自身线程。所以，上述代码打印顺序可以肯定是`main`线程先打印`start`，`t`线程再打印`hello`，`main`线程最后再打印`end`。

如果`t`线程已经结束，对实例`t`调用`join()`会立刻返回。此外，`join(long)`的重载方法也可以指定一个等待时间，超过等待时间后就不再继续等待。
## 8.4 中断线程

如果线程需要执行一个长时间任务，就可能需要能中断线程。中断线程就是其他线程给该线程发一个信号，该线程收到信号后结束执行`run()`方法，使得自身线程能立刻结束运行。

我们举个栗子：假设从网络下载一个100M的文件，如果网速很慢，用户等得不耐烦，就可能在下载过程中点“取消”，这时，程序就需要中断下载线程的执行。

中断一个线程非常简单，只需要在其他线程中对目标线程调用`interrupt()`方法，目标线程需要反复检测自身状态是否是interrupted状态，如果是，就立刻结束运行。

我们还是看示例代码：
```java
// 中断线程
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new MyThread();
        t.start();
        Thread.sleep(1); // 暂停1毫秒
        t.interrupt(); // 中断t线程
        t.join(); // 等待t线程结束
        System.out.println("end");
    }
}

class MyThread extends Thread {
    public void run() {
        int n = 0;
        while (! isInterrupted()) {
            n ++;
            System.out.println(n + " hello!");
        }
    }
}
```
仔细看上述代码，`main`线程通过调用`t.interrupt()`方法中断`t`线程，但是要注意，`interrupt()`方法仅仅向`t`线程发出了“中断请求”，至于`t`线程是否能立刻响应，要看具体代码。而`t`线程的`while`循环会检测`isInterrupted()`，所以上述代码能正确响应`interrupt()`请求，使得自身立刻结束运行`run()`方法。

如果线程处于等待状态，例如，`t.join()`会让`main`线程进入等待状态，此时，如果对`main`线程调用`interrupt()`，`join()`方法会立刻抛出`InterruptedException`，因此，目标线程只要捕获到`join()`方法抛出的`InterruptedException`，就说明有其他线程对其调用了`interrupt()`方法，通常情况下该线程应该立刻结束运行。

我们来看下面的示例代码：
```java
// 中断线程
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new MyThread();
        t.start();
        Thread.sleep(1000);
        t.interrupt(); // 中断t线程
        t.join(); // 等待t线程结束
        System.out.println("end");
    }
}

class MyThread extends Thread {
    public void run() {
        Thread hello = new HelloThread();
        hello.start(); // 启动hello线程
        try {
            hello.join(); // 等待hello线程结束
        } catch (InterruptedException e) {
            System.out.println("interrupted!");
        }
        hello.interrupt();
    }
}

class HelloThread extends Thread {
    public void run() {
        int n = 0;
        while (!isInterrupted()) {
            n++;
            System.out.println(n + " hello!");
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                break;
            }
        }
    }
}
```

`main`线程通过调用`t.interrupt()`从而通知`t`线程中断，而此时`t`线程正位于`hello.join()`的等待中，此方法会立刻结束等待并抛出`InterruptedException`。由于我们在`t`线程中捕获了`InterruptedException`，因此，就可以准备结束该线程。在`t`线程结束前，对`hello`线程也进行了`interrupt()`调用通知其中断。如果去掉这一行代码，可以发现`hello`线程仍然会继续运行，且JVM不会退出。
![[Pasted image 20251208173800.png]]
另一个常用的中断线程的方法是设置标志位。我们通常会用一个`running`标志位来标识线程是否应该继续运行，在外部线程中，通过把`HelloThread.running`置为`false`，就可以让线程结束：

```java
// 中断线程
public class Main {
    public static void main(String[] args)  throws InterruptedException {
        HelloThread t = new HelloThread();
        t.start();
        Thread.sleep(1);
        t.running = false; // 标志位置为false
    }
}

class HelloThread extends Thread {
    public volatile boolean running = true;
    public void run() {
        int n = 0;
        while (running) {
            n ++;
            System.out.println(n + " hello!");
        }
        System.out.println("end!");
    }
}
```

注意到`HelloThread`的标志位`boolean running`是一个线程间共享的变量。线程间共享变量需要使用`volatile`关键字标记，确保每个线程都能读取到更新后的变量值。

为什么要对线程间共享的变量用关键字`volatile`声明？这涉及到Java的内存模型。在Java虚拟机中，变量的值保存在主内存中，但是，当线程访问变量时，它会先获取一个副本，并保存在自己的工作内存中。如果线程修改了变量的值，虚拟机会在某个时刻把修改后的值回写到主内存，但是，这个时间是不确定的！

```
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
           Main Memory
│                               │
   ┌───────┐┌───────┐┌───────┐
│  │ var A ││ var B ││ var C │  │
   └───────┘└───────┘└───────┘
│     │ ▲               │ ▲     │
 ─ ─ ─│─│─ ─ ─ ─ ─ ─ ─ ─│─│─ ─ ─
      │ │               │ │
┌ ─ ─ ┼ ┼ ─ ─ ┐   ┌ ─ ─ ┼ ┼ ─ ─ ┐
      ▼ │               ▼ │
│  ┌───────┐  │   │  ┌───────┐  │
   │ var A │         │ var C │
│  └───────┘  │   │  └───────┘  │
   Thread 1          Thread 2
└ ─ ─ ─ ─ ─ ─ ┘   └ ─ ─ ─ ─ ─ ─ ┘
```

这会导致如果一个线程更新了某个变量，另一个线程读取的值可能还是更新前的。例如，主内存的变量`a = true`，线程1执行`a = false`时，它在此刻仅仅是把变量`a`的副本变成了`false`，主内存的变量`a`还是`true`，在JVM把修改后的`a`回写到主内存之前，其他线程读取到的`a`的值仍然是`true`，这就造成了多线程之间共享的变量不一致。

因此，`volatile`关键字的目的是告诉虚拟机：

- 每次访问变量时，总是获取主内存的最新值；
- 每次修改变量后，立刻回写到主内存。

`volatile`关键字解决的是可见性问题：当一个线程修改了某个共享变量的值，其他线程能够立刻看到修改后的值。

如果我们去掉`volatile`关键字，运行上述程序，发现效果和带`volatile`差不多，这是因为在x86的架构下，JVM回写主内存的速度非常快，但是，换成ARM的架构，就会有显著的延迟。

## 8.5 守护线程
Java程序入口就是由jvm启动`main`线程又可以启动其他线程，当所有线程都运行结束时，jvm退出，进程结束
如果有一个线程没有退出，jvm进程就不会退出。所以，必须保证所有线程都能计时结束
但有一种线程的目的就是无限循环，例如，一个定时触发任务的线程：
```java
class TimerThread extends Thread {
    @Override
    public void run() {
        while (true) {
            System.out.println(LocalTime.now());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                break;
            }
        }
    }
}
```
如果这个线程不结束，JVM进程就无法结束。问题是，由谁负责结束这个线程？

然而这类线程经常没有负责人来负责结束它们。但是，当其他线程结束时，JVM进程又必须要结束，怎么办？

答案是使用守护线程（Daemon Thread）。

守护线程是指为其他线程服务的线程。在JVM中，所有非守护线程都执行完毕后，无论有没有守护线程，虚拟机都会自动退出。

因此，JVM退出时，不必关心守护线程是否已结束。

如何创建守护线程呢？方法和普通线程一样，只是在调用`start()`方法前，调用`setDaemon(true)`把该线程标记为守护线程：
```java
Thread t = new MyThread();
t.setDaemon(true);
t.start();
```

在守护线程中，编写代码要注意：守护线程不能持有任何需要关闭的资源，例如打开文件等，因为虚拟机退出时，守护线程没有任何机会来关闭文件，这会导致数据丢失。
## 8.6 线程同步
当多个线程同时运行时，现成的调度由操作系统决定，程序本身无法决定。因此，任何一个线程都有可能在任何指令出被操作系统暂停，然后再某个时间段后继续执行。
这个时候，有个惨线程模型下不存在的问题就来了；如果多个线程同时读写共享变量，会出现数据不一致的问题。
我们来看一个例子：

```java
// 多线程
public class Main {
    public static void main(String[] args) throws Exception {
        var add = new AddThread();
        var dec = new DecThread();
        add.start();
        dec.start();
        add.join();
        dec.join();
        System.out.println(Counter.count);
    }
}

class Counter {
    public static int count = 0;
}

class AddThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) { Counter.count += 1; }
    }
}

class DecThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) { Counter.count -= 1; }
    }
}
```

上面的代码很简单，两个线程同时对一个`int`变量进行操作，一个加10000次，一个减10000次，最后结果应该是0，但是，每次运行，结果实际上都是不一样的。

这是因为对变量进行读取和写入时，结果要正确，必须保证是原子操作。原子操作是指不能被中断的一个或一系列操作。

例如，对于语句：

```java
n = n + 1;
```

看上去是一行语句，实际上对应了3条指令：

```java
ILOAD
IADD
ISTORE
```

我们假设`n`的值是`100`，如果两个线程同时执行`n = n + 1`，得到的结果很可能不是`102`，而是`101`，原因在于：

```
┌───────┐     ┌───────┐
│Thread1│     │Thread2│
└───┬───┘     └───┬───┘
    │             │
    │ILOAD (100)  │
    │             │ILOAD (100)
    │             │IADD
    │             │ISTORE (101)
    │IADD         │
    │ISTORE (101) │
    ▼             ▼
```

如果线程1在执行`ILOAD`后被操作系统中断，此刻如果线程2被调度执行，它执行`ILOAD`后获取的值仍然是`100`，最终结果被两个线程的`ISTORE`写入后变成了`101`，而不是期待的`102`。

这说明多线程模型下，要保证逻辑正确，对共享变量进行读写时，必须保证一组指令以原子方式执行：即某一个线程执行时，其他线程必须等待：

```
┌───────┐     ┌───────┐
│Thread1│     │Thread2│
└───┬───┘     └───┬───┘
    │             │
    │-- lock --   │
    │ILOAD (100)  │
    │IADD         │
    │ISTORE (101) │
    │-- unlock -- │
    │             │-- lock --
    │             │ILOAD (101)
    │             │IADD
    │             │ISTORE (102)
    │             │-- unlock --
    ▼             ▼
```

通过加锁和解锁的操作，就能保证3条指令总是在一个线程执行期间，不会有其他线程会进入此指令区间。即使在执行期线程被操作系统中断执行，其他线程也会因为无法获得锁导致无法进入此指令区间。只有执行线程将锁释放后，其他线程才有机会获得锁并执行。这种加锁和解锁之间的代码块我们称之为临界区（Critical Section），任何时候临界区最多只有一个线程能执行。

可见，保证一段代码的原子性就是通过加锁和解锁实现的。Java程序使用`synchronized`关键字对一个对象进行加锁：

```java
synchronized(lock) {
    n = n + 1;
}
```

`synchronized`保证了代码块在任意时刻最多只有一个线程能执行。我们把上面的代码用`synchronized`改写如下：

```java
// 多线程
public class Main {
    public static void main(String[] args) throws Exception {
        var add = new AddThread();
        var dec = new DecThread();
        add.start();
        dec.start();
        add.join();
        dec.join();
        System.out.println(Counter.count);
    }
}

class Counter {
    public static final Object lock = new Object();
    public static int count = 0;
}

class AddThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.count += 1;
            }
        }
    }
}

class DecThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.count -= 1;
            }
        }
    }
}
```

注意到代码：

```java
synchronized(Counter.lock) { // 获取锁
    ...
} // 释放锁
```

它表示用`Counter.lock`实例作为锁，两个线程在执行各自的`synchronized(Counter.lock) { ... }`代码块时，必须先获得锁，才能进入代码块进行。执行结束后，在`synchronized`语句块结束会自动释放锁。这样一来，对`Counter.count`变量进行读写就不可能同时进行。上述代码无论运行多少次，最终结果都是0。

使用`synchronized`解决了多线程同步访问共享变量的正确性问题。但是，它的缺点是带来了性能下降。因为`synchronized`代码块无法并发执行。此外，加锁和解锁需要消耗一定的时间，所以，`synchronized`会降低程序的执行效率。

我们来概括一下如何使用`synchronized`：

1. 找出修改共享变量的线程代码块；
2. 选择一个共享实例作为锁；
3. 使用`synchronized(lockObject) { ... }`。

在使用`synchronized`的时候，不必担心抛出异常。因为无论是否有异常，都会在`synchronized`结束处正确释放锁：

```java
public void add(int m) {
    synchronized (obj) {
        if (m < 0) {
            throw new RuntimeException();
        }
        this.value += m;
    } // 无论有无异常，都会在此释放锁
}
```

我们再来看一个错误使用`synchronized`的例子：

```java
// 多线程
public class Main {
    public static void main(String[] args) throws Exception {
        var add = new AddThread();
        var dec = new DecThread();
        add.start();
        dec.start();
        add.join();
        dec.join();
        System.out.println(Counter.count);
    }
}

class Counter {
    public static final Object lock1 = new Object();
    public static final Object lock2 = new Object();
    public static int count = 0;
}

class AddThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock1) {
                Counter.count += 1;
            }
        }
    }
}

class DecThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock2) {
                Counter.count -= 1;
            }
        }
    }
}
```

结果并不是0，这是因为两个线程各自的`synchronized`锁住的_不是同一个对象_！这使得两个线程各自都可以同时获得锁：因为JVM只保证同一个锁在任意时刻只能被一个线程获取，但两个不同的锁在同一时刻可以被两个线程分别获取。

因此，使用`synchronized`的时候，获取到的是哪个锁非常重要。锁对象如果不对，代码逻辑就不对。

我们再看一个例子：

```java
// 多线程
public class Main {
    public static void main(String[] args) throws Exception {
        var ts = new Thread[] { new AddStudentThread(), new DecStudentThread(), new AddTeacherThread(), new DecTeacherThread() };
        for (var t : ts) {
            t.start();
        }
        for (var t : ts) {
            t.join();
        }
        System.out.println(Counter.studentCount);
        System.out.println(Counter.teacherCount);
    }
}

class Counter {
    public static final Object lock = new Object();
    public static int studentCount = 0;
    public static int teacherCount = 0;
}

class AddStudentThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.studentCount += 1;
            }
        }
    }
}

class DecStudentThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.studentCount -= 1;
            }
        }
    }
}

class AddTeacherThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.teacherCount += 1;
            }
        }
    }
}

class DecTeacherThread extends Thread {
    public void run() {
        for (int i=0; i<10000; i++) {
            synchronized(Counter.lock) {
                Counter.teacherCount -= 1;
            }
        }
    }
}
```

上述代码的4个线程对两个共享变量分别进行读写操作，但是使用的锁都是`Counter.lock`这一个对象，这就造成了原本可以并发执行的`Counter.studentCount += 1`和`Counter.teacherCount += 1`，现在无法并发执行了，执行效率大大降低。实际上，需要同步的线程可以分成两组：`AddStudentThread`和`DecStudentThread`，`AddTeacherThread`和`DecTeacherThread`，组之间不存在竞争，因此，应该使用两个不同的锁，即：

`AddStudentThread`和`DecStudentThread`使用`lockStudent`锁：

```java
synchronized(Counter.lockStudent) {
    ...
}
```

`AddTeacherThread`和`DecTeacherThread`使用`lockTeacher`锁：

```java
synchronized(Counter.lockTeacher) {
    ...
}
```

这样才能最大化地提高执行效率。

**不需要synchronized的操作**

JVM规范定义了几种原子操作：

- 基本类型（`long`和`double`除外）赋值，例如：`int n = m`；
- 引用类型赋值，例如：`List<String> list = anotherList`。

`long`和`double`是64位数据，JVM没有明确规定64位赋值操作是不是一个原子操作，不过在x64平台的JVM是把`long`和`double`的赋值作为原子操作实现的。

单条原子操作的语句不需要同步。例如：

```java
public void set(int m) {
    synchronized(lock) {
        this.value = m;
    }
}
```

就不需要同步。

对引用也是类似。例如：

```java
public void set(String s) {
    this.value = s;
}
```

上述赋值语句并不需要同步。

但是，如果是多行赋值语句，就必须保证是同步操作，例如：

```java
class Point {
    int x;
    int y;
    public void set(int x, int y) {
        synchronized(this) {
            this.x = x;
            this.y = y;
        }
    }
}
```


==多线程连续读写多个变量时，同步的目的是为了保证程序逻辑正确！==

==不但写需要同步，读也需要同步：==


```java
class Point {
    int x;
    int y;

    public void set(int x, int y) {
        synchronized(this) {
            this.x = x;
            this.y = y;
        }
    }

    public int[] get() {
        int[] copy = new int[2];
        copy[0] = x;
        copy[1] = y;
    }
}
```

假定当前坐标是`(100, 200)`，那么当设置新坐标为`(110, 220)`时，上述未同步的多线程读到的值可能有：

- (100, 200)：x，y更新前；
- (110, 200)：x更新后，y更新前；
- (110, 220)：x，y更新后。

如果读取到`(110, 200)`，即读到了更新后的x，更新前的y，那么可能会造成程序的逻辑错误，无法保证读取的多个变量状态保持一致。

有些时候，通过一些巧妙的转换，可以把非原子操作变为原子操作。例如，上述代码如果改造成：

```java
class Point {
    int[] ps;
    public void set(int x, int y) {
        int[] ps = new int[] { x, y };
        this.ps = ps;
    }
}
```

就不再需要写同步，因为`this.ps = ps`是引用赋值的原子操作。而语句：

```java
int[] ps = new int[] { x, y };
```

这里的`ps`是方法内部定义的局部变量，每个线程都会有各自的局部变量，互不影响，并且互不可见，并不需要同步。

不过要注意，读方法在复制`int[]`数组的过程中仍然需要同步。


 **不可变对象无需同步**

如果多线程读写的是一个不可变对象，那么无需同步，因为不会修改对象的状态：

```java
class Data {
    List<String> names;
    void set(String[] names) {
        this.names = List.of(names);
    }
    List<String> get() {
        return this.names;
    }
}
```

注意到`set()`方法内部创建了一个不可变`List`，这个`List`包含的对象也是不可变对象`String`，因此，整个`List<String>`对象都是不可变的，因此读写均无需同步。

分析变量是否能被多线程访问时，首先要理清概念，多线程同时执行的是方法。对于下面这个例子：

```java
class Status {
    List<String> names;
    int x;
    int y;
    void set(String[] names, int n) {
        List<String> ns = List.of(names);
        this.names = ns;
        int step = n * 10;
        this.x += step;
        this.y += step;
    }
    StatusRecord get() {
        return new StatusRecord(this.names, this.x, this.y);
    }
}
```

如果有A、B两个线程，同时执行是指：

- 可能同时执行set()；
- 可能同时执行get()；
- 可能A执行set()，同时B执行get()。

类的成员变量`names`、`x`、`y`显然能被多线程同时读写，但局部变量（包括方法参数）如果没有“逃逸”，那么只有当前线程可见。局部变量`step`仅在`set()`方法内部使用，因此每个线程同时执行set时都有一份独立的step存储在线程的栈上，互不影响，但是局部变量`ns`虽然每个线程也各有一份，但后续赋值后对其他线程就变成可见了。对`set()`方法同步时，如果要最小化`synchronized`代码块，可以改写如下：

```java
void set(String[] names, int n) {
    // 局部变量其他线程不可见:
    List<String> ns = List.of(names);
    int step = n * 10;
    synchronized(this) {
        this.names = ns;
        this.x += step;
        this.y += step;
    }
}
```

因此，深入理解多线程还需理解变量在栈上的存储方式，基本类型和引用类型的存储方式也不同。

### 8.6.1 同步方法
Java程序依靠`synchronized`对线程进行同步，使用`sychornized`的时候，锁住的是哪个对象很重要。
让线程自己选择锁对象往往会使得代码逻辑混乱，也不利于封装。更好的方法是把`synchronized`逻辑封装起来。例如，我们编写一个计数器如下：

```java
public class Counter {
    private int count = 0;

    public void add(int n) {
        synchronized(this) {
            count += n;
        }
    }

    public void dec(int n) {
        synchronized(this) {
            count -= n;
        }
    }

    public int get() {
        return count;
    }
}
```

这样一来，线程调用`add()`、`dec()`方法时，它不必关心同步逻辑，因为`synchronized`代码块在`add()`、`dec()`方法内部。并且，我们注意到，`synchronized`锁住的对象是`this`，即当前实例，这又使得创建多个`Counter`实例的时候，它们之间互不影响，可以并发执行：

```java
var c1 = Counter();
var c2 = Counter();

// 对c1进行操作的线程:
new Thread(() -> {
    c1.add();
}).start();
new Thread(() -> {
    c1.dec();
}).start();

// 对c2进行操作的线程:
new Thread(() -> {
    c2.add();
}).start();
new Thread(() -> {
    c2.dec();
}).start();
```

现在，对于`Counter`类，多线程可以正确调用。

如果一个类被设计为允许多线程正确访问，我们就说这个类就是“线程安全”的（thread-safe），上面的`Counter`类就是线程安全的。Java标准库的`java.lang.StringBuffer`也是线程安全的。

还有一些不变类，例如`String`，`Integer`，`LocalDate`，它们的所有成员变量都是`final`，多线程同时访问时只能读不能写，这些不变类也是线程安全的。

最后，类似`Math`这些只提供静态方法，没有成员变量的类，也是线程安全的。

除了上述几种少数情况，大部分类，例如`ArrayList`，都是非线程安全的类，我们不能在多线程中修改它们。但是，如果所有线程都只读取，不写入，那么`ArrayList`是可以安全地在线程间共享的。



**没有特殊说明时，一个类默认是非线程安全的。**

我们再观察`Counter`的代码：

```java
public class Counter {
    public void add(int n) {
        synchronized(this) {
            count += n;
        }
    }
    ...
}
```

当我们锁住的是`this`实例时，实际上可以用`synchronized`修饰这个方法。下面两种写法是等价的：

写法一：
```java
public void add(int n) {
    synchronized(this) { // 锁住this
        count += n;
    } // 解锁
}
```

写法二：

```java
public synchronized void add(int n) { // 锁住this
    count += n;
} // 解锁
```

因此，用`synchronized`修饰的方法就是同步方法，它表示整个方法都必须用`this`实例加锁。

我们再思考一下，如果对一个静态方法添加`synchronized`修饰符，它锁住的是哪个对象？

```java
public synchronized static void test(int n) {
    ...
}
```

对于`static`方法，是没有`this`实例的，因为`static`方法是针对类而不是实例。但是我们注意到任何一个类都有一个由JVM自动创建的`Class`实例，因此，对`static`方法添加`synchronized`，锁住的是该类的`Class`实例。上述`synchronized static`方法实际上相当于：

```java
public class Counter {
    public static void test(int n) {
        synchronized(Counter.class) {
            ...
        }
    }
}
```

我们再考察`Counter`的`get()`方法：

```java
public class Counter {
    private int count;

    public int get() {
        return count;
    }
    ...
}
```

它没有同步，因为读一个`int`变量不需要同步。

然而，如果我们把代码稍微改一下，返回一个包含两个`int`的对象：

```java
public class Counter {
    private int first;
    private int last;

    public Pair get() {
        Pair p = new Pair();
        p.first = first;
        p.last = last;
        return p;
    }
    ...
}
```

就必须要同步了

### 8.6.2 死锁
Java的线程锁是可重入的锁
什么是可重入的锁？我们还是来看例子：

```java
public class Counter {
    private int count = 0;

    public synchronized void add(int n) {
        if (n < 0) {
            dec(-n);
        } else {
            count += n;
        }
    }

    public synchronized void dec(int n) {
        count += n;
    }
}
```

观察`synchronized`修饰的`add()`方法，一旦线程执行到`add()`方法内部，说明它已经获取了当前实例的`this`锁。如果传入的`n < 0`，将在`add()`方法内部调用`dec()`方法。由于`dec()`方法也需要获取`this`锁，现在问题来了：

对同一个线程，能否在获取到锁以后继续获取同一个锁？

答案是肯定的。JVM允许同一个线程重复获取同一个锁，这种能被同一个线程反复获取的锁，就叫做**可重入锁**。

由于Java的线程锁是可重入锁，所以，获取锁的时候，不但要判断是否是第一次获取，还要记录这是第几次获取。每获取一次锁，记录+1，每退出`synchronized`块，记录-1，减到0的时候，才会真正释放锁。

**死锁**

一个线程可以获取一个锁后，再继续获取另一个锁。例如：

```java
public void add(int m) {
    synchronized(lockA) { // 获得lockA的锁
        this.value += m;
        synchronized(lockB) { // 获得lockB的锁
            this.another += m;
        } // 释放lockB的锁
    } // 释放lockA的锁
}

public void dec(int m) {
    synchronized(lockB) { // 获得lockB的锁
        this.another -= m;
        synchronized(lockA) { // 获得lockA的锁
            this.value -= m;
        } // 释放lockA的锁
    } // 释放lockB的锁
}
```

在获取多个锁的时候，不同线程获取多个不同对象的锁可能导致死锁。对于上述代码，线程1和线程2如果分别执行`add()`和`dec()`方法时：

- 线程1：进入`add()`，获得`lockA`；
- 线程2：进入`dec()`，获得`lockB`。

随后：

- 线程1：准备获得`lockB`，失败，等待中；
- 线程2：准备获得`lockA`，失败，等待中。

此时，两个线程各自持有不同的锁，然后各自试图获取对方手里的锁，造成了双方无限等待下去，这就是死锁。

死锁发生后，没有任何机制能解除死锁，只能强制结束JVM进程。

因此，在编写多线程应用时，要特别注意防止死锁。因为死锁一旦形成，就只能强制结束进程。

那么我们应该如何避免死锁呢？答案是：线程获取锁的顺序要一致。即严格按照先获取`lockA`，再获取`lockB`的顺序，改写`dec()`方法如下：
```java
public void dec(int m) {
    synchronized(lockA) { // 获得lockA的锁
        this.value -= m;
        synchronized(lockB) { // 获得lockB的锁
            this.another -= m;
        } // 释放lockB的锁
    } // 释放lockA的锁
}
```
### 8.6.3 使用wait 和 notify









# 9 JDBC

先准备了一些数据来练习使用JDBC
```sql
-- 创建数据库learjdbc:
DROP DATABASE IF EXISTS learnjdbc;
CREATE DATABASE learnjdbc;

-- 创建登录用户learn/口令learnpassword
CREATE USER IF NOT EXISTS learn@'%' IDENTIFIED BY 'learnpassword';
GRANT ALL PRIVILEGES ON learnjdbc.* TO learn@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

-- 创建表students:
USE learnjdbc;
CREATE TABLE students (
  id BIGINT AUTO_INCREMENT NOT NULL,
  name VARCHAR(50) NOT NULL,
  gender TINYINT(1) NOT NULL,
  grade INT NOT NULL,
  score INT NOT NULL,
  PRIMARY KEY(id)
) Engine=INNODB DEFAULT CHARSET=UTF8;

-- 插入初始数据:
INSERT INTO students (name, gender, grade, score) VALUES ('小明', 1, 1, 88);
INSERT INTO students (name, gender, grade, score) VALUES ('小红', 1, 1, 95);
INSERT INTO students (name, gender, grade, score) VALUES ('小军', 0, 1, 93);
INSERT INTO students (name, gender, grade, score) VALUES ('小白', 0, 1, 100);
INSERT INTO students (name, gender, grade, score) VALUES ('小牛', 1, 2, 96);
INSERT INTO students (name, gender, grade, score) VALUES ('小兵', 1, 2, 99);
INSERT INTO students (name, gender, grade, score) VALUES ('小强', 0, 2, 86);
INSERT INTO students (name, gender, grade, score) VALUES ('小乔', 0, 2, 79);
INSERT INTO students (name, gender, grade, score) VALUES ('小青', 1, 3, 85);
INSERT INTO students (name, gender, grade, score) VALUES ('小王', 1, 3, 90);
INSERT INTO students (name, gender, grade, score) VALUES ('小林', 0, 3, 91);
INSERT INTO students (name, gender, grade, score) VALUES ('小贝', 0, 3, 77);

```


- JDBC是java语言操作关系型数据库的一套API
- JDBC本质上是官方定义的一套操作所有关系型数据库的规则，即接口，各个数据库厂商去实现这套接口，提供数据库驱动jar包，我们可以使用这套接口，JDBC，真正执行的代码是驱动jar包中的实现类
- JDBC好处：各个数据厂商使用相同的接口，java代码不需要针对不同数据库分别开发

![[Pasted image 20251213193839.png]]

## 9.1 快速入门
![[Pasted image 20251213194806.png]]


```java
package demo1213;  
  
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.Statement;  
  
/**  
 * JDBC快速入门  
 */  
  
  
public class JDBCDemo {  
    public static void main(String[] args) throws Exception {  
        //1.注册驱动  
        Class.forName("com.mysql.jdbc.Driver");  
  
        //2.获取链接  
        String url="jdbc:mysql://localhost:3306/learnjdbc";  
        String username="root";  
        String password="211266";  
        Connection connection = DriverManager.getConnection(url,username,password);  
  
        //3.定义sql  
        String sql = "update students set name = '梁瑞斌',gender = 1,grade = 6,score = 1000 where id = 2";  
  
        //4.获取执行sql的对象Statement  
        Statement statement = connection.createStatement();  
  
        //5.执行sql  
        int count  = statement.executeUpdate(sql);  
  
        //6.处理结果  
        System.out.println(count);  
  
        //7.释放资源  
        statement.close();  
        connection.close();  
    }  
}
```


![[Pasted image 20251213201218.png]]

![[Pasted image 20251213201237.png]]

这里那行红的表示我使用了过时的驱动类名
改成这个即可
![[Pasted image 20251213201618.png]]
至于刚刚为什么用那个过时的也可以是因为
![[Pasted image 20251213203047.png]]


**注意，这个jar包得提前给他处理一下，添加成库**

![[Pasted image 20251213202037.png]]

## 9.2 JDBC API 详解

### 9.2.1 DriverManager
- DriverManager（驱动管理类）作用：
     1.注册驱动
     2.获取数据库连接
注册驱动我们在上面的例子写的是
```java
Class.forName("com.mysql.jdbc.Driver");  
```
也不是用的DriverManager中的RegisterDiver()方法
上面那个是用反射直接加载了这个类，然后再看这个类中的代码，这里面有一部分静态代码块，这部分在被加载进来的时候会自动执行
![[Pasted image 20251213204340.png]]

在mysql5之后这行不用写也可以
自动加载jar包中META-INF/sevices/java.sql.Driver文件中的驱动类
![[Pasted image 20251213204646.png]]

获取连接
```java
DriverManager.getConnection(url,username,password);
```

![[Pasted image 20251213205129.png]]

### 9.2.2 Connection

- Connection(数据库连接对象)作用：
	- 获取执行sql的对象
	- 管理事务

![[Pasted image 20251213210413.png]]

![[Pasted image 20251213210459.png]]

我这里创建了两条sql语句，要让他们都执行成功后

# 10 常用API

## 10.1 Math
- 一个帮助我们用于进行数学结算的工具类
- 私有化构造方法，所有的方法都是静态的

**Math常用方法**

![[Pasted image 20260123121508.png]]


# 11 正则表达式
## 11.1 好处
- 一个正则表达式就是一个描述规则的字符串
- 只需要编写正确的规则，就可以让正则表达式引擎去判断目标字符串
- 正则表达式是一套标准，可以用于任何语言
- jdk内置正则表达式引擎：java.util.regex
![[Pasted image 20260312124222.png]]

**作用：**
	校验字符串是否满足规则
	在一段文本中查找满足要求的内容

## 11.2 基本规则
![[Pasted image 20260312130247.png]]
