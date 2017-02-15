# AJAX简介

AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。  
AJAX = 异步 JavaScript和XML（标准通用标记语言的子集）。  
AJAX 是一种用于创建快速动态网页的技术。  
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。  
传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个网页页面。  

|  |  |
| :--- | :--- |
|  |  |

# 应用场景

####表单驱动的交互
传统的表单提交，在文本框输入内容后，点击按钮，后台处理完毕后，页面刷新，再回头检查是否刷新结果正确。使用Ajax，在点击sunmit按钮后，立刻进行异步处理，并在页面上快速显示了更新后的结果，这里没有整个页面刷新的问题。
####深层次的树的导航
深层次的级联菜单（树）的遍历是一项非常复杂的任务，使用JavaScript来控制显示逻辑，使用Ajax延迟加载更深层次的数据可以有效的减轻服务器的负担。
我们以前的对级联菜单的处理多数是这样的：
为了避免每次对菜单的操作引起的重载页面，不采用每次调用后台的方式，而是一次性将级联菜单的所有数据全部读取出来并写入数组，然后根据用户的操作用 JavaScript来控制它的子集项目的呈现，这样虽然解决了操作响应速度、不重载页面以及避免向服务器频繁发送请求的问题，但是如果用户不对菜单进行 操作或只对菜单中的一部分进行操作的话，那读取的数据中的一部分就会成为冗余数据而浪费用户的资源，特别是在菜单结构复杂、数据量大的情况下（比如菜单有 很多级、每一级菜又有上百个项目），这种弊端就更为突出。
如果在此案中应用Ajax后，结果就会有所改观：
在初始化页面时我们只读出它的第一级的所有数据并显示，在用户操作一级菜单其中一项时，会通过Ajax向后台请求当前一级项目所属的二级子菜单的所有数据，如 果再继续请求已经呈现的二级菜单中的一项时，再向后面请求所操作二级菜单项对应的所有三级菜单的所有数据，以此类推……这样，用什么就取什么、用多少就取 多少，就不会有数据的冗余和浪费，减少了数据下载总量，而且更新页面时不用重载全部内容，只更新需要更新的那部分即可，相对于后台处理并重载的方式缩短了 用户等待时间，也把对资源的浪费降到最低。
####用户间的交流响应
在众多人参与的交流讨论的场景下，最不爽的事情就是让用户一遍又一遍刷新页面以便知道是否有新的讨论出现。新的回复应该以最快的速度显示出来，而把用户从分神的刷新中解脱出来，Ajax是最好的选择。
####类似投票等场景
对于类似这样的场景中，如果提交过程需要达到40秒，很多的用户就会直接忽略过去而不会参与，但是Ajax可以把时间控制在1秒之内，从而更多的用户会加入进来。
####过滤场景
对数据使用过滤器，按照时间排序，或者按照时间和名称排序，开关过滤器等等。任何要求具备很高交互性数据操纵的场合都应该用JavaScript，而不是用一系列的服务器请求来完成。在每次数据更新后，再对其进行查找和处理需要耗费较多的时间，而Ajax可以加速这个过程。
####文本输入场景
在文本框等输入表单中给予输入提示，或者自动完成，可以有效的改善用户体验，尤其是那些自动完成的数据可能来自于服务器端的场合，Ajax是很好的选择。
#创建AJAX对象
创建对象
`
<script>

    var xmlhttp;
    if (window.XMLHttpRequest)
    {// code for IE7+, Firefox, Chrome, Opera, Safari
        xmlhttp=new XMLHttpRequest();
    }
    else
    {// code for IE6, IE5
        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
    }
</script>    
```
向服务器发送请求

请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法： 
open(method,url,async)

规定请求的类型、URL 以及是否异步处理请求。

method：请求的类型；GET 或 POST
url：文件在服务器上的位置
async：true（异步）或 false（同步）
send(string)

将请求发送到服务器。

string：仅用于 POST 请求

GET 请求
```
xmlhttp.open("GET","demo_get.php",true);
xmlhttp.send();
```
```
xmlhttp.open("GET","demo_get2.asp?fname=Bill&lname=Gates",true);
xmlhttp.send();
```

POST 请求 
setRequestHeader(header,value)向请求添加 HTTP 头。

header: 规定头的名称
value: 规定头的值
onreadystatechange 存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。 
readyState 存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。

0: 请求未初始化
1: 服务器连接已建立
2: 请求已接收
3: 请求处理中
4: 请求已完成，且响应已就绪
status

200: “OK”
404: 未找到页面
```
xmlhttp.open("POST","demo_post.php",true);
xmlhttp.send();
```
```
xmlhttp.open("POST","ajax_test.php",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill&lname=Gates");
```
Async = true

当使用 async=true 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：
```
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```
sync = false 
如需使用 async=false，请将 open() 方法中的第三个参数改为 false：
```
xmlhttp.open("GET","test1.txt",false);
xmlhttp.send();
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```

响应

responseText 获得字符串形式的响应数据。
responseXML 获得 XML 形式的响应数据。
```
<script type="text/javascript">
function loadXMLDoc()
{
var xmlhttp;
var txt,x,i;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    xmlDoc=xmlhttp.responseXML;
    txt="";
    x=xmlDoc.getElementsByTagName("title");
    for (i=0;i<x.length;i++)
      {
      txt=txt + x[i].childNodes[0].nodeValue + "<br />";
      }
    document.getElementById("myDiv").innerHTML=txt;
    }
  }
xmlhttp.open("GET","/example/xmle/books.xml",true);
xmlhttp.send();
}
</script>
```
请求的回调
```
<script type="text/javascript">
var xmlhttp;
function loadXMLDoc(url,cfunc)
{
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
  xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
  xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
xmlhttp.onreadystatechange=cfunc;
xmlhttp.open("GET",url,true);
xmlhttp.send();
}
function myFunction()
{
loadXMLDoc("/ajax/test1.txt",function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  });
}
</script>
```