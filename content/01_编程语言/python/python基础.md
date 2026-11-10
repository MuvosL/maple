前面的基础语法那些就不写了，选择 循环等就敲一敲就ok了
主要是下面的

# Python 推导式
python推导式是一种独特的数据处理方式，可以从一个数据序列构建另一个数据序列的结构体
python推导式是一种强大且简洁的语法，适用于生成列表、字典、集合和生成器

**列表推导式**
[表达式 for 变量 in 列表] 
[out_exp_res for out_exp in input_list]

或者 

[表达式 for 变量 in 列表 if 条件]
[out_exp_res for out_exp in input_list if condition]

- out_exp_res：列表生成元素表达式，可以是有返回值的函数。
- for out_exp in input_list：迭代 input_list 将 out_exp 传入到 out_exp_res 表达式中。
- if condition：条件语句，可以过滤列表中不符合条件的值。

```python
>>> names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
>>> new_names = [name.upper()for name in names if len(name)>3]
>>> print(new_names)
['ALICE', 'JERRY', 'WENDY', 'SMITH']
```


```python
>>> multiples = [i for i in range(30) if i % 3 == 0]
>>> print(multiples)
[0, 3, 6, 9, 12, 15, 18, 21, 24, 27]
```
![[Pasted image 20260323210109.png]]

元组推导式这里不太一样
![[Pasted image 20260323212314.png]]
它生成的不是元组，而是一个生成器对象
想要元组，可以使用tuple将其转换一下
![[Pasted image 20260323212602.png]]


列表和集合还有元组推导式的语法其实差不多，从直观现象来看，就是括号不一样
这里我重新梳理一下对这三种数据结构的认识，列表，有点像数组，但是它又可以用append对数组内容进行更改。元组，不可变。集合，无序的，并且成员不重复，用add进行添加，就像java中的set。字典，就是一堆的键值对集合


字典推导式这块儿我是有一下没看懂
![[Pasted image 20260323213428.png]]
不过敲了两下也是懂了点

# 迭代器与生成器
## 迭代器
迭代是访问集合元素的一种方式
迭代器是一个可以记住遍历的位置的对象。
迭代器对象从集合的第一个元素开始访问，知道所有的元素被访问结束。
有两个基本的方法，iter() 和 next()
字符串，列表或元组对象都可以用于创建迭代器

```python
#!/usr/bin/python3
 
import sys         # 引入 sys 模块
 
list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
 
while True:
    try:
        print (next(it))
    except StopIteration:
        sys.exit()
        
```

### 创建一个迭代器

把一个类作为一个迭代器使用需要在类中实现两个方法 __iter__() 与 __next__() 。

如果你已经了解的面向对象编程，就知道类都有一个构造函数，Python 的构造函数为 __init__(), 它会在对象初始化的时候执行。

