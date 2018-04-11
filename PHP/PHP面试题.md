# php 面试题

1、用PHP打印出前一天的时间格式是2006-5-10 22:21:21

```php
echo date('Y-m-d H:i:s',strtotime('-1 day'));
```

2、如何实现字符串(英文)翻转?

```php
strrev($str);
```

3、MYSQL取得当前时间的函数是?，格式化日期的函数是?

```php
CURRENT_TIMESTAMP()
DATE_FORMAT()
select DATE_FORMAT("2011-11-21 10:10:10", "%Y-%m-%d");
```

4、实现中文字串截取无乱码的方法?

```php
mb_substr($str, 1, 1, "UTF-8");
```

5、用PHP写出显示客户端IP与服务器IP的代码?

```php
$_SERVER["REMOTE_ADDR"];
$_SERVER["SERVER_ADDR"];
```

6、如何修改SESSION的生存时间?

```php
session_set_cookie_params(1800);
```

7、在PHP中，heredoc是一种特殊的字符串，它的结束标志必须?

```php
$a = <<EOD
good test
EOD;
```

8、MySQL自增类型(通常为表ID字段)必需将其设为(?)字段

```mysql
auto_increment
```

9、请写出PHP5权限控制修饰符?

```php
public
private 
protected
```

10、请写出php5的构造函数和析构函数？

```php
public function __construct(){
}
public function __destruct(){
}
```

11、写一个函数，尽可能高效的，从一个标准 url 里取出文件的扩展名,例如: http://www.sina.com.cn/abc/de/fg.php?id=1 需要取出 php 或 .php

```php
$url = "http://www.sina.com.cn/abc/de/fg.php?id=1";
$arr = parse_url($url);
//Array ( [scheme] => http [host] => www.sina.com.cn [path] => /abc/de/fg.php [query] => id=1 ) 

$pathArr = pathinfo($arr['path']);
//Array ( [dirname] => /abc/de [basename] => fg.php [extension] => php [filename] => fg )

print_r($pathArr);
```

12、双引号和单引号的区别？

```
- 双引号解释变量，单引号不解释变量
- 双引号里插入单引号，其中单引号里如果有变量的话，变量解释
- 双引号的变量名后面必须要有一个非数字、字母、下划线的特殊字符，或者用{}讲变量括起来，否则会将变量名后面的部分当做一个整体，引起语法错误
- 双引号解释转义字符，单引号不解释转义字符，但是解释'\和\
- 能使单引号字符尽量使用单引号，单引号的效率比双引号要高（因为双引号要先遍历一遍，判断里面有没有变量，然后再进行操作，而单引号则不需要判断）
```

13、常用的超全局变量(8个)？

```
- $_GET ----->get传送方式
- $_POST ----->post传送方式
- $_REQUEST ----->可以接收到get和post两种方式的值
- $GLOBALS ----->所有的变量都放在里面
- $_FILES ----->上传文件使用
- $_SERVER ----->系统环境变量
- $_SESSION ----->会话控制的时候会用到
- $_COOKIE ----->会话控制的时候会用到
- $_ENV ------>
```

14、HTTP中POST、GET、PUT、DELETE方式的区别？

```
HTTP定义了与服务器交互的不同的方法，最基本的是POST、GET、PUT、DELETE，与其比不可少的URL的全称是资源描述符，我们可以这样理解：url描述了一个网络上资源，而post、get、put、delegate就是对这个资源进行增、删、改、查的操作！
```

15、表单中get和post提交方式的区别？

```php
- get是把参数数据队列加到提交表单的action属性所指的url中，值和表单内各个字段一一对应，从url中可以看到；post是通过HTTPPOST机制，将表单内各个字段与其内容防止在HTML的head中一起传送到action属性所指的url地址，用户看不到这个过程
- 对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据
- get传送的数据量较小(1024B)，post传送的数据量较大，一般被默认不受限制，但在理论上，IIS4中最大量为80kb，IIS5中为1000k，get安全性非常低，post安全性较高
```

16、echo、print_r、print、var_dump之间的区别？

```php
* echo、print是php语句，var_dump和print_r是函数
* echo 输出一个或多个字符串，中间以逗号隔开，没有返回值是语言结构而不是真正的函数，因此不能作为表达式的一部分使用
* print也是php的一个关键字，有返回值 只能打印出简单类型变量的值(如int，string)，如果字符串显示成功则返回true，否则返回false
* print_r 可以打印出复杂类型变量的值(如数组、对象）以列表的形式显示，并以array、object开头，但print_r输出布尔值和NULL的结果没有意义，因为都是打印"\n"，因此var_dump()函数更适合调试
* var_dump() 判断一个变量的类型和长度，并输出变量的数值
```

17、常见的HTTP状态码

