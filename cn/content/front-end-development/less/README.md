#less

less编程方式编写css，css预处理语言。基于node.js


####变量
```less
@color:#999;``background:@color; //注意，变量实际上是“常量”，因为它们只能定义一次。
``` 
####混合
```less
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
#menu a {
  color: #111;
  .bordered;
}

.post a {
  color: red;
  .bordered;
}
```
函数声明
```less
.raduis(@num){
	border-radius: @num;
}
```