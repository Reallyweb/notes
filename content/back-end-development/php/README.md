# PHP Introduction/PHP简介

PHP（外文名:PHP: Hypertext Preprocessor，中文名：“超文本预处理器”）是一种通用开源脚本语言。语法吸收了C语言、Java和Perl的特点，利于学习，使用广泛，主要适用于Web开发领域。PHP 独特的语法混合了C、Java、Perl以及PHP自创的语法。它可以比CGI或者Perl更快速地执行动态网页。用PHP做出的动态页面与其他的编程语言相比，PHP是将程序嵌入到HTML（标准通用标记语言下的一个应用）文档中去执行，执行效率比完全生成HTML标记的CGI要高许多；PHP还可以执行编译后代码，编译可以达到加密和优化代码运行，使代码运行更快。

### [php Syntax/php基本语法](content/back-end-development/php/php-syntax/README.md)

PHP 脚本可放置于文档中的任何位置。

PHP 脚本以`<?php`开头，以`?>`结尾：

```php
<?php
// 此处是 PHP 代码
?>
```

PHP 文件的默认文件扩展名是 ".php"。

PHP 文件通常包含 HTML 标签以及一些 PHP 脚本代码。

### PHP 支持三种注释：

```php
<!DOCTYPE html>
<html>
<body>
<?php
// 这是单行注释

# 这也是单行注释

/*这是多行注释块
它横跨了
多行*/

?>
</body>
</html>
```

### PHP 大小写敏感

在 PHP 中，所有用户定义的函数、类和关键词（例如 if、else、echo 等等）都对大小写不敏感。

```php
<!DOCTYPE html>
<html>
<body>

<?php
ECHO "Hello World!<br>";
echo "Hello World!<br>";
EcHo "Hello World!<br>";
?>

</body>
</html>
```

### PHP 变量

正如代数，PHP 变量可用于保存值（x=5）和表达式（z=x+y）。  
变量的名称可以很短（比如 x 和 y），也可以取更具描述性的名称（比如 carname、total\_volume）。  
PHP 没有创建变量的命令。  
变量会在首次为其赋值时被创建：

##### PHP 变量规则：

变量以 $ 符号开头，其后是变量的名称  
变量名称必须以字母或下划线开头  
变量名称不能以数字开头  
变量名称只能包含字母数字字符和下划线（A-z、0-9 以及 \_）  
变量名称对大小写敏感（$y 与 $Y 是两个不同的变量）

```php
<?php
$x=5;
$y=6;
$z=$x+$y;
echo $z;
?>
```

##### PHP 是一门类型松散的语言

在上面的例子中，请注意我们不必告知 PHP 变量的数据类型。  
PHP 根据它的值，自动把变量转换为正确的数据类型。  
在诸如 C 和 C++ 以及 Java 之类的语言中，程序员必须在使用变量之前声明它的名称和类型。

##### PHP 变量作用域

在 PHP 中，可以在脚本的任意位置对变量进行声明。  
变量的作用域指的是变量能够被引用/使用的那部分脚本。  
PHP 有三种不同的变量作用域：  
local（局部）  
global（全局）  
static（静态）

###### Local 和 Global 作用域

函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。  
函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。  
下面的例子测试了带有局部和全局作用域的变量：

```php
<?php
$x=5; // 全局作用域

function myTest() {
  $y=10; // 局部作用域
  echo "<p>测试函数内部的变量：</p>";
  echo "变量 x 是：$x";
  echo "<br>";
  echo "变量 y 是：$y";
} 

myTest();

echo "<p>测试函数之外的变量：</p>";
echo "变量 x 是：$x";
echo "<br>";
echo "变量 y 是：$y";
?>
```

在上例中，有两个变量 $x 和 $y，以及一个函数 myTest\(\)。$x 是全局变量，因为它是在函数之外声明的，而 $y 是局部变量，因为它是在函数内声明的。  
如果我们在 myTest\(\) 函数内部输出两个变量的值，$y 会输出在本地声明的值，但是无法 $x 的值，因为它在函数之外创建。  
然后，如果在 myTest\(\) 函数之外输出两个变量的值，那么会输出 $x 的值，但是不会输出 $y 的值，因为它是局部变量，并且在 myTest\(\) 内部创建。  
注释：您可以在不同的函数中创建名称相同的局部变量，因为局部变量只能被在其中创建它的函数识别。

##### PHP global 关键词

global 关键词用于访问函数内的全局变量。  
要做到这一点，请在（函数内部）变量前面使用 global 关键词：

```php
<?php
$x=5;
$y=10;
function myTest() {
  global $x,$y;
  $y=$x+$y;
}
myTest();
echo $y; // 输出 15
?>
```

