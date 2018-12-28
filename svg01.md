# svg概述和语法



---
>摘自阮一峰http://www.ruanyifeng.com/blog/2018/08/svg.html

**一、概述**

 - SVG 是一种基于 XML 语法的图像格式，全称是可缩放矢量图（Scalable Vector Graphics）。
其他图像格式都是基于像素处理的，SVG 则是属于对图像的形状描述，所以它本质上是文本文件，体积较小，且不管放大多少倍都不会失真.
 - SVG 文件可以直接插入网页，成为 DOM 的一部分，然后用 JavaScript 和 CSS 进行操作。

```
<!DOCTYPE html>
<html>
<head></head>
<body>
<svg
  id="mysvg"
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 800 600"
  preserveAspectRatio="xMidYMid meet"
>
  <circle id="mycircle" cx="400" cy="300" r="50" />
<svg>
</body>
</html>
```
SVG 代码也可以写在一个独立文件中，然后用`<img>`、`<object>`、`<embed>`、<iframe>等标签插入网页。

```
<img src="circle.svg">
<object id="object" data="circle.svg" type="image/svg+xml"></object>
<embed id="embed" src="icon.svg" type="image/svg+xml">
<iframe id="iframe" src="icon.svg"></iframe>
```
CSS 也可以使用 SVG 文件。

```
.logo {
  background: url(icon.svg);
}
```
SVG 文件还可以转为 BASE64 编码，然后作为 Data URI 写入网页。

```
<img src="data:image/svg+xml;base64,[data]">
```
**二、语法**

 - SVG 代码都放在顶层标签<svg>之中
 - `<svg>`的width属性和height属性，指定了 SVG 图像在 HTML 元素中所占据的宽度和高度。除了相对单位，也可以采用绝对单位（单位：像素）。
 如果不指定这两个属性，SVG 图像默认大小是300像素（宽） x 150像素（高）。
如果只想展示 SVG 图像的一部分，就要指定`viewBox`属性。

    **viewBox**
    ```
        <svg width="100" height="100" viewBox="50 50 50 50">
          <circle id="mycircle" cx="50" cy="50" r="50" />
        </svg>
    ```
    - viewbox的属性值有四个数字，左上角的横纵坐标，适口的宽度和高度。
    - 视口必须适配所在的空间。
    
 - `<circle>`标签代表圆形。
    ```
    <svg width="300" height="180">
      <circle cx="30"  cy="50" r="25" />
      <circle cx="90"  cy="50" r="25" class="red" />
      <circle cx="150" cy="50" r="25" class="fancy" />
    </svg>
    ```
    - <circle>标签的cx、cy、r属性分别为横坐标、纵坐标和半径，单位为像素。坐标都是**相对于`<svg>`画布的左上角原点。** 
    - class属性用来指定对应的 CSS 类
