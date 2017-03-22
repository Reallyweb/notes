## CSS3 选择器

在 CSS 中，选择器是一种模式，用于选择需要添加样式的元素。

"CSS" 列指示该属性是在哪个 CSS 版本中定义的。（CSS1、CSS2 还是 CSS3。）

| 选择器 | 例子 | 例子描述 | CSS |
| :--- | :--- | :--- | :--- |
| .class | .intro | 选择 class="intro" 的所有元素。 | 1 |
| #id | \#firstname | 选择 id="firstname" 的所有元素。 | 1 |
| *| 选择所有元素。 | - |
| element | p | 选择所有 &lt;`p`&gt; 元素。 | 1 |
| element,element | div,p | 选择所有 &lt;`div`&gt; 元素和所有 &lt;p&gt; 元素。 | 1 |
| elementelement | div p | 选择 &lt;`div`&gt; 元素内部的所有 &lt;p&gt; 元素。 | 1 |
| element&gt;element | div&gt;p | 选择父元素为 &lt;`div`&gt; 元素的所有 &lt;p&gt; 元素。 | 2 |
| element+element | div+p | 选择紧接在 &lt;`div`&gt; 元素之后的所有 &lt;p&gt; 元素。 | 2 |
| attribute | \[target\] | 选择带有 `target` 属性所有元素。 | 2 |
| attribute=value | \[target=\_blank\] | 选择 target="\_blank" 的所有元素。 | 2 |
| attribute~=value | \[title~=flower\] | 选择 title 属性包含单词 "flower" 的所有元素。 | 2 |
|attribute\|=value | \[lang\|=en\] | 选择 lang 属性值以 "en" 开头的所有元素。 | 2 |
| :link | a:link | 选择所有未被访问的链接。 | 1 |
| :visited | a:visited | 选择所有已被访问的链接。 | 1 |
| :active | a:active | 选择活动链接。 | 1 |
| :hover | a:hover | 选择鼠标指针位于其上的链接。 | 1 |
| :focus| input:focus | 选择获得焦点的 input 元素。 | 2 |
| :first-letter| p:first-letter | 选择每个 &lt;`p`&gt; 元素的首字母。 | 1 |
| :first-line| p:first-line | 选择每个 &lt;`p`&gt; 元素的首行。 | 1 |
| :first-child | p:first-child | 选择属于父元素的第一个子元素的每个 &lt;`p`&gt; 元素。 | 2 |
| :before | p:before | 在每个 &lt;`p`&gt; 元素的内容之前插入内容。 | 2 |
| :after| p:after | 在每个 &lt;`p`&gt; 元素的内容之后插入内容。 | 2 |
| :lang\(language\)| p:lang\(it\) | 选择带有以 "it" 开头的 lang 属性值的每个 &lt;`p`&gt; 元素。 | 2 |
| element1~element2| p~ul | 选择前面有 &lt;`p`&gt; 元素的每个 &lt;`ul`&gt; 元素。 | 3 |
| \[attribute^=value\] | a\[src^="https"\] | 选择其 src 属性值以 "https" 开头的每个 &lt;`a`&gt; 元素。 | 3 |
| \[attribute$=value\]| a\[src$=".pdf"\] | 选择其 src 属性以 ".pdf" 结尾的所有 &lt;`a`&gt; 元素。 | 3 |
| \[attribute\*=value\] | a\[src\*="abc"\] | 选择其 src 属性中包含 "abc" 子串的每个 &lt;`a`&gt; 元素。 | 3 |
| :first-of-type| p:first-of-type | 选择属于其父元素的首个 &lt;p&gt; 元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :last-of-type | p:last-of-type | 选择属于其父元素的最后 &lt;p&gt; 元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :only-of-type | p:only-of-type | 选择属于其父元素唯一的 &lt;p&gt; 元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :only-child | p:only-child | 选择属于其父元素的唯一子元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :nth-child\(n\)| p:nth-child\(2\) | 选择属于其父元素的第二个子元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :nth-last-child\(n\) | p:nth-last-child\(2\) | 同上，从最后一个子元素开始计数。 | 3 |
| :nth-of-type\(n\) | p:nth-of-type\(2\) | 选择属于其父元素第二个 &lt;`p`&gt; 元素的每个 &lt;`p`&gt; 元素。 | 3 |
| :nth-last-of-type\(n\)| p:nth-last-of-type\(2\) | 同上，但是从最后一个子元素开始计数。 | 3 |
| :last-child | p:last-child | 选择属于其父元素最后一个子元素每个 &lt;`p`&gt; 元素。 | 3 |
| :root| :root | 选择文档的根元素。 | 3 |
| :empty | p:empty | 选择没有子元素的每个 &lt;`p`&gt; 元素（包括文本节点）。 | 3 |
| :target | \#news:target | 选择当前活动的 \#news 元素。 | 3 |
| :enabled | input:enabled | 选择每个启用的 &lt;`input`&gt; 元素。 | 3 |
| :disabled | input:disabled | 选择每个禁用的 &lt;`input`&gt; 元素 | 3 |
| :checked| input:checked | 选择每个被选中的 &lt;`input`&gt; 元素。 | 3 |
| :not\(selector\)| :not\(p\) | 选择非 &lt;`p`&gt; 元素的每个元素。 | 3 |
| ::selection| ::selection | 选择被用户选取的元素部分。 | 3 |

