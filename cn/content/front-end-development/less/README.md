#less

less编程方式编写css，是css的预处理语言。基于`node.js`


##语言特性

作为CSS的扩展，Less不仅向后兼容CSS，它添加的额外功还能使用现有的CSS语法。这使得学习更轻松。

####变量
```less
@color:#999;``background:@color; //注意，变量实际上是“常量”，因为它们只能定义一次。
``` 
####混合
混合是一种将一连串属性从一个规则集合包含到另一个规则集合中的方式。（注意:你也可以使用`#ids`mixin）
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
Less能够使用嵌套，而不是级联，或者与级联组合使用。
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
指令比如`media`或`keyframe`可以以与选择器相同的方式嵌套。指令置​​于顶部，相对于相同规则集合内的其他元素的相对顺序保持不变。这也称为冒泡。

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
剩余的非条件指令，例如font-face或keyframes，也可以冒泡。他们结构不会改变：
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
算术运算`+`，`-`，`*`，`/`可在任何数目，颜色或变量操作。如果条件允许，数学运算会考虑单位，并在加法，减法或比较之前转换数字。结果最左边明确说明单元类型。如果转换失败或无意义，则忽略单位。不可能转换的示例：px到cm或rad到％。
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
####功能

Less提供了各种功能，可以转换颜色，操作字符串和做数学。它们全部记录在函数参考中。

使用它们是相当简单的。以下示例使用百分比将0.5转换至50％，将基色的饱和度增加5％，然后将背景颜色设置为减轻25％并扭转8度的背景颜色：

```less
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```
####命名空间和访问器

（不要混淆`CSS@namespace`与`命名空间选择器`）。

有时，你可能想要组合你的mixin，组织逻辑，或只是想提供一些封装。你可以在Less中很直观地做到这一点，比如你想在下面捆绑一些mixins和变量`#bundle`，以便于开发和复用.：
```less
#bundle {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab { ... }
  .citation { ... }
}
```
如果我们想`.button`在我们的类中混合`#header a`，我们可以做：
```less
#header a {
  color: orange;
  #bundle > .button;
}
```
注意，在命名空间中声明的变量将仅限于该命名空间，并且将不会通过与用于引用mixin（`#Namespace > .mixin-name`）的相同语法在范围外可用。因此，例如，您不能执行以下操作：（`#Namespace > @this-will-not-work`）。
####范围

Less中的范围与编程语言非常相似。变量和mixins首先在本地查找，如果没有找到，编译器将查找父范围，等等。
```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```
变量和混合在使用之前不必声明，所以以下Less代码与前面的示例相同：
```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```
####函数声明

```less
.raduis(@num){
	border-radius: @num;
}
```
####循环

```less
.loop(@counter) when (@counter > 0) {
  .loop((@counter - 1));    // next iteration
  width: (10px * @counter); // code for each iteration
}
div {
  .loop(5); // launch the loop
}
//生成以下代码
div {
  width: 10px;
  width: 20px;
  width: 30px;
  width: 40px;
  width: 50px;
}
```
使用递归循环生成CSS网格类的一个通用示例：
```less
.generate-columns(4);
.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
//生成以下代码

.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
```