```http
200 : 请求成功，请求的数据随之返回。
301 : 永久性重定向。
302 : 暂时行重定向。
401 : 当前请求需要用户验证。
403 : 服务器拒绝执行请求，即没有权限。
404 : 请求失败，请求的数据在服务器上未发现。
500 : 服务器错误。一般服务器端程序执行错误。
503 : 服务器临时维护或过载。这个状态时临时性的。
```

18、HTTP状态码分类

```http
1** - 信息，服务器收到的请求，需要请求者继续执行操作
2** - 成功，操作被成功接收并处理
3** - 重定向，需要进一步的操作以完成请求
4** - 客户端错误，请求包含语法错误或者无法完成请求
5** - 服务器错误，服务器在处理请求的过程中发生了错误
```

19、优化数据库的方法

```mysql
- 选取最适用的字段属性，尽可能减少定义字段宽度，尽量把字段设置NOTNULL，例如'省份'、'性别'最好适用ENUM
- 使用连接(JOIN)来代替子查询
- 适用联合(UNION)来代替手动创建的临时表
- 事务处理
- 锁定表、优化事务处理
- 适用外键，优化锁定表
- 建立索引
- 优化查询语句
```

20、对于大流量网站，采用什么方法来解决访问量的问题？

```
- 确认服务器硬件是否能够支持当前的流量
- 数据库读写分离，优化数据表
- 程序功能规则，禁止外部的盗链
- 控制大文件的下载
- 使用不同主机分流主要流量
```

21、isset、empty、is_null的区别

isset 判断变量是否定义或者是否为空

```php
  变量存在返回ture，否则返回false
  变量定义不赋值返回false
  unset一个变量，返回false
  变量赋值为null，返回false  
```

empty：判断变量的值是否为空，能转换为false的都是空，为空返回true，反之返回false。

```php
    "",0,"0",NULL，FALSE都认为为空，返回true
    没有任何属性的对象都认为是空
```

is_null：检测传入的值(值、变量、表达式)是否为null

```php
    定义了，但是赋值为Null
    定义了，但是没有赋值
    unset一个变量
```

22、简单描述mysql中，索引，主键，唯一索引，联合索引的区别，对数据库的性能有什么影响（从读写两方面）

```mysql
- 索引是一种特殊的文件(InnoDB数据表上的索引是表空间的一个组成部分)，它们包含着对数据表里所有记录的引用指针。
- 普通索引(由关键字KEY或INDEX定义的索引)的唯一任务是加快对数据的访问速度。
- 普通索引允许被索引的数据列包含重复的值。如果能确定某个数据列将只包含彼此各不相同的值，在为这个数据列创建索引的时候就应该用关键字UNIQUE把它定义为一个唯一索引。也就是说，唯一索引可以保证数据记录的唯一性。
- 主键，是一种特殊的唯一索引，在一张表中只能定义一个主键索引，主键用于唯一标识一条记录，使用关键字 PRIMARY KEY 来创建。
- 索引可以覆盖多个数据列，如像INDEX(columnA, columnB)索引，这就是联合索引。
- 索引可以极大的提高数据的查询速度，但是会降低插入、删除、更新表的速度，因为在执行这些写操作时，还要操作索引文件。
```

23、数据库中的事务是什么?

```
事务（transaction）是作为一个单元的一组有序的数据库操作。如果组中的所有操作都成功，则认为事务成功，即使只有一个操作失败，事务也不成功。如果所有操作完成，事务则提交，其修改将作用于所有其他数据库进程。如果一个操作失败，则事务将回滚，该事务所有操作的影响都将取消。ACID 四大特性,原子性、隔离性、一致性、持久性。
```

24、SQL注入漏洞产生的原因？如何防止？

```mysql
SQL注入产生的原因：程序开发过程中不注意规范书写sql语句和对特殊字符进行过滤，导致客户端可以通过全局变量POST和GET提交一些sql语句正常执行。

防止SQL注入的方式：
1、开启配置文件中的magic_quotes_gpc 和 magic_quotes_runtime设置
2、执行sql语句时使用addslashes进行sql语句转换
3、Sql语句书写尽量不要省略双引号和单引号。
4、过滤掉sql语句中的一些关键词：update、insert、delete、select、 * 。
5、提高数据库表和字段的命名技巧，对一些重要的字段根据程序的特点命名，取不易被猜到的。
6、Php配置文件中设置register_globals为off,关闭全局变量注册
7、控制错误信息，不要在浏览器上输出错误信息，将错误信息写到日志文件中。
```

25、对于关系型数据库而言，索引是相当重要的概念，请回答有关索引的几个问题

```
a)、索引的目的是什么？

1、快速访问数据表中的特定信息，提高检索速度
2、创建唯一性索引，保证数据库表中每一行数据的唯一性。
3、加速表和表之间的连接
4、使用分组和排序子句进行数据检索时，可以显著减少查询中分组和排序的时间
```