#### CSS3渐变

CSS3 渐变（gradients）可以让你在两个或多个指定的颜色之间显示平稳的过渡。
以前，你必须使用图像来实现这些效果。但是，通过使用 CSS3 渐变（gradients），你可以减少下载的事件和宽带的使用。此外，渐变效果的元素在放大时看起来效果更好，因为渐变（gradient）是由浏览器生成的。
CSS3 定义了两种类型的渐变（gradients）：
 * 线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
 * 径向渐变（Radial Gradients）- 由它们的中心定义
 
#####CSS3 线性渐变
为了创建一个线性渐变，必须至少定义两种颜色结点。颜色结点即想要呈现平稳过渡的颜色。同时，也可以设置一个起点和一个方向（或一个角度）。
语法
```css
background: linear-gradient(direction, color-stop1, color-stop2, ...);
```

######线性渐变 - 从上到下（默认情况下）
下面的实例演示了从顶部开始的线性渐变。起点是红色，慢慢过渡到蓝色：
实例
从上到下的线性渐变：
```css
#grad {
  background: -webkit-linear-gradient(red, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(red, blue); /* 标准的语法 */
}
```

######线性渐变 - 从左到右
下面的实例演示了从左边开始的线性渐变。起点是红色，慢慢过渡到蓝色：
实例
从左到右的线性渐变：
```css
#grad {
  background: -webkit-linear-gradient(left, red , blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(right, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(right, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(to right, red , blue); /* 标准的语法 */
}
```
######线性渐变 - 对角
你可以通过指定水平和垂直的起始位置来制作一个对角渐变。
下面的实例演示了从左上角开始（到右下角）的线性渐变。起点是红色，慢慢过渡到蓝色：

从左上角到右下角的线性渐变：
```css
#grad {
  background: -webkit-linear-gradient(left top, red , blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(bottom right, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(bottom right, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(to bottom right, red , blue); /* 标准的语法 */
}
```

#####使用角度
如果你想要在渐变的方向上做更多的控制，你可以定义一个角度，而不用预定义方向（to bottom、to top、to right、to left、to bottom right，等等）。
语法
background: linear-gradient(angle, color-stop1, color-stop2);
角度是指水平线和渐变线之间的角度，逆时针方向计算。换句话说，0deg 将创建一个从下到上的渐变，90deg 将创建一个从左到右的渐变。

但是，请注意很多浏览器(Chrome,Safari,fiefox等)的使用了旧的标准，即 0deg 将创建一个从左到右的渐变，90deg 将创建一个从下到上的渐变。换算公式 90 - x = y 其中 x 为标准角度，y为非标准角度。
下面的实例演示了如何在线性渐变上使用角度：

