# AJAX简介

AJAX即“Asynchronous Javascript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的网页开发技术。  
AJAX = 异步 `JavaScript`和`XML`（标准通用标记语言的子集）。  
`AJAX` 是一种用于创建快速动态网页的技术。  
通过在后台与服务器进行少量数据交换，`AJAX` 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。  
传统的网页（不使用 `AJAX`）如果需要更新内容，必须重载整个网页页面。

# 应用场景

#### 表单驱动的交互

传统的表单提交，在文本框输入内容后，点击按钮，后台处理完毕后，页面刷新，再回头检查是否刷新结果正确。使用`Ajax`，在点击`sunmit`按钮后，立刻进行异步处理，并在页面上快速显示了更新后的结果，这里没有整个页面刷新的问题。

#### 深层次的树的导航

深层次的级联菜单（树）的遍历是一项非常复杂的任务，使用`JavaScript`来控制显示逻辑，使用Ajax延迟加载更深层次的数据可以有效的减轻服务器的负担。  
我们以前的对级联菜单的处理多数是这样的：  
为了避免每次对菜单的操作引起的重载页面，不采用每次调用后台的方式，而是一次性将级联菜单的所有数据全部读取出来并写入数组，然后根据用户的操作用 JavaScript来控制它的子集项目的呈现，这样虽然解决了操作响应速度、不重载页面以及避免向服务器频繁发送请求的问题，但是如果用户不对菜单进行 操作或只对菜单中的一部分进行操作的话，那读取的数据中的一部分就会成为冗余数据而浪费用户的资源，特别是在菜单结构复杂、数据量大的情况下（比如菜单有 很多级、每一级菜又有上百个项目），这种弊端就更为突出。  
如果在此案中应用Ajax后，结果就会有所改观：  
在初始化页面时我们只读出它的第一级的所有数据并显示，在用户操作一级菜单其中一项时，会通过Ajax向后台请求当前一级项目所属的二级子菜单的所有数据，如 果再继续请求已经呈现的二级菜单中的一项时，再向后面请求所操作二级菜单项对应的所有三级菜单的所有数据，以此类推……这样，用什么就取什么、用多少就取 多少，就不会有数据的冗余和浪费，减少了数据下载总量，而且更新页面时不用重载全部内容，只更新需要更新的那部分即可，相对于后台处理并重载的方式缩短了 用户等待时间，也把对资源的浪费降到最低。

#### 用户间的交流响应

在众多人参与的交流讨论的场景下，最不爽的事情就是让用户一遍又一遍刷新页面以便知道是否有新的讨论出现。新的回复应该以最快的速度显示出来，而把用户从分神的刷新中解脱出来，Ajax是最好的选择。

#### 类似投票等场景

对于类似这样的场景中，如果提交过程需要达到40秒，很多的用户就会直接忽略过去而不会参与，但是Ajax可以把时间控制在1秒之内，从而更多的用户会加入进来。

#### 过滤场景

对数据使用过滤器，按照时间排序，或者按照时间和名称排序，开关过滤器等等。任何要求具备很高交互性数据操纵的场合都应该用JavaScript，而不是用一系列的服务器请求来完成。在每次数据更新后，再对其进行查找和处理需要耗费较多的时间，而Ajax可以加速这个过程。

#### 文本输入场景

在文本框等输入表单中给予输入提示，或者自动完成，可以有效的改善用户体验，尤其是那些自动完成的数据可能来自于服务器端的场合，Ajax是很好的选择。

# AJAX

##### 获取信息

实例化xmlhttprequest 对象

```js
    new XMLHttpRequest();
    new ActiveXObject("Microsoft.XMLHTTP");//ie8以下兼容性写法
    var xml=window.XMLHttpRequest?new  XMLHttpRequest():new ActiveXObject("Microsoft.XMLHTTP"); 
```

当创建了`XMLHttpRequest`对象后，要先设置`onreadystatechange`的回调函数。在回调函数中，通常我们只需通过`readyState === 4`判断请求是否完成，如果已完成，再根据`status === 200`判断是否是一个成功的响应。

