>easy ajax editing interface for mysql tables
通过Ajax编辑数据库表实例

add.php
```php
<?php
	sleep(2);
	include "header.php";
	$sql="insert into person (id,name,age,sex) values ('','','','')";
	$aa->query($sql);
	if($aa->affected_rows>0){
		$id=$aa->insert_id;
		echo $id;
	}
?>
```
del.php
```php
<?php
	include "header.php";
	$id=$_GET["id"];
	$sql="delete from person where id=".$id;
	$aa->query($sql);
	if($row=$aa->affected_rows>0){
		echo "OK";
	}else{
		echo "ERROR";
	}
?>
```
header.php
```php
<?php
	$aa=new mysqli("localhost","root","","datebase");
	$aa->query("set names utf8");
?>
```
edit.php
```php
<?php
	include "header.php";
	$id=$_GET["id"];
	$end=$_GET["end"];
	$update=$_GET["update"];
	$sql="update stu set {$update}='{$end}' where id='$id'";
	$result=$aa->query($sql);
	echo $result;
?>
```
table.php
```php
<?php
	include "header.php";
	$result=$aa->query("select * from person");
	$array=array();
	while($row=$result->fetch_assoc()){ 
		$array[]=($row);
	}
	echo json_encode($array);
?>
```