带有指定的角度的线性渐变：
```css
#grad {
  background: -webkit-linear-gradient(180deg, red, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(180deg, red, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(180deg, red, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(180deg, red, blue); /* 标准的语法 */
}
```
#####使用多个颜色结点
下面的实例演示了如何设置多个颜色结点：
实例
带有多个颜色结点的从上到下的线性渐变：
```
#grad {
  background: -webkit-linear-gradient(red, green, blue); /* Safari 5.1 - 6.0 */
  background: -o-linear-gradient(red, green, blue); /* Opera 11.1 - 12.0 */
  background: -moz-linear-gradient(red, green, blue); /* Firefox 3.6 - 15 */
  background: linear-gradient(red, green, blue); /* 标准的语法 */
}

```
下面的实例演示了如何创建一个带有彩虹颜色和文本的线性渐变：
实例
```css
#grad {
  /* Safari 5.1 - 6.0 */
  background: -webkit-linear-gradient(left,red,orange,yellow,green,blue,indigo,violet);
  /* Opera 11.1 - 12.0 */
  background: -o-linear-gradient(left,red,orange,yellow,green,blue,indigo,violet);
  /* Firefox 3.6 - 15 */
  background: -moz-linear-gradient(left,red,orange,yellow,green,blue,indigo,violet);
  /* 标准的语法 */
  background: linear-gradient(to right, red,orange,yellow,green,blue,indigo,violet); 
}
```
#####使用透明度（Transparency）
CSS3 渐变也支持透明度（transparency），可用于创建减弱变淡的效果。
为了添加透明度，我们使用 rgba() 函数来定义颜色结点。rgba() 函数中的最后一个参数可以是从 0 到 1 的值，它定义了颜色的透明度：0 表示完全透明，1 表示完全不透明。
下面的实例演示了从左边开始的线性渐变。起点是完全透明，慢慢过渡到完全不透明的红色：
实例
从左到右的线性渐变，带有透明度：
```css
#grad {
  background: -webkit-linear-gradient(left,rgba(255,0,0,0),rgba(255,0,0,1)); /* Safari 5.1 - 6 */
  background: -o-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Opera 11.1 - 12*/
  background: -moz-linear-gradient(right,rgba(255,0,0,0),rgba(255,0,0,1)); /* Firefox 3.6 - 15*/
  background: linear-gradient(to right, rgba(255,0,0,0), rgba(255,0,0,1)); /* 标准的语法 */
}

```
#####重复的线性渐变
repeating-linear-gradient() 函数用于重复线性渐变：

一个重复的线性渐变：
```css
#grad {
  /* Safari 5.1 - 6.0 */
  background: -webkit-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* Opera 11.1 - 12.0 */
  background: -o-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* Firefox 3.6 - 15 */
  background: -moz-repeating-linear-gradient(red, yellow 10%, green 20%);
  /* 标准的语法 */
  background: repeating-linear-gradient(red, yellow 10%, green 20%);
}

```

####CSS3 径向渐变
径向渐变由它的中心定义。
为了创建一个径向渐变，你也必须至少定义两种颜色结点。颜色结点即你想要呈现平稳过渡的颜色。同时，你也可以指定渐变的中心、形状（原型或椭圆形）、大小。默认情况下，渐变的中心是 `center`（表示在中心点），渐变的形状是 `ellipse`（表示椭圆形），渐变的大小是 `farthest-corner`（表示到最远的角落）。
径向渐变的实例：
Radial gradient
语法
```css
background: radial-gradient(center, shape size, start-color, ..., last-color);
```
#####径向渐变 - 颜色结点均匀分布（默认情况下）

颜色结点均匀分布的径向渐变：
```css
#grad {
  background: -webkit-radial-gradient(red, green, blue); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(red, green, blue); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(red, green, blue); /* Firefox 3.6 - 15 */
  background: radial-gradient(red, green, blue); /* 标准的语法 */
}
```

#####径向渐变 - 颜色结点不均匀分布

颜色结点不均匀分布的径向渐变：
```css
#grad {
  background: -webkit-radial-gradient(red 5%, green 15%, blue 60%); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(red 5%, green 15%, blue 60%); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(red 5%, green 15%, blue 60%); /* Firefox 3.6 - 15 */
  background: radial-gradient(red 5%, green 15%, blue 60%); /* 标准的语法 */
}
```
#####设置形状
shape 参数定义了形状。它可以是值 circle 或 ellipse。其中，circle 表示圆形，ellipse 表示椭圆形。默认值是 ellipse。