```
b)、索引对数据库系统的负面影响是什么？

负面影响：
创建索引和维护索引需要耗费时间，这个时间随着数据量的增加而增加；索引需要占用物理空间，不光是表需要占用数据空间，每个索引也需要占用物理空间；当对表进行增、删、改、的时候索引也要动态维护，这样就降低了数据的维护速度。
```

```
c)、为数据表建立索引的原则有哪些？

在最频繁使用的、用以缩小查询范围的字段上建立索引。
在频繁使用的、需要排序的字段上建立索引
```

```
d)、 什么情况下不宜建立索引？

对于查询中很少涉及的列或者重复值比较多的列，不宜建立索引。
对于一些特殊的数据类型，不宜建立索引，比如文本字段（text）等。
```

26、什么是面向对象？主要特征是什么？几大原则是什么？

```
面向对象是程序的一种设计模式，它利于提高程序的重用性，使程序机构更加清晰。 主要特征是：封装、继承、多态。
五大基本原则： 单一职责原则；开放封闭原则；替换原则； 依赖原则； 接口分离原则。
```

27、使用过 Memcache 缓存吗，如果使用过，能够简单的描述一下它的工作原理吗？

```
Memcahce 是把所有的数据保存在内存当中，采用 hash 表的方式，每条数据由 key 和 value 组成，每个 key 是独一无二的，当要访问某个值的时候先按照找到值，然后返回结果。
Memcahce 采用 LRU 算法来逐渐把过期数据清除掉。
```

28、Myql中的事务回滚机制概述？

```
事务是用户定义的一个数据库操作序列，这些操作要么全做要么全不做，是一个不可分割的工作单位，事务回滚是指将该事务已经完成的对数据库的更新操作撤销。

　　要同时修改数据库中两个不同表时，如果它们不是一个事务的话，当第一个表修改完，可能第二个表修改过程中出现了异常而没能修改，此时就只有第二个表依旧是未修改之前的状态，而第一个表已经被修改完毕。而当你把它们设定为一个事务的时候，当第一个表修改完，第二表修改出现异常而没能修改，第一个表和第二个表都要回到未修改的状态，这就是所谓的事务回滚。
```

29、array+array与array_merge()的区别 ？

```php
二者之间的区别是： 
1 键名为数字时，array_merge()不会覆盖掉原来的值，但＋合并数组则会把最先出现的值作为最终结果返回，而把后面的数组拥有相同键名的那些值“抛弃”掉（不是覆盖） 
2 键名为字符时，＋仍然把最先出现的值作为最终结果返回，而把后面的数组拥有相同键名的那些值“抛弃”掉，但array_merge()此时会覆盖掉前面相同键名的值
```

30、请列举最少3个php对象的魔术方法和说明它们的用途

```php
__construct() 实例化类时自动调用。
__destruct() 类对象使用结束时自动调用。
__set() 在给未定义的属性赋值的时候调用。
__get() 调用未定义的属性时候调用。
__isset() 使用isset()或empty()函数时候会调用。
__unset() 使用unset()时候会调用。
__sleep() 使用serialize序列化时候调用。
__wakeup() 使用unserialize反序列化的时候调用。
__call() 调用一个不存在的方法的时候调用。
__callStatic()调用一个不存在的静态方法是调用。
__toString() 把对象转换成字符串的时候会调用。比如 echo。
__invoke() 当尝试把对象当方法调用时调用。
__set_state() 当使用var_export()函数时候调用。接受一个数组参数。
__clone() 当使用clone复制一个对象时候调用。
```

31、在PHP中，当前脚本的名称（不包括路径和查询字符串）记录在预定义变量（1）中；而链接到当前页面的URL记录在预定义变量（2）中。

```php
(1)echo $_SERVER['PHP_SELF'];
(2)echo $_SERVER["HTTP_REFERER"];
```

32、在HTTP 1.0中，状态码 401 的含义是（1）；如果返回“找不到文件”的提示，则可用 header 函数，其语句为（2）。

```http
(1)未授权 
(2)header("HTTP/1.0 404 Not Found");
```

33、数组函数 arsort 的作用是（1）；语句 error_reporting(2047)的作用是（2）。

```
(1)对数组进行逆向排序并保持索引关系  
(2)All errors and warnings
```

34、语句include和require的区别是什么？为避免多次包含同一文件，可用什么？

```php

require->require是无条件包含也就是如果一个流程里加入require,无论条件成立与否都会先执行 require
include->include有返回值，而require没有(可能因为如此require的速度比include快)
注意:包含文件不存在或者语法错误的时候require是致命的,include不是。
①、PHP程序执行到require（）时，只会读取一次档案，故常放在程序开头，档案引入后PHP会将网页档重新编译，让引入档成为原先网页的一部分。
②、PHP程序执行到include（）时，每次皆会读取档案，故常用于流程控制的区段，如条件判断或循环中。
③、require() :无条件包含，如果文件不存在，会报出一个fatal error.脚本停止执行
④、include() : 有条件包含，如果文件不存在，会给出一个 warning，但脚本会继续执行
⑤、推荐使用require_once()和include_once()，可以检测文件是否有重复包含。
  
```

