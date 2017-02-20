> easy ajax editing interface for mysql tables  

> 通过Ajax编辑数据库表实例

add.php

```php
<?php
    sleep(1); //模拟服务器延时
    include "header.php"; //引入连接数据库单元
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
    sleep(1);
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
    sleep(1);
    include "header.php";
    $id=$_GET["id"];
    $end=$_GET["end"];
    $update=$_GET["update"];
    $sql="update person set {$update}='{$end}' where id='$id'";
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

ajax.js

```js
/* ajax封装
 * @param  {object} obj
 */
function ajax(obj) {
    //判断输入格式是否正确
    if (typeof obj != "object") { //传入参数是否正确
        console.error("请输入正确的参数类型");
        return false;
    }
    if (obj.url == undefined) { //传入地址格式是否正确
        console.error("请输入正确的地址");
    }
    //对数值进行初始化
    var method = obj.method == undefined ? 'get' : obj.method; //string 使用何种方式传递get,post。默认为get
    var asynch = obj.asynch == undefined ? true : obj.asynch; //boolean 是否进行异步,默认为true
    var dataType = obj.dataType == undefined ? 'text' : obj.dataType; //string 传入的类型说明，默认为text
    var data = obj.data; //string,json  传递的数据
    var success = obj.success; //function 成功执行函数后的回调函数 
    var error = obj.error; //错误状态说明
    var str = ""; //储存传递数据
    //判断传入数值的类型，并进行相应操作
    switch (typeof data) {
    case "undefined":
        ;
        break;
    case "object":
        for (var i in obj.data) {
            str += i + '=' + obj.data[i] + '&'
        }
        str = str.slice(0, -1);
        break;
    case "string":
        str = obj.data;
        break;
    }
    //兼容的实例化XMLHttpRequest对象，并根据请求，数据类型的不同进行操作
    var xml = window.XMLHttpRequest ? new XMLHttpRequest : new ActiveXObject("Microsoft.XMLHTTP");
    if (method == "get") {
        xml.open('get', obj.url + '?' + str, asynch);
        xml.responseType = dataType;
        xml.send(null);
    } else {
        xml.open('post', obj.url, asynch);
        xml.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
        xml.responseType = dataType;
        xml.send(str);
    }
    //通过修改onreadystatechange函数进行错误判断，处理xml类型数据
    xml.onreadystatechange = function() {
        if (xml.readyState == 4) {
            if (xml.status == 200) {
                var obj;
                if (dataType == 'xml') {
                    obj = xml.responseXML;
                } else {
                    obj = xml.response;
                }
                if (success) {
                    success(obj);
                }
            }
            if (xml.status == 404) {
                var info = "页面找不到";
                error(info);
            }
            if (xml.status == 503) {
                var info = "服务暂时不可用";
                error(info);
            }
        }
    }
}
```

table.html

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
<html lang="en">
<head>
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8"/>
<title>通过ajax实现表格增删改查</title>
<script src="ajax.js"></script>
</head>
<style>
*{
padding:0;
margin:0;
}
table{
width:500px;
margin:0px auto;
border-collapse: collapse;
border:1px solid #000;
margin-top: 20px;
table-layout: fixed;
}
th,td{
width:200px;
border:1px solid #000;
height:40px;
text-align: center;
}
.add{
width:804px;
height:30px;
line-height: 30px;
text-align: center;
border:1px solid #000;
border-top: none;
text-decoration: none;
margin:0 auto;
font-size:30px;
cursor: pointer;
}
.pass{
width:60px;
height:30px;
line-height: 30px;
text-align: center;
background: red;
color:#fff;
border-top: none;
text-decoration: none;
margin-left:10px;
float:left;
cursor: pointer;
}
.wait{
width: 5px;
height: 10px;
background-color: #000;
position: fixed;
left: 0;right: 0;top: 0;bottom: 0;
margin: auto;
animation: wait 1s ease infinite alternate;
}
.wait::before{
width:100%;
height: 100%;
background-color: #000;
content: "";
position:absolute;
left: 10px;
display: block;
animation: wait 0.5s ease infinite alternate;
}
.wait::after{
width:100%;
height: 100%;
background-color: #000;
content: "";
position:absolute;
right: 10px;
display: block;
animation: wait 0.5s ease infinite alternate;
}
@keyframes wait{
0%{transform: scale(1,1.5);}
100%{transform: scale(1.2,1);}
}
input{
width:100px;
height:30px;
}
</style>
<script>
window.onload = function() {
	var wait = document.querySelector(".wait");
	wait.style.display = "block";
	var tbody = document.getElementsByTagName("tbody")[0]; //表主体
	ajax({
		url: "table.php",
		dataType: "json",
		success: function(e) {
			wait.style.display = "none";
			var str = "";
			for (var i = 0; i < e.length; i++) {
				str += "<tr id=" + e[i].id + ">"
				str += "<td attr='name'>" + e[i].name + "</td>"
				str += "<td attr='age'>" + e[i].age + "</td>"
				str += "<td attr='sex'>" + e[i].sex + "</td>"
				str += "<td>" + "<div class='pass'>删除</div>" + "</td>"
				str += "</tr>"
			}
			tbody.innerHTML = str;
		}
	})
	var add = document.querySelector(".add"); //添加控件
	add.onclick = function() {
		wait.style.display = "block";
		var tr = document.createElement("tr");
		ajax({
			url: "add.php",
			success: function(e) {
				console.log(e);
				tr.setAttribute("id", e);
				// 给tr添加属性id 属性值是e;
				wait.style.display = "none";
				var str = "";
				str += "<td attr='name'></td><td attr='age'></td><td attr='sex'></td><td>" + "<div class='pass'>删除</div>" + "</td>"
				tr.innerHTML = str;
				tbody.appendChild(tr);
			}
		})
	}
	// 删除
	// 因为js是单线程异步机制,所以pass获取不到,所以用时事件委派。
	tbody.onclick = function(e) {
		var target = e.target || e.srcElement;
		if (target.nodeName == "DIV") {
			wait.style.display = "block";
			var parent = target.parentNode.parentNode;
			var id = parent.id;
			ajax({
				url: "del.php",
				data: {
					id
				},
				success: function(e) {
					wait.style.display = "none";
					if (e == "OK") {
						tbody.removeChild(parent);
						console.log("删除成功");
					} else {
						console.log("删除不成功");
					}
				}
			})
		}
		// 修改
		function getChilds(obj, type) {
			var type = type || "no";
			// 默认是no,其他情况另赋值
			var arr = [];
			// getClids返回值为集合，创建空数组接收集合
			var childs = obj.childNodes;
			// 获取所有子节点
			for (var i = 0; i < childs.length; i++) {
				// 遍历所有节点
				if (type == "yes") {
					// 要文本文档
					if (childs[i].nodeType == 1 || childs[i].nodeType == 3 && childs[i].nodeValue.replace(/^\s*|\s*$/g, "")) {
						// 是元素属性或者文本类型并且是没有空格的字符
						arr.push(childs[i]);
						// 存放到新数组
					}
				} else if (type == "no") {
					// 不要文本文档
					if (childs[i].nodeType == 1) {
						// 是元素文本
						arr.push(childs[i]);
						// 存入新数组
					}
				}
			}
			return arr;
			// 返回新数组
		}
		if (target.nodeName == "TD" && getChilds(target, "no").length == 0) {
			console.log(target.nodeType)
			var update = target.getAttribute("attr");
			var id = target.parentNode.id;
			var ad = document.createElement("input");
			var aa = target.innerHTML;
			target.innerHTML = "";
			ad.value = aa;
			target.appendChild(ad);
			ad.focus();
			ad.onblur = function() {
				var end = ad.value;
				if (end == aa || end == "") {
					target.innerHTML = aa;
				} else {
					ajax({
						url: "edit.php",
						data: {
							update: update,
							end: end,
							id: id
						},
						success: function(e) {
							console.log(e);
							if (e == 1) {
								target.innerHTML = end;
							} else {
								alert("修改失败");
							}
						}
					})
				}
			};
		}
	}
}
</script>
<body>
<table>
<thead>
<tr>
	<th>
		姓名
	</th>
	<th>
		年龄
	</th>
	<th>
		性别
	</th>
	<th>
		操作
	</th>
</tr>
</thead>
<tbody>
</tbody>
</table>
<div class="add">
	+
</div>
<div class="wait">
</div>
</body>
</html>
```