形状为圆形的径向渐变：
```css
#grad {
  background: -webkit-radial-gradient(circle, red, yellow, green); /* Safari 5.1 - 6.0 */
  background: -o-radial-gradient(circle, red, yellow, green); /* Opera 11.6 - 12.0 */
  background: -moz-radial-gradient(circle, red, yellow, green); /* Firefox 3.6 - 15 */
  background: radial-gradient(circle, red, yellow, green); /* 标准的语法 */
}
```
#####不同尺寸大小关键字的使用
size 参数定义了渐变的大小。它可以是以下四个值：
closest-side
farthest-side
closest-corner
farthest-corner

带有不同尺寸大小关键字的径向渐变：
```css
#grad1 {
  /* Safari 5.1 - 6.0 */
  background: -webkit-radial-gradient(60% 55%, closest-side,blue,green,yellow,black); 
  /* Opera 11.6 - 12.0 */
  background: -o-radial-gradient(60% 55%, closest-side,blue,green,yellow,black);
  /* Firefox 3.6 - 15 */
  background: -moz-radial-gradient(60% 55%, closest-side,blue,green,yellow,black);
  /* 标准的语法 */
  background: radial-gradient(60% 55%, closest-side,blue,green,yellow,black);
}
 
#grad2 {
  /* Safari 5.1 - 6.0 */
  background: -webkit-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black);
  /* Opera 11.6 - 12.0 */ 
  background: -o-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black);
  /* Firefox 3.6 - 15 */
  background: -moz-radial-gradient(60% 55%, farthest-side,blue,green,yellow,black);
  /* 标准的语法 */
  background: radial-gradient(60% 55%, farthest-side,blue,green,yellow,black);
}
```

#####重复的径向渐变
repeating-radial-gradient() 函数用于重复径向渐变：
重复的径向渐变：
```css
#grad {
  /* Safari 5.1 - 6.0 */
  background: -webkit-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* Opera 11.6 - 12.0 */
  background: -o-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* Firefox 3.6 - 15 */
  background: -moz-repeating-radial-gradient(red, yellow 10%, green 15%);
  /* 标准的语法 */
  background: repeating-radial-gradient(red, yellow 10%, green 15%);
}
```
#### CSS3过渡
通过 CSS3，我们可以在不使用 Flash 动画或 JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。
######浏览器支持				
Internet Explorer 10、Firefox、Chrome 以及 Opera 支持 transition 属性。
Safari 需要前缀 -webkit-。
注释：Internet Explorer 9 以及更早的版本，不支持 transition 属性。
注释：Chrome 25 以及更早的版本，需要前缀 -webkit-。
#####它如何工作？
CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。
要实现这一点，必须规定两项内容：
* 规定您希望把效果添加到哪个 CSS 属性上
* 规定效果的时长


应用于宽度属性的过渡效果，时长为 2 秒：
```css
div
{
transition: width 2s;
-moz-transition: width 2s;	/* Firefox 4 */
-webkit-transition: width 2s;	/* Safari 和 Chrome */
-o-transition: width 2s;	/* Opera */
}
```
注释：如果时长未规定，则不会有过渡效果，因为默认值是 0。
效果开始于指定的 CSS 属性改变值时。CSS 属性改变的典型时间是鼠标指针位于元素上时：

当鼠标指针悬浮于 <div> 元素上时：
```css
div:hover
{
width:300px;
}
```
注释：当指针移出元素时，它会逐渐变回原来的样式。
多项改变
如需向多个样式添加过渡效果，请添加多个属性，由逗号隔开：

向宽度、高度和转换添加过渡效果：
```css
div
{
transition: width 2s, height 2s, transform 2s;
-moz-transition: width 2s, height 2s, -moz-transform 2s;
-webkit-transition: width 2s, height 2s, -webkit-transform 2s;
-o-transition: width 2s, height 2s,-o-transform 2s;
}
```

过渡属性
下面的表格列出了所有的转换属性：

| 属性 | 描述 | CSS |
| :--- | :--- | :--- |
| transition | 简写属性，用于在一个属性中设置四个过渡属性。 | 3 |
| transition-property | 规定应用过渡的 CSS 属性的名称。 | 3 |
| transition-duration | 定义过渡效果花费的时间。默认是 0。 | 3 |
| transition-timing-function | 规定过渡效果的时间曲线。默认是 "ease"。 | 3 |
| transition-delay | 规定过渡效果何时开始。默认是 0。 | 3 |

下面的两个例子设置所有过渡属性：