35、类的属性可以序列化后保存到 session 中，从而以后可以恢复整个类，这要用到的函数是？

```php
serialize() /unserialize()
```

36、请写一个函数，实现以下功能： 字符串“open_door” 转换成 “OpenDoor”、”make_by_id” 转换成 ”MakeById”。

```php
function func($str){
	$arr1=explode('_',$str);
	$str = implode(' ',$arr1);
	return str_replace(' ','',ucwords($str));
}
$str='open_door';
echo func($str);
```

37、如何用php的环境变量得到一个网页地址的内容？ip地址又要怎样得到？

```php
$_SERVSR['REQUEST_URI'];
$_SERVER['REMOTE_ADDR'];
```

38、表中有A B C三列,用SQL语句实现：当A列大于B列时选择A列否则选择B列，当B列大于C列时选择B列否则选择C列。

```mysql
select case when A>B then A else B end,
       case when B>C then B else C end
From test
```

39、请简述项目中优化sql语句执行效率的方法,从哪些方面,sql语句性能如何分析?

```
（1）选择最有效率的表名顺序
（2）WHERE子句中的连接顺序
（3）SELECT子句中避免使用‘*'
（4）用Where子句替换HAVING子句
（5）通过内部函数提高SQL效率
（6）避免在索引列上使用计算。
（7）提高GROUP BY 语句的效率, 可以通过将不需要的记录在GROUP BY 之前过滤掉。
```

40、mysql_fetch_row() 和 mysql_fetch_array() 有什么分别？

```php
mysql_fetch_row() 把数据库的一列储存在一个以零为基数的阵列中，第一栏在阵列的索引 0，第二栏在索引 1，如此类推。mysql_fetch_assoc() 把数据库的一列储存在一个关联阵列中，阵列的索引就是栏位名称，例如我的数据库查询送回“first_name”、“last_name”、 “email”三个栏位，阵列的索引便是“first_name”、“last_name”和“email”。mysql_fetch_array() 可以同时送回 mysql_fetch_row() 和 mysql_fetch_assoc() 的值。
```

41、写一段上传文件的代码。

upload.html

```php+HTML
<form enctype="multipart/form-data" method="POST" action="upload.php">
Send this file: <input name="name" type="file" />
<input type="submit" value="Send File" />
</form>	
```

upload.php

```php
$uploads_dir = '/uploads';
foreach ($_FILES["error"] as $key => $error) {
	if ($error == UPLOAD_ERR_OK) {
		$tmp_name = $_FILES["tmp_name"][$key];
		$name = $_FILES["name"][$key];
		move_uploaded_file($tmp_name, "$uploads_dir/$name");
	}
}
```

42、Mysql 的存储引擎,myisam和innodb的区别？

```mysql
a. MyISAM类型不支持事务处理等高级处理，而InnoDB类型支持.
b. MyISAM类型的表强调的是性能，其执行数度比InnoDB类型更快.
c. InnoDB不支持FULLTEXT类型的索引.
d. InnoDB中不保存表的具体行数，也就是说，执行select count(*) from table时，InnoDB要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可.
e. 对于AUTO_INCREMENT类型的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中，可以和其他字段一起建立联合索引。
f. DELETE FROM table时，InnoDB不会重新建立表，而是一行一行的删除。
g. LOAD TABLE FROM MASTER操作对InnoDB是不起作用的，解决方法是首先把InnoDB表改成MyISAM表，导入数据后再改成InnoDB表，但是对于使用的额外的InnoDB特性(例如外键)的表不适用.
h. MyISAM支持表锁，InnoDB支持行锁。
```

43、写代码来解决多进程/线程同时读写一个文件的问题

PHP是不支持多线程的，可以使用php的flock加锁函数实现。

```php
$fp = fopen("/tmp/lock.txt", "w+");
if (flock($fp, LOCK_EX)) { // 进行排它型锁定
    fwrite($fp, "Write something here\n");
  	flock($fp, LOCK_UN); // 释放锁定
} else {
	echo "Couldn't lock the file !";
}
fclose($fp);
```

44、MySQL数据库作发布系统的存储，一天五万条以上的增量，预计运维三年,怎么优化？

```mysql
a. 设计良好的数据库结构，允许部分数据冗余，尽量避免join查询，提高效率。
b. 选择合适的表字段数据类型和存储引擎，适当的添加索引。
c. mysql库主从读写分离。
d. 找规律分表，减少单表中的数据量提高查询速度。
e。添加缓存机制，比如memcached，apc等。
f. 不经常改动的页面，生成静态页面。
g. 书写高效率的SQL。比如 SELECT * FROM TABEL 改为 SELECT field_1, field_2, field_3 FROM TABLE.
```

