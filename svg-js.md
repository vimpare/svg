# svg js操作

标签（空格分隔）： 未分类

---

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        circle {
            stroke-width: 5;
            stroke: #f00;
            fill: #ff0;
        }

        circle:hover {
            stroke: #090;
            fill: #fff;
        }
    </style>
</head>

<body>
    <svg id="mysvg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 600" preserveAspectRatio="xMidYMid meet">
        <circle id="mycircle" cx="400" cy="300" r="50" />
    </svg>
    <script>
        var mycircle = document.getElementById('mycircle');

        mycircle.addEventListener('click', function (e) {
            console.log('circle clicked - enlarging');
            mycircle.setAttribute('r', 60);
        }, false);
        // 上面代码指定，如果点击图形，就改写circle元素的r属性。
    </script>
</body>

</html>
```

在svg01.md中提到，
>SVG 代码也可以写在一个独立文件中，然后用`<img>`、`<object>`、`<embed>`、`<iframe>`等标签插入网页。

使用`<object>`、`<iframe>`、`<embed>`标签插入 SVG 文件，可以获取 SVG DOM。
```
var svgObject = document.getElementById('object').contentDocument;
var svgIframe = document.getElementById('iframe').contentDocument;
var svgEmbed = document.getElementById('embed').getSVGDocument();
```
注意，如果使用<img>标签插入 SVG 文件，就无法获取 SVG DOM。

###实例：折线图

Date|Amount
-----------|------
2014-01-01 | $10
2014-02-01 | $20
2014-03-01 | $40
2014-04-01 | $80

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        circle {
            stroke-width: 5;
            stroke: #f00;
            fill: #ff0;
        }

        circle:hover {
            stroke: #090;
            fill: #fff;
        }
    </style>
</head>

<body>
    <svg width="350" height="160">
        <g class="layer" transform="translate(60,10)">
          <circle r="5" cx="0"   cy="105" />
          <circle r="5" cx="90"  cy="90"  />
          <circle r="5" cx="180" cy="60"  />
          <circle r="5" cx="270" cy="0"   />
      
          <g class="y axis">
            <line x1="0" y1="0" x2="0" y2="120" />
            <text x="-40" y="105" dy="5">$10</text>
            <text x="-40" y="0"   dy="5">$80</text>
          </g>
          <g class="x axis" transform="translate(0, 120)">
            <line x1="0" y1="0" x2="270" y2="0" />
            <text x="-30"   y="20">January 2014</text>
            <text x="240" y="20">April</text>
          </g>
        </g>
      </svg>
</body>

</html>
```
