#less

less编程方式编写css，是css的预处理语言。基于`node.js`


##语言特性

####变量
```less
@color:#999;``background:@color; //注意，变量实际上是“常量”，因为它们只能定义一次。
``` 
####混合
混合是一种将一束属性从一个规则集合包含（“混合”）到另一个规则集合中的方式。（注意，你也可以使用`#ids`mixin）
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
指令例如`media`或`keyframe`可以以与选择器相同的方式嵌套。指令置​​于顶部，相对于相同规则集内的其他元素的相对顺序保持不变。这称为冒泡。

条件指令例如`@Media`，`@supports`并且`@document`还将选择器复制到其主体中：
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
@media screen {
  .screen-color {
    color: green;
  }
}
@media screen and (min-width: 768px) {
  .screen-color {
    color: red;
  }
}
@media tv {
  .screen-color {
    color: black;
  }
}
```
剩余的非条件指令，例如font-face或keyframes，也可以冒泡。他们本身不改变：
```less
#a {
  color: blue;
  @font-face {
    src: made-up-url;
  }
  padding: 2 2 2 2;
}
//生成以下代码
#a {
  color: blue;
}
@font-face {
  src: made-up-url;
}
#a {
  padding: 2 2 2 2;
}
```
####操作
算术运算`+`，`-`，`*`，`/`可在任何数目，颜色或变量操作。如果可能，数学运算会考虑单位，并在加法，减法或比较之前转换数字。结果最左边明确说明单元类型。如果转换不可能或无意义，则忽略单位。不可能转换的示例：px到cm或rad到％。
```less
// numbers are converted into the same units
@conversion-1: 5cm + 10mm; // result is 6cm
@conversion-2: 2 - 3cm - 5mm; // result is 1.5cm

// conversion is impossible
@incompatible-units: 2 + 5px - 3cm; // result is 4px

// example with variables
@base: 5%;
@filler: @base * 2; // result is 10%
@other: @base + @filler; // result is 15%
```
乘法和除法不转换数字。它在大多数情况下没有意义 - 长度乘以长度给出一个区域，css不支持指定区域。Less将对数字进行操作，并为结果分配明确声明的单元类型。
```less
@base: 2cm * 3mm; // result is 6cm
```
颜色分为红，绿，蓝和阿尔法尺寸。该操作分别应用于每个颜色维度。例如，如果用户添加了两种颜色，则结果的绿色维度等于输入颜色的绿色维度的总和。如果用户将颜色乘以数字，则每个颜色维度将相乘。

注意：alpha上的算术运算没有定义，因为颜色上的数学运算没有标准同意的意思。不要依赖当前的实现，因为它可能在以后的版本中改变。

对颜色的操作总是产生有效的颜色。如果结果的某个颜色维度大于`ff`或小于`00`，则维度将舍入为`ff`或`00`。如果alpha结束大于`1.0`或小于`0.0`，alpha将四舍五入为`1.0`或`0.0`。
```less
@color: #224488 / 2; //results in #112244
background-color: #112244 + #111; // result is #223355
```
####转义
转义允许你使用任何任意字符串作为属性或变量值。任何在里面`~"anything"`或被`~'anything'`使用，除了插值之外没有任何变化。
```less
.weird-element {
  content: ~"^//* some horrible but needed css hack";
}
//生成以下代码
.weird-element {
  content: ^//* some horrible but needed css hack;
}
```
####函数声明
```less
.raduis(@num){
	border-radius: @num;
}
```