45、请用最简单的语言告诉我PHP是什么？

```php
PHP全称：Hypertext Preprocessor，是一种用来开发动态网站的服务器脚本语言。
```

46、什么是MVC？

```
MVC由Model（模型）, View（视图）和Controller（控制器）组成，PHP MVC可以更高效地管理好3个不同层的PHP代码。
Model：数据信息存取层。
View：view层负责将应用的数据以特定的方式展现在界面上。
Controller：通常控制器负责从视图读取数据，控制用户输入，并向模型发送数据。
```

47、在页面中引用CSS有几种方式？

```
1.引用外部CSS文件
2.内部定义Style样式
3.内联样式
```

48、请问GET和POST方法有什么区别？

```
我们再网页上填写的表单信息都可以通过这两个方法将数据传递到服务器上，当我们使用GET方法是，所有的信息都会出现在URL地址中，并且使用GET方法最多只能传递1024个字符，所以如果在传输量小或者安全性不那么重要的情况下可以使用GET方法。说到POST方法，最多可以传输2MB字节的数据，而且可以根据需要调节。
```

49、PHP中获取图像尺寸大小的方法是什么？

```php
getimagesize() //获取图片的尺寸
Imagesx() //获取图片的宽度
Imagesy() //获取图片的高度
```

50、PHP中的PEAR是什么？

```php
PEAR也就是为PHP扩展与应用库（PHP Extension and Application Repository），它是一个PHP扩展及应用的一个代码仓库。
```

51、如何用PHP和MySQL上传视频？

```
我们可以在数据库中存放视频的地址，而不需要将真正的视频数据存在数据库中。可以将视频数据存放在服务器的指定文件夹下，上传的默认大小是2MB，但是我们也可以在php.ini文件中修改max_file size选项来改变。
```

52、PHP中的错误类型有哪些？

```
提示：这都是一些非常正常的信息，而非重大的错误，有些甚至不会展示给用户。比如访问不存在的变量。
警告：这是有点严重的错误，将会把警告信息展示给用户，但不会影响代码的输出，比如包含一些不存在的文件。
错误：这是真正的严重错误，比如访问不存在的PHP类。
```

53、如何不使用submit按钮来提交表单？

```javascript
如果我们不想用submit按钮来提交表单，我们也可以用超链接来提交，我们可以这样写代码：
<a href='javascript: document.myform.submit();'>Submit Me</a>
```

54、如何在PHP中定义常量？

```php
define ('Newconstant', 30);//PHP中使用Define () 来定义常量。
if (defined('Newconstant')) {//PHP中使用defined() 来检查某个名称的常量是否存在
    echo constant("Newconstant");//PHP中使用constant()返回一个常量的值
}
```

55、

```php
    $str1 = null;
    $str2 = false;
    echo $str1==$str2 ? '相等' : '不相等';
    $str3 = '';
    $str4 = 0;
    echo $str3==$str4 ? '相等' : '不相等';
    $str5 = 0;
    $str6 = '0';
    echo $str5===$str6 ? '相等' : '不相等';
    //相等 相等 不相等
```

56、

```php
    $a1 = null;
    $a2 = false;
    $a3 = 0;
    $a4 = '';
    $a5 = '0';
    $a6 = 'null';
    $a7 = array();
    $a8 = array(array());
    echo empty($a1) ? 'true' : 'false';
    echo empty($a2) ? 'true' : 'false';
    echo empty($a3) ? 'true' : 'false';
    echo empty($a4) ? 'true' : 'false';
    echo empty($a5) ? 'true' : 'false';
    echo empty($a6) ? 'true' : 'false';
    echo empty($a7) ? 'true' : 'false';
    echo empty($a8) ? 'true' : 'false';

    //true true true true true false true false
```

57、

```php
$a = "date";
$b = &$a;
echo $a; // date
echo $b; // date
$b = "date1";
echo $a; // date1
echo $b; // date1
unset($a);
echo $b; // date1

//就是给$a增加了一个别名$b，如果删除了$a，只是删除了这个变量的名字，并没有删除变量的内容，用别名还是可以把这个变量的内容显示出来
```

58、

```php
$count = 5;
function get_count(){
    static $count = 0;
    return $count++;
}
echo $count;
++$count;
echo get_count();
echo get_count();

//5 0 1
```

59、

```php
function get_arr($arr){
	unset($arr[0]);
}
$arr1 = array(1, 2);
$arr2 = array(1, 2);
get_arr(&$arr1);
get_arr($arr2);
echo count($arr1);
echo count($arr2);

//1 2
```

60、

```php
$GLOBALS['var1'] = 5;
$var2 = 1;
function get_value(){
	global $var2;
	$var1 = 0;
	return $var2++;
}
get_value();
echo $var1;
echo $var2;

//5 2
```