在一个例子中使用所有过渡属性：
```css
div
{
transition-property: width;
transition-duration: 1s;
transition-timing-function: linear;
transition-delay: 2s;
/* Firefox 4 */
-moz-transition-property:width;
-moz-transition-duration:1s;
-moz-transition-timing-function:linear;
-moz-transition-delay:2s;
/* Safari 和 Chrome */
-webkit-transition-property:width;
-webkit-transition-duration:1s;
-webkit-transition-timing-function:linear;
-webkit-transition-delay:2s;
/* Opera */
-o-transition-property:width;
-o-transition-duration:1s;
-o-transition-timing-function:linear;
-o-transition-delay:2s;
}
```

与上面的例子相同的过渡效果，但是使用了简写的 transition 属性：
```css
div
{
transition: width 1s linear 2s;
/* Firefox 4 */
-moz-transition:width 1s linear 2s;
/* Safari and Chrome */
-webkit-transition:width 1s linear 2s;
/* Opera */
-o-transition:width 1s linear 2s;
}
```

#### CSS3 2D 转换

CSS3 转换
通过 CSS3 转换，我们能够对元素进行移动、缩放、转动、拉长或拉伸。
#####它如何工作？
转换是使元素改变形状、尺寸和位置的一种效果。
您可以使用 2D 或 3D 转换来转换您的元素。
######浏览器支持				
Internet Explorer 10、Firefox 以及 Opera 支持 transform 属性。
Chrome 和 Safari 需要前缀 -webkit-。
注释：Internet Explorer 9 需要前缀 -ms-。
#####2D 转换
在本章中，您将学到如下 2D 转换方法：
translate()
rotate()
scale()
skew()
matrix()
您将在下一章学习 3D 转换。
```css
div
{
transform: rotate(30deg);
-ms-transform: rotate(30deg);		/* IE 9 */
-webkit-transform: rotate(30deg);	/* Safari and Chrome */
-o-transform: rotate(30deg);		/* Opera */
-moz-transform: rotate(30deg);		/* Firefox */
}
```

#####translate() 方法
通过 translate() 方法，元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标） 位置参数：
```css
div
{
transform: translate(50px,100px);
-ms-transform: translate(50px,100px);		/* IE 9 */
-webkit-transform: translate(50px,100px);	/* Safari and Chrome */
-o-transform: translate(50px,100px);		/* Opera */
-moz-transform: translate(50px,100px);		/* Firefox */
}
```

#####rotate() 方法
通过 rotate() 方法，元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转。
```css
div
{
transform: rotate(30deg);
-ms-transform: rotate(30deg);		/* IE 9 */
-webkit-transform: rotate(30deg);	/* Safari and Chrome */
-o-transform: rotate(30deg);		/* Opera */
-moz-transform: rotate(30deg);		/* Firefox */
}
```

#####scale() 方法
通过 scale() 方法，元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数：
```css
div
{
transform: scale(2,4);
-ms-transform: scale(2,4);	/* IE 9 */
-webkit-transform: scale(2,4);	/* Safari 和 Chrome */
-o-transform: scale(2,4);	/* Opera */
-moz-transform: scale(2,4);	/* Firefox */
}
```

#####skew() 方法
通过 skew() 方法，元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）参数：
```css
div
{
transform: skew(30deg,20deg);
-ms-transform: skew(30deg,20deg);	/* IE 9 */
-webkit-transform: skew(30deg,20deg);	/* Safari and Chrome */
-o-transform: skew(30deg,20deg);	/* Opera */
-moz-transform: skew(30deg,20deg);	/* Firefox */
}
```

#####matrix() 方法
matrix() 方法把所有 2D 转换方法组合在一起。
matrix() 方法需要六个参数，包含数学函数，允许您：旋转、缩放、移动以及倾斜元素。
使用 matrix 方法将 div 元素旋转 30 度：
```css
div
{
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
-ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0);		/* IE 9 */
-moz-transform:matrix(0.866,0.5,-0.5,0.866,0,0);	/* Firefox */
-webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0);	/* Safari and Chrome */
-o-transform:matrix(0.866,0.5,-0.5,0.866,0,0);		/* Opera */
}
```

下面的表格列出了所有的转换属性：