SVG 的 CSS 属性与网页元素有所不同。
    ```
    fill：填充色
    stroke：描边色
    stroke-width：边框宽度
    ```
    

 - `<line>`标签用来绘制直线。

    ```
    <svg width="300" height="180">
      <line x1="0" y1="0" x2="200" y2="0" style="stroke:rgb(0,0,0);stroke-width:5" />
    </svg>
    ```
    

 - `<polyline>`标签用于绘制一根折线。
    ```
    <svg width="300" height="180">
      <polyline points="3,3 30,28 3,53" fill="none" stroke="black" />
    </svg>
    ```
    - `<polyline>`的points属性指定了每个端点的坐标，横坐标与纵坐标之间与逗号分隔，点与点之间用空格分隔。

 - `<rect>`标签用于绘制矩形
 ```
    <svg width="300" height="180">
      <rect x="0" y="0" height="100" width="200" style="stroke: #70d5dd; fill: #dd524b" />
    </svg>
```

 - `<ellipse>`标签用于绘制椭圆。
    ```
    <svg width="300" height="180">
      <ellipse cx="60" cy="60" ry="40" rx="20" stroke="black" stroke-width="5" fill="silver"/>
    </svg>
    ```

 - `<polygon>`标签用于绘制多边形。
 
    ```
    <svg width="300" height="180">
      <polygon fill="green" stroke="orange" stroke-width="1" points="0,0 100,0 100,100 0,100 0,0"/>
    </svg>
    ```

 - `<path>`标签用于制路径。
 
    ```
    <svg width="300" height="180">
    <path d="
      M 18,3
      L 46,3
      L 46,40
      L 61,40
      L 32,68
      L 3,40
      L 18,40
      Z
    "></path></svg>
    ```
 `<path>`的d属性表示绘制顺序，它的值是一个长字符串，每个字母表示一个绘制动作，后面跟着坐标。

    >M：移动到（moveto）
    >L：画直线到（lineto）
    >Z：闭合路径

 - `<text>`标签用于绘制文本。
    ```
    <svg width="300" height="180">
      <text x="50" y="25">Hello World</text>
    </svg>
    ```
    - `<text>`的x属性和y属性，表示文本区块基线（baseline）起点的横坐标和纵坐标。文字的样式可以用class或style属性指定。

 - `<use>`标签用于复制一个形状。
    ```
    <svg viewBox="0 0 30 10" xmlns="http://www.w3.org/2000/svg">
      <circle id="myCircle" cx="5" cy="5" r="4"/>
    
      <use href="#myCircle" x="10" y="0" fill="blue" />
      <use href="#myCircle" x="20" y="0" fill="white" stroke="blue" />
    </svg>
    ```
    - <use>的href属性指定所要复制的节点，x属性和y属性是<use>左上角的坐标。另外，还可以指定width和height坐标。
    

 - `<g>`标签用于将多个形状组成一个组（group），方便复用。
    ```
    <svg width="300" height="100">
      <g id="myCircle">
        <text x="25" y="20">圆形</text>
        <circle cx="50" cy="50" r="20"/>
      </g>
    
      <use href="#myCircle" x="100" y="0" fill="blue" />
      <use href="#myCircle" x="200" y="0" fill="white" stroke="blue" />
    </svg>
    ```
    

 - `<defs>`标签用于自定义形状，它内部的代码不会显示，仅供引用。
    ```
    <svg width="300" height="100">
      <defs>
        <g id="myCircle">
          <text x="25" y="20">圆形</text>
          <circle cx="50" cy="50" r="20"/>
        </g>
      </defs>
    
      <use href="#myCircle" x="0" y="0" />
      <use href="#myCircle" x="100" y="0" fill="blue" />
      <use href="#myCircle" x="200" y="0" fill="white" stroke="blue" />
    </svg>
    ```

 - `<pattern>`标签用于自定义一个形状，该形状可以被引用来平铺一个区域。
    ```
    <svg width="500" height="500">
      <defs>
        <pattern id="dots" x="0" y="0" width="100" height="100" patternUnits="userSpaceOnUse">
          <circle fill="#bee9e8" cx="50" cy="50" r="35" />
        </pattern>
      </defs>
      <rect x="0" y="0" width="100%" height="100%" fill="url(#dots)" />
    </svg>
    ```
    - `<pattern>`标签将一个圆形定义为dots模式。`patternUnits="userSpaceOnUse"`表示`<pattern>`的宽度和长度是实际的像素值。然后，指定这个模式去填充下面的矩形。

 - `<animate>`标签用于产生动画效果。
    ```
    <svg width="500px" height="500px">
      <rect x="0" y="0" width="100" height="100" fill="#feac5e">
        <animate attributeName="x" from="0" to="500" dur="2s" repeatCount="indefinite" />
      </rect>
    </svg>
    ```
    `<animate>`的属性含义如下。

    >**attributeName**：发生动画效果的属性名。
    **from**：单次动画的初始值。
    **to**：单次动画的结束值。
    **dur**：单次动画的持续时间。
    **repeatCount**：动画的循环模式。
    可以在多个属性上面定义动画。

    ```
    <animate attributeName="x" from="0" to="500" dur="2s" repeatCount="indefinite" />
    <animate attributeName="width" to="500" dur="2s" repeatCount="indefinite" />
    ```