61、使用五种以上方式获取一个文件的扩展名
要求：dir/upload.image.jpg，找出 .jpg 或者 jpg ，
必须使用PHP自带的处理函数进行处理，方法不能明显重复，可以封装成函数，比如 get_ext1($file_name), get_ext2($file_name)

```php
//strrchr() 函数查找字符串在另一个字符串中最后一次出现的位置，并返回从该位置到字符串结尾的所有字符。
function get_ext1($file_name){
    return strrchr($file_name, '.');
}
//strrpos() 函数查找字符串在另一字符串中最后一次出现的位置。
function get_ext2($file_name){
    return substr($file_name, strrpos($file_name, '.'));
}
//explode()函数把字符串打散为数组。
//array_pop() 函数删除数组中的最后一个元素。返回被删除的值
function get_ext3($file_name){
    return array_pop(explode('.', $file_name));
}
//pathinfo()函数以数组或字符串的形式返回关于文件路径的信息。
//PATHINFO_DIRNAME - 只返回 dirname(dir)
//PATHINFO_BASENAME - 只返回 basename(upload.image.jpg)
//PATHINFO_EXTENSION - 只返回 extension(jpg)
function get_ext4($file_name){
    return pathinfo($file_name, PATHINFO_EXTENSION);
}
//strrev()函数反转字符串。
function get_ext5($file_name){
    return strrev(substr(strrev($file_name), 0, strpos(strrev($file_name), '.')));
}
```

62、 使用PHP描述冒泡排序和快速排序算法，对象可以是一个数组

//冒泡排序（数组排序）

```php
function bubble_sort($array){
    $count = count($array);
    if ($count <= 0) return false;
    for($i=0; $i<$count; $i++){
        for($j=$i; $j<$count-1; $j++){
            if ($array[$i] > $array[$j]){
                $tmp = $array[$i];
                $array[$i] = $array[$j];
                $array[$j] = $tmp;
            }
        }
    }
    return $array;
}
```

//快速排序（数组排序）

```php
function quick_sort($array) {
    if (count($array) <= 1) return $array;
    $key = $array[0];
    $left_arr = array();
    $right_arr = array();
    for ($i=1; $i<count($array); $i++){
        if ($array[$i] <= $key)
            $left_arr[] = $array[$i];
        else
            $right_arr[] = $array[$i];
    }
    $left_arr = quick_sort($left_arr);
    $right_arr = quick_sort($right_arr);
    return array_merge($left_arr, array($key), $right_arr);
}
```

63、使用PHP描述顺序查找和二分查找（也叫做折半查找）算法，顺序查找必须考虑效率，对象可以是一个有序数组
//二分查找（数组里查找某个元素）

```php
function bin_sch($array, $low, $high, $k){
    if ($low <= $high){
    	$mid = intval(($low+$high)/2);
    	if ($array[$mid] == $k){
    		return $mid;
    	}elseif ($k < $array[$mid]){
    		return bin_sch($array, $low, $mid-1, $k);
    	}else{
    		return bin_sch($array, $mid+1, $high, $k);
    	}
    }
    return -1;
}
```

//顺序查找（数组里查找某个元素）

```php
function seq_sch($array, $n, $k){
    $array[$n] = $k;
    for($i=0; $i<$n; $i++){
        if($array[$i]==$k){
            break;
        }
    }
    if ($i<$n){
        return $i;
    }else{
        return -1;
    }
}
```

64、写一个二维数组排序算法函数，能够具有通用性，可以调用php内置函数
//二维数组排序， $arr是数据，$keys是排序的健值，$order是排序规则，1是升序，0是降序

```php
function array_sort($arr, $keys, $order=0) {
    if (!is_array($arr)) {
        return false;
    }
    $keysvalue = array();
    foreach($arr as $key => $val) {
        $keysvalue[$key] = $val[$keys];
    }
    if($order == 0){
        asort($keysvalue);
    }else {
        arsort($keysvalue);
    }
    reset($keysvalue);
    foreach($keysvalue as $key => $vals) {
        $keysort[$key] = $key;
    }
    $new_array = array();
    foreach($keysort as $key => $val) {
        $new_array[$key] = $arr[$val];
    }
    return $new_array;
}
```
65、session与cookie的区别?

```php
session:储存用户访问的全局唯一变量,存储在服务器上的php指定的目录中的（session_dir）的位置进行的存放
cookie:用来存储连续訪問一个頁面时所使用，是存储在客户端，对于Cookie来说是存储在用户WIN的Temp目录中的。
两者都可通过时间来设置时间长短
```

66、有一个网页地址, 比如PHP开发资源网主页: http://www.php100.com/index.html,如何得到它的内容?

```php
方法1(对于PHP5及更高版本):
$readcontents = fopen(“http://www.php100.com/index.html”, “rb”);
$contents = stream_get_contents($readcontents);// stream_get_contents 取得字符串赋值给$contents
fclose($readcontents);
echo $contents;
```