更多内容查阅：[Python3 面向对象](https://www.runoob.com/python3/python3-class.html)

__iter__() 方法返回一个特殊的迭代器对象， 这个迭代器对象实现了 __next__() 方法并通过 StopIteration 异常标识迭代的完成。

__next__() 方法（Python 2 里是 next()）会返回下一个迭代器对象。

创建一个返回数字的迭代器，初始值为 1，逐步递增 1：

```python
class MyNumbers:
  def __iter__(self):
    self.a = 1
    return self
 
  def __next__(self):
    x = self.a
    self.a += 1
    return x
 
myclass = MyNumbers()
myiter = iter(myclass)
 
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
print(next(myiter))
```

### StopIteration

StopIteration 异常用于标识迭代的完成，防止出现无限循环的情况，在 __next__() 方法中我们可以设置在完成指定循环次数后触发 StopIteration 异常来结束迭代。

在 20 次迭代后停止执行：
![[Pasted image 20260324121606.png]]


## 生成器
在python中，使用了yield的函数被称为生成器（generator）

**yield** 是一个关键字，用于定义生成器函数，生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果。

生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果
跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点点理解，生成器就是一个迭代器


```python
import sys  
def fibonacci(n):  
    a,b,counter = 0,1,1  
    while True:  
        if (counter >= n):  
            return  
        yield a  
        a,b = b,a+b  
        counter += 1  
f = fibonacci(100)  
  
while True:  
    try:  
        print(next(f))  
    except StopIteration:  
        sys.exit()
```
这个yield
**详细步骤：**

1. **首次调用 `next(f)`**：
    
    - 进入函数，初始化 `a=0, b=1, counter=0`
        
    - 进入 `while True`循环
        
    - `if (counter > n)`为 `False`（`0 > 10`不成立）
        
    - 执行 `yield a`，**将 `a=0`返回给调用者，并在此处暂停**。此时 `print`输出 `0`。
        
    - **注意**：函数在 `yield`处暂停，局部变量（`a, b, counter`）的状态被保留。
        
    
2. **第二次调用 `next(f)`**：
    
    - 从上次暂停处（`yield a`之后）继续执行
        
    - 执行 `a, b = b, a + b`→ `a=1, b=0+1=1`
        
    - `counter += 1`→ `counter=1`
        
    - 回到 `while`循环开头
        
    - `if (counter > n)`为 `False`（`1 > 10`不成立）
        
    - 执行 `yield a`，返回当前 `a=1`并暂停。输出 `1`。
        
    
3. **第三次调用 `next(f)`**：
    
    - 从暂停处继续
        
    - `a, b = b, a + b`→ `a=1, b=1+1=2`
        
    - `counter=2`
        
    - `yield a`返回 `a=1`。输出 `1`。
        
    
4. **如此反复**，每次 `next(f)`都会：
    
    - 更新 `a, b`
        
    - 计数器加1
        
    - 返回当前的 `a`值
        
    
5. **当 `counter`变为 11 时**（即已生成第0到第10项，共11个数）：
    
    - `if (counter > n)`为 `True`（`11 > 10`）
        
    - 执行 `return`，这会导致生成器函数结束，并**自动抛出 `StopIteration`异常**。
        
    - 外层的 `except StopIteration`捕获异常，调用 `sys.exit()`退出程序。
        
    

**3. 关键点总结**

- **生成器函数**：使用 `yield`的函数，调用时返回一个生成器（迭代器）。
    
- **状态保持**：每次 `yield`暂停时，所有局部变量和执行位置都会被“冻结”，下次 `next()`时原样恢复。这就是为什么它能记住 `a, b, counter`的值。
    
- **执行流程**：生成器函数是“惰性”的，只有调用 `next()`时才执行一部分代码，并返回一个值。这非常适合生成大型或无限的序列（如斐波那契数列可以无限生成，但这里用 `n`限制了长度）。
    
- **与普通迭代器的对比**：
    
    - 之前的 `MyNumbers`类需要显式定义 `__iter__`和 `__next__`，并手动管理状态（`self.a`）。
        
    - 生成器函数通过 `yield`自动将普通函数转换为迭代器，状态管理由 Python 在幕后完成，代码更简洁。
        
    


# with

## with 语句的基本语法

### 基础用法

`with` 语句的基本形式如下：

## 语法格式
```python
with expression [as variable]:  
```


- `expression` 返回一个支持上下文管理协议的对象
- `as variable` 是可选的，用于将表达式结果赋值给变量
- 代码块执行完毕后，自动调用清理方法

### 文件操作示例

最常见的 `with` 语句应用是文件操作：

```python
with open('example.txt', 'r') as file:  
    content = file.read()  
    print(content)  
```


这个和java中的try with resources差不多

# 函数

![[Pasted image 20260324213532.png]]
像这种多变参数就是第一种，它会以元组的形式呈现
第二种两个✳会以字典的形式来呈现
![[Pasted image 20260324213702.png]]
![[Pasted image 20260324215023.png]]

# python装饰器
是python中的一种高级功能，允许动态地修改函数或类的行为，是一种函数，它接受一个函数作为参数，并返回一个新的函数或修改原来的函数
这个感觉有点类似于Java中的注解