| 属性 | 描述 | CSS |
| :--- | :--- | :--- |
| transform | 向元素应用 2D 或 3D 转换。 | 3 |
| transform-origin | 允许你改变被转换元素的位置。 | 3 |

#####2D Transform 方法

| 函数 | 描述 |
| :--- | :--- | 
| matrix(n,n,n,n,n,n) | 定义 2D 转换，使用六个值的矩阵。| 
| translate(x,y)| 定义 2D 转换，沿着 X 和 Y 轴移动元素。| 
| translateX(n)|定义 2D 转换，沿着 X 轴移动元素。| 
| translateY(n)| 定义 2D 转换，沿着 Y 轴移动元素。| 
| scale(x,y)| 定义 2D 缩放转换，改变元素的宽度和高度。| 
| scaleX(n)| 定义 2D 缩放转换，改变元素的宽度。| 
| scaleY(n)| 定义 2D 缩放转换，改变元素的高度。| 
| rotate(angle)| 定义 2D 旋转，在参数中规定角度。| 
| skew(x-angle,y-angle)| 定义 2D 倾斜转换，沿着 X 和 Y 轴。| 
| skewX(angle)| 定义 2D 倾斜转换，沿着 X 轴。| 
| skewY(angle)| 定义 2D 倾斜转换，沿着 Y 轴。| 

####CSS3 3D 转换

3D 转换
CSS3 允许您使用 3D 转换来对元素进行格式化。
在本章中，您将学到其中的一些 3D 转换方法：
rotateX()
rotateY()
点击下面的元素，来查看 2D 转换与 3D 转换之间的不同之处：
2D 旋转3D 旋转
它如何工作？
转换是使元素改变形状、尺寸和位置的一种效果。
您可以使用 2D 或 3D 转换来转换您的元素。
浏览器支持
属性	浏览器支持
transform					
Internet Explorer 10 和 Firefox 支持 3D 转换。
Chrome 和 Safari 需要前缀 -webkit-。
Opera 仍然不支持 3D 转换（它只支持 2D 转换）。
rotateX() 方法
通过 rotateX() 方法，元素围绕其 X 轴以给定的度数进行旋转。
实例
div
{
transform: rotateX(120deg);
-webkit-transform: rotateX(120deg);	/* Safari 和 Chrome */
-moz-transform: rotateX(120deg);	/* Firefox */
}
亲自试一试
rotateY() 旋转
通过 rotateY() 方法，元素围绕其 Y 轴以给定的度数进行旋转。
实例
div
{
transform: rotateY(130deg);
-webkit-transform: rotateY(130deg);	/* Safari 和 Chrome */
-moz-transform: rotateY(130deg);	/* Firefox */
}
亲自试一试
转换属性
下面的表格列出了所有的转换属性：
属性	描述	CSS
transform	向元素应用 2D 或 3D 转换。	3
transform-origin	允许你改变被转换元素的位置。	3
transform-style	规定被嵌套元素如何在 3D 空间中显示。	3
perspective	规定 3D 元素的透视效果。	3
perspective-origin	规定 3D 元素的底部位置。	3
backface-visibility	定义元素在不面对屏幕时是否可见。	3
2D Transform 方法
函数	描述
matrix3d(n,n,n,n,n,n,
n,n,n,n,n,n,n,n,n,n)	定义 3D 转换，使用 16 个值的 4x4 矩阵。
translate3d(x,y,z)	定义 3D 转化。
translateX(x)	定义 3D 转化，仅使用用于 X 轴的值。
translateY(y)	定义 3D 转化，仅使用用于 Y 轴的值。
translateZ(z)	定义 3D 转化，仅使用用于 Z 轴的值。
scale3d(x,y,z)	定义 3D 缩放转换。
scaleX(x)	定义 3D 缩放转换，通过给定一个 X 轴的值。
scaleY(y)	定义 3D 缩放转换，通过给定一个 Y 轴的值。
scaleZ(z)	定义 3D 缩放转换，通过给定一个 Z 轴的值。
rotate3d(x,y,z,angle)	定义 3D 旋转。
rotateX(angle)	定义沿 X 轴的 3D 旋转。
rotateY(angle)	定义沿 Y 轴的 3D 旋转。
rotateZ(angle)	定义沿 Z 轴的 3D 旋转。
perspective(n)	定义 3D 转换元素的透视视图。