```php
方法2:
echo file_get_contents(“http://www.php100.com/index.html”);
// file_get_contents() 函数把整个文件读入一个字符串中。
```

67、sort()、asort()、和 ksort() 有什么分别?它们分别在什么情况下使用?

```php
sort()
根据阵列中元素的值，以英文字母顺序排序，索引键会由 0 到 n-1 重新编号。主要是当阵列索引键的值无关疼痒时用来把阵列排序。
asort()
与 sort() 一样把阵列的元素按英文字母顺序来排列，不同的是所有索引键都获得保留，特别适合替联想阵列排序。
ksort()
根据阵列中索引键的值，以英文字母顺序排序，特别适合用于希望把索引键排序的联想阵列。
```

68、“===”是什么?试举一个“==”是真但“===”是假的例子。

```php
"==="是既可以返回布尔值“假”，也可以返回一个不是布尔值但却可以赋与“假”值的函式，strpos() 和 strrpos() 便是其中两个例子。

if (strpos("abc", "a") == true){ // 这部分永不会被执行，因为 "a" 的位置是 0，换算成布尔值“假”}
if (strpos("abc", "a") === true){ // 这部份会被执行，因为“===”保证函式 strpos() 的送回值不会换算成布尔值.}
```

69、PHP中对数组序列化和反序列化的函数是哪两个？

```php
serialize和unserialize函数
<?php
$a =array('a' => 'Apple' ,'b' => 'banana' , 'c' => 'Coconut');
//序列化数组
$s = serialize($a);
echo $s;
//输出结果：a:3:{s:1:"a";s:5:"Apple";s:1:"b";s:6:"banana";s:1:"c";s:7:"Coconut";}
echo'<br /><br />';
//反序列化
$o = unserialize($s);
print_r($o);
//输出结果 Array ( [a] => Apple [b] => banana [c] => Coconut )
?>
```

70、PHP中过滤HTML的函数是什么？经常用在哪些地方？

```php
strip_tags() 函数
strip_tags() 函数剥去HTML、XML 以及PHP 的标签。
```

71、写出把HTML中的js脚本过利率掉的正则表达式。

```php
<?php
$script="以下内容不显示：<script language='javascript'>alert('cc');</script>";
echo preg_replace("/<script[^>].*?>.*?</script>/si","替换内容",$script);
?>
$str = '';
$isMatched = preg_match('/\/<script[^>]*?>.*?<\/script>\/si /', $str, $matches);
var_dump($isMatched, $matches);
```

72、写出三个调用系统命令的函数？

```php
我们在执行linux系统的shell命令时，会用到 虽然这三个命令都能执行linux系统的shell命令，但是其实他们是有区别的：
system() 输出并返回最后一行shell结果。
exec() 不输出结果，返回最后一行shell结果，所有结果可以保存到一个返回的数组里面。
passthru() 只调用命令，把命令的运行结果原样地直接输出到标准输出设备上。
相同点：都可以获得命令执行的状态码
```

73、PHP把utf8转换成gbk的函数是？

```php
iconv函数可以转，但是由于字符集的问题，iconv 函数在utf8转 GBK 的时候，会存在一些问题，比如一些特殊字符类似中文“-”会导致无法转换，要加 //IGNORE 来保证执行
iconv("UTF-8", "GBK//IGNORE", $text);
mb_convert_encoding($str, "GBK", "UTF-8");
```

74、写一个函数将1234567890转换成1，234，567，890每3位用逗号隔开的形式。

```php
//方法一
$str='1234567890';
function str($str) {
	$str=strrev($str);
	$str=chunk_split($str,3,',');
	$str=strrev($str);
	$str=ltrim($str , ',');
	return $str;
}
echo str($str); 
```

```php
//方法二
function zhengstr($str){
	//计算字符串长度
	$strl=strlen($str);
	//echo $strl;
	//每3位加逗号，其余的也要使用逗号隔开。
	//求字符串长度对3的余数，用来计算逗号放的位置
	$y=$strl%3;
	$l=$strl-1;
	for($i=0;$i<=$l;$i++){
		//如果对3取余等于余数需要加逗号。并且排除(i=0)的情况
		if($i%3==$y && $i!=0){
			$newstr.=',';
		}
		$newstr.=$str{$i};
	}
	//返回处理后的字符串
	return $newstr;
}
echo zhengstr('1234567890');
```

```php
//方法三
function fanstr($str){
	//先将字符串反转
	$rstr=strrev($str);
	//求字符串长度 下标从0开始所以需要长度-1
	$l=strlen($rstr)-1;
	for($i=0;$i<=$l;$i++){
		//反转后字符串每3位加一个逗号，并且排除一种情况(i=0)
		if($i%3==0 && $i!=0){
			$newstr.=',';
		}
		$newstr.=$rstr{$i};
	}
	//最后再进行反转返回
	return strrev($newstr);
}
echo fanstr('1234567890');
```
75、下面的输出结果会是怎样？