```js
    xml.onreadystatechang=function(){
        alert(xml.readyState);   
        if(xml.readyState==4){
            if(xml.status==200){ 
                console.log(xml.response);
            }
        }

    }
    //等价方法
    xml.onload=function(){
         console.log(xml.response);
        }
```

XMLHttpRequest对象的`open()`方法有3个参数，第一个参数指定是`GET`还是`POST`，第二个参数指定URL地址，第三个参数指定是否使用异步，默认是true，所以不用写。

注意，千万不要把第三个参数指定为`false`，否则浏览器将停止响应，直到AJAX请求完成。如果这个请求耗时10秒，那么10秒内你会发现浏览器处于“假死”状态。

```js
    xml.open("get","/content/index.html",true);
```

最后调用`send()`方法才真正发送请求。GET请求不需要参数，POST请求需要把body部分以字符串或者FormData对象传进去。

```js
    xml.send();
```

##### 传递信息


网页分两种情况，其中`GET`在`open()`中添加信息，而`POST`需要在`send()中`添加信息并使用`setRequestHeader()`控制编码格式

```js
// get
xml.open("GET","php.php?name=zhangsan&age=12",true);
xml.send();
//post
xml.open("POST","php.php"); 
xml.setRequestHeader("Content-type","application/x-www-form-urlencoded"); 
xml.send("name=zhangsan&age=12");
```
php代码如下

```php
<?php
if($_GET["name"]=="zhangsan"){
echo "OK";
}else{
echo "error";
}
?>
```
 
返回值类型可以通过在`open()`后设置`xml.responseType()`来调整类型，默认为text.

