#HTML5

css3发展缓慢，过程化编程
内核前缀：表示先进性，表示不通用
####响应式布局
能对不同终端进行响应，

less编程方式编写css，css预处理语言。基于node.js
可以给边框设置圆角，
变量
eg:`@color:#999;``background:@color; //注意，变量实际上是“常量”，因为它们只能定义一次。` 
混合
eg:
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
eg:
```less
.raduis(@num){
	border-radius: @num;
}
```