PHP 同时在名为 $GLOBALS\[index\] 的数组中存储了所有的全局变量。下标存有变量名。这个数组在函数内也可以访问，并能够用于直接更新全局变量。  
上面的例子可以这样重写：

```php
<?php
$x=5;
$y=10;
function myTest() {
  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 
myTest();
echo $y; // 输出 15
?>
```

##### PHP static 关键词

通常，当函数完成/执行后，会删除所有变量。不过，有时我需要不删除某个局部变量。实现这一点需要更进一步的工作。  
要完成这一点，请在您首次声明变量时使用 static 关键词：

```php
<?php
function myTest() {
  static $x=0;
  echo $x;
  $x++;
}
myTest();
myTest();
myTest();
?>
```

然后，每当函数被调用时，这个变量所存储的信息都是函数最后一次被调用时所包含的信息。

### PHP echo 和 print 语句

##### PHP echo 和 print 语句

echo 和 print 之间的差异：  
echo - 能够输出一个以上的字符串  
print - 只能输出一个字符串，并始终返回 1  
提示：echo 比 print 稍快，因为它不返回任何值。

##### PHP echo 语句

echo 是一个语言结构，有无括号均可使用：echo 或 echo\(\)。

###### 显示字符串

下面的例子展示如何用 echo 命令来显示不同的字符串（同时请注意字符串中能包含 HTML 标记）：

```php
<?php
echo "<h2>PHP is fun!</h2>";
echo "Hello world!<br>";
echo "I'm about to learn PHP!<br>";
echo "This", " string", " was", " made", " with multiple parameters.";
?>
```

###### 显示变量

下面的例子展示如何用 echo 命令来显示字符串和变量：

```php
<?php
$txt1="Learn PHP";
$txt2="W3School.com.cn";
$cars=array("Volvo","BMW","SAAB");

echo $txt1;
echo "<br>";
echo "Study PHP at $txt2";
echo "My car is a {$cars[0]}";
?>
```

##### PHP print 语句

print 也是语言结构，有无括号均可使用：print 或 print\(\)。

###### 显示字符串

下面的例子展示如何用 print 命令来显示不同的字符串（同时请注意字符串中能包含 HTML 标记）：

```php
<?php
print "<h2>PHP is fun!</h2>";
print "Hello world!<br>";
print "I'm about to learn PHP!";
?>
```

###### 显示变量

下面的例子展示如何用 print 命令来显示字符串和变量：

```php
<?php
$txt1="Learn PHP";
$txt2="W3School.com.cn";
$cars=array("Volvo","BMW","SAAB");

print $txt1;
print "<br>";
print "Study PHP at $txt2";
print "My car is a {$cars[0]}";
?>
```

php操作mysql

var json\_uncode把php数组转为json格式。

js里单引号和双引号无区别

php 双引号功能比单引号多 单引号运行效率比双引号高

db.php文件代码

```html
<?php
$db=new mysqli("localhost","root","root","w1610");
//创建db访问数据库的对象,地址,用户名，密码，数据库名
$db->query("set names utf8");
//设置字符编码
?>
```

1.php文件代码,php和html可以混排；

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    table{
      width:600px;margin:0 auto;
      border:1px solid #000;
      border-collapse: collapse;
    }
    td,th{
      border:1px solid #000;
    }
    .add{
      display: block;
      width:598px;border:1px solid #000;
      height:30px;
      border-top:none;text-align: center;
      line-height:30px ;margin:0 auto;
      text-decoration: none;
    }
  </style>
</head>
<body>
  <table>
    <tr>
      <th>名字</th>
      <th>年龄</th>
      <th>性别</th>
      <th>操作</th>
    </tr>
    <?php
      include "db.php";
      //include语句会获取指定文件中存在的所有文本/代码/标记，并复制到使用 include 语句的文件中。
      $sql="select * from stu";
      $result=$db->query($sql);
      //根据指定的$sql查询语句去执行一个查询，并将结果返回给$db．赋给result；
      while ($row=$result->fetch_assoc()){
    ?>
          <tr>
              <td><?php echo $row["name"]?></td>
              <td><?php echo $row["age"]?></td>
              <td><?php echo $row["sex"]?></td>
              <td>
                <a href="del.php?id=<?php echo $row['id']?>">删除</a> <a href="edit.php?id=<?php echo $row['id']?>">编辑</a></td>
          </tr>
    <?php
      }
      ?>
  </table>
  <a href="" class="add">+</a>
</body>
</html>
```

del.php文件代码

```php
<?php
 include "db.php";
 $id=$_GET["id"];
 $db->query("delete from stu where id=".$id);
 if($db->affected_rows>0){
     echo "<script>alert('删除成功');location.href='1.php'</script>";
 }
?>
```



