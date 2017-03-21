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

实例
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
实例
规定当鼠标指针悬浮于 <div> 元素上时：
```css
div:hover
{
width:300px;
}
```

注释：当指针移出元素时，它会逐渐变回原来的样式。
多项改变
如需向多个样式添加过渡效果，请添加多个属性，由逗号隔开：
实例
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

translate() 方法
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

rotate() 方法
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

scale() 方法
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

skew() 方法
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

matrix() 方法
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
属性	描述	CSS
transform	向元素应用 2D 或 3D 转换。	3
transform-origin	允许你改变被转换元素的位置。	3
2D Transform 方法
函数	描述
matrix(n,n,n,n,n,n)	定义 2D 转换，使用六个值的矩阵。
translate(x,y)	定义 2D 转换，沿着 X 和 Y 轴移动元素。
translateX(n)	定义 2D 转换，沿着 X 轴移动元素。
translateY(n)	定义 2D 转换，沿着 Y 轴移动元素。
scale(x,y)	定义 2D 缩放转换，改变元素的宽度和高度。
scaleX(n)	定义 2D 缩放转换，改变元素的宽度。
scaleY(n)	定义 2D 缩放转换，改变元素的高度。
rotate(angle)	定义 2D 旋转，在参数中规定角度。
skew(x-angle,y-angle)	定义 2D 倾斜转换，沿着 X 和 Y 轴。
skewX(angle)	定义 2D 倾斜转换，沿着 X 轴。
skewY(angle)	定义 2D 倾斜转换，沿着 Y 轴。


