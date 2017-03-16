#less

less编程方式编写css，css预处理语言。基于node.js


####变量
```less
@color:#999;``background:@color; //注意，变量实际上是“常量”，因为它们只能定义一次。
``` 
####混合
混合是一种将一束属性从一个规则集合包含（“混合”）到另一个规则集合中的方式。
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
####嵌套规则
Less能够使用嵌套，而不是级联，或与级联组合使用。
```less
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
//生成以下代码
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```
####嵌套指令和冒泡
指令例如media或keyframe可以以与选择器相同的方式嵌套。指令置​​于顶部，相对于相同规则集内的其他元素的相对顺序保持不变。这称为冒泡。

条件指令例如@Media，@supports并且@document还将选择器复制到其主体中：
```less
.screen-color {
  @media screen {
    color: green;
    @media (min-width: 768px) {
      color: red;
    }
  }
  @media tv {
    color: black;
  }
}
//生成以下代码
```
####函数声明
```less
.raduis(@num){
	border-radius: @num;
}
```