```php
$x = 5;
echo $x;                   //5
echo "<br />";
echo $x+++$x++;            //11
echo "<br />";
echo $x;                   //7
echo "<br />";
echo $x---$x--;            //1
echo "<br />";
echo $x;                   //5
```

76、关于变量的引用；

```php
$a = '1';
$b = &$a;
$b = "2$b";
```

请问 `$a` 和 `$b`的值各位多少

部分第一时间会想到 `$a='1' $b='21'`,仔细一看 `$b=&$a`,这里`$b`是变量`$a`的引用而不是直接 赋值。

77、下面是true还是false？

```php
var_dump(0123 == 123);//var_dump(0123 == 123);// false,PHP会默认把0123当作8进制来处理，实际转化为10进制就是83，显然这不是相等的。
var_dump('0123' == 123);//var_dump('0123' == 123);// true这里php会非常有趣的将'0123'转换成一个数字而且默认去掉了前面的0也就是123==123
var_dump('0123' === 123);//var_dump('0123' === 123);// false很显然上面的问题已经说过了数字和字符串类型不一致。
```

78、下面的代码有什么问题吗？输出会是什么，怎样修复它

```php
$referenceTable = array();
$referenceTable['val1'] = array(1, 2);
$referenceTable['val2'] = 3;
$referenceTable['val3'] = array(4, 5);

$testArray = array();

$testArray = array_merge($testArray, $referenceTable['val1']);
var_dump($testArray);
$testArray = array_merge($testArray, $referenceTable['val2']);
var_dump($testArray);
$testArray = array_merge($testArray, $referenceTable['val3']);
var_dump($testArray);
```

实际输出如下：

```php
array(2) { [0]=> int(1) [1]=> int(2) }
NULL
NULL
```

运行的时候你或许还能看到下面的警告

```php
Warning: array_merge(): Argument #2 is not an array
Warning: array_merge(): Argument #1 is not an array
```

`array_merge`需要传入的参数都是数组，如果不是，则会返回null。
你可以这样修改

```php
$testArray = array_merge($testArray, (array)$referenceTable['val1']);
var_dump($testArray);
$testArray = array_merge($testArray, (array)$referenceTable['val2']);
var_dump($testArray);
$testArray = array_merge($testArray, (array)$referenceTable['val3']);
var_dump($testArray);
```

79、$x应该是输出什么？

```php
$x = true and false;
var_dump($x);
```

部分同学或许会第一时间想到false,实际上这里依旧是强调运算符的优先级，＝ 会比 and级别高点，因此等同下面的代码

```php
$x = true;
true and false
```

答案显而易见。

80、经过下面的运算 $x的值应该是多少？

```php
$x = 3 + "15%" + "$25"
```

答案是`18`，PHP是会根据上下文实现[类型的自动转换](http://www.php.net//manual/en/language.types.type-juggling.php)

上面的代码我们可以这样理解，如果我们在与字符串进行数学运算，实际php会尽可能将字符串中的数组进行转换，如果是数字开头的话则转换成改数字比如"15%"会变成15,如果不是数字开头则会变成0;上面的运算类似下面 ：

```php
$x = 3 + 15 + 0
```

81、运行下面的代码，`$text` 的值是多少？`strlen($text)`又会返回什么结果？

```php
$text = 'John ';
$text[10] = 'Doe';

//上面代码执行完毕后 $text = "John D"(John后面会有连续的5个空格)strlen($text)会返回11
//$text[10] = "Doe"给某个字符串具体的某个位置具体字符时候，实际只会把D赋给$text. 虽然$text才开始只有5个自负长度，但是php会默认填充空格。这和别的语言有些差别。
```

82、下面的输出结果会是什么？

```php
$v = 1;
$m = 2;
$l = 3;

if( ($l > $m) > $v){
    echo "yes";
}else{
    echo "no";
}
//实际的输出是"no",只要仔细分析就不难得出$l>$m 会转换成1 ，则这个时候再和$m比较。
```

83、执行下面代码`$x`会变成什么值呢？

```php
$x = NULL;

if ('0xFF' == 255) {
    $x = (int)'0xFF';
}
```

实际的运行结果是`$x=0`而不是255.首先`'oxFF' == 255`我们好判断，会进行转换将16进制数字转换成10进制数字，0xff -> 255.PHP使用`is_numeric_string` 判断字符串是否包含十六进制数字然后进行转换。但是`$x = (int)'0xFF';`是否也会变成255呢？显然不是，将一个字符串进行强制类型转换实际上用的是`convert_to_long`,它实际上是将字符串从左向右进行转换，遇到非数字字符则停止。因此`0xFF`到x就停止了。所以`$x=0`