```js
xml.responseType()="Text";
xml.responseXML();
xml.responseType()="document";
xml.responseType()="bolb";//二进制
xml.responseType()="json";
xml.responseType()="arraybuffer";
```
每次进行ajax操作都会有很多重复的操作，在这里，我们可以对函数进行封装，使操作更加方便。
```js
/* ajax封装
 * @param  {object} obj
 * //obj包含以下内容 *为必须 []为可选
 * obj.url链接地址          *
 * obj.methodget获取方式    []默认使用get方式
 * obj.data数据             []
 * obj.success回调函数      []
 * obj.datatype数据类型     []可接受text,xml,document,json
 * obj.asynch是否异步       []
 * obj.error状态
 */
function ajax(obj) {
        //判断输入格式是否正确
	if (typeof obj != "object") {
		console.error("请输入正确的参数类型");
		return false;
	}
	if (obj.url == undefined) {
		console.error("请输入正确的地址");
	}
	//对数值进行初始化
	var method = obj.method == undefined ? 'get' : obj.method;
	var asynch = obj.asynch == undefined ? true : obj.asynch;
	var dataType = obj.dataType == undefined ? 'text' : obj.dataType;
	var data = obj.data;
	var success = obj.success;
	var error = obj.error;
	var str = "";
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
	//兼容的实例化XMLHttpRequest对象
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

### 安全限制

上面代码的URL使用的是相对路径。如果把它改为`'http://www.sina.com.cn/'`，再运行，肯定报错。在Chrome的控制台里，还可以看到错误信息。

这是因为浏览器的同源策略导致的。默认情况下，JavaScript在发送AJAX请求时，URL的域名必须和当前页面完全一致。

完全一致的意思是，域名要相同（`www.example.com`和`example.com`不同），协议要相同（`http`和`https`不同），端口号要相同（默认是`:80`端口，它和`:8080`就不同）。有的浏览器口子松一点，允许端口不同，大多数浏览器都会严格遵守这个限制。

那是不是用JavaScript无法请求外域（就是其他网站）的URL了呢？方法还是有的，大概有这么几种：

一是通过Flash插件发送HTTP请求，这种方式可以绕过浏览器的安全限制，但必须安装Flash，并且跟Flash交互。不过Flash用起来麻烦，而且现在用得也越来越少了。

二是通过在同源域名下架设一个代理服务器来转发，JavaScript负责把请求发送到代理服务器：

```js
/proxy?url=http://www.sina.com.cn
```

代理服务器再把结果返回，这样就遵守了浏览器的同源策略。这种方式麻烦之处在于需要服务器端额外做开发。

第三种方式称为JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源：

```js
<script src="http://example.com/abc.js"></script>
```

JSONP通常以函数调用的形式返回，例如，返回JavaScript内容如下：

```js
foo('data');
```

这样一来，我们如果在页面中先准备好`foo()`函数，然后给页面动态加一个`<script>`节点，相当于动态读取外域的JavaScript资源，最后就等着接收回调了。

以163的股票查询URL为例，对于URL：[http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice](http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice)，你将得到如下返回：

```
refreshPrice({"0000001":{"code": "0000001", ... });
```

因此我们需要首先在页面中准备好回调函数：

```js
function refreshPrice(data) {
    var p = document.getElementById('test-jsonp');
    p.innerHTML = '当前价格：' +
        data['0000001'].name +': ' + 
        data['0000001'].price + '；' +
        data['1399001'].name + ': ' +
        data['1399001'].price;
}
```

最后用getPrice\(\)函数触发：

```js
function getPrice() {
    var
        js = document.createElement('script'),
        head = document.getElementsByTagName('head')[0];
    js.src = 'http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice';
    head.appendChild(js);
}
```

就完成了跨域加载数据。

### CORS

如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。

CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。

了解CORS前，我们先搞明白概念：

Origin表示本域，也就是浏览器当前页面的域。当JavaScript向外域（如sina.com）发起请求后，浏览器收到响应后，首先检查`Access-Control-Allow-Origin`是否包含本域，如果是，则此次跨域请求成功，如果不是，则请求失败，JavaScript将无法获取到响应的任何数据。

用一个图来表示就是：

![](/assets/l.png)

假设本域是`my.com`，外域是`sina.com`，只要响应头`Access-Control-Allow-Origin`为`http://my.com`，或者是`*`，本次请求就可以成功。

可见，跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的`Access-Control-Allow-Origin`，决定权始终在对方手中。

上面这种跨域请求，称之为“简单请求”。简单请求包括GET、HEAD和POST（POST的Content-Type类型 仅限`application/x-www-form-urlencoded`、`multipart/form-data`和`text/plain`），并且不能出现任何自定义头（例如，`X-Custom: 12345`），通常能满足90%的需求。

无论你是否需要用JavaScript通过CORS跨域请求资源，你都要了解CORS的原理。最新的浏览器全面支持HTML5。在引用外域资源时，除了JavaScript和CSS外，都要验证CORS。例如，当你引用了某个第三方CDN上的字体文件时：

```css
/* CSS */
@font-face {
  font-family: 'FontAwesome';
  src: url('http://cdn.com/fonts/fontawesome.ttf') format('truetype');
}
```

如果该CDN服务商未正确设置`Access-Control-Allow-Origin`，那么浏览器无法加载字体资源。

对于PUT、DELETE以及其他类型如`application/json`的POST请求，在发送AJAX请求之前，浏览器会先发送一个`OPTIONS`请求（称为preflighted请求）到这个URL上，询问目标服务器是否接受：

```php
OPTIONS /path/to/resource HTTP/1.1
Host: bar.com
Origin: http://my.com
Access-Control-Request-Method: POST
```

服务器必须响应并明确指出允许的Method：

```php
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://my.com
Access-Control-Allow-Methods: POST, GET, PUT, OPTIONS
Access-Control-Max-Age: 86400
```

浏览器确认服务器响应的`Access-Control-Allow-Methods`头确实包含将要发送的AJAX请求的Method，才会继续发送AJAX，否则，抛出一个错误。

由于以`POST`、`PUT`方式传送JSON格式的数据在REST中很常见，所以要跨域正确处理`POST`和`PUT`请求，服务器端必须正确响应`OPTIONS`请求。

