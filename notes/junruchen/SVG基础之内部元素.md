说明：SVG概念，元素样式设置等请查看[SVG基础](https://github.com/junruchen/junruchen.github.io/wiki/SVG%E5%9F%BA%E7%A1%80)
### 目录
* 图形元素
* 文字元素
* 特殊元素
* 滤镜元素
* 渐变元素

## 图形元素
### 1. 矩形
矩形使用`<rect></rect>`标签进行绘制

示例图：

![rectDemo.png](../assets/1500315-31df3693806db8e5.png)

示例代码如下：
```
<svg width="200" height="200">
  <rect x="10" y="10" width="100" height="100" rx="5" ry="5" fill="yellow"></rect>
</svg>
```
参数说明：
* x：左上角x的坐标，距离左边的距离，相当于margin-left
* y：左上角y的坐标，距离顶部的距离，相当于margin-top
* width：矩形的宽度
* height：矩形的高度
* rx：圆角矩形，x轴方向的半径
* ry：圆角矩形，y轴方向的半径

说明：fill用来设置填充颜色，在文章[SVG基础](https://github.com/junruchen/junruchen.github.io/wiki/SVG%E5%9F%BA%E7%A1%80)已进行详细说明，这里不做更多解释

### 2. 圆形
圆形使用`<circle></circle>`标签进行绘制

示例图：

![circleDemo.png](../assets/1500315-938e60b15a3bf859.png)

示例代码如下：
```
<svg width="200" height="200">
  <circle cx="50" cy="50" r="40" fill="yellow"></circle>
</svg>
```
参数说明：
* cx：圆心的x坐标
* cy：圆心的y坐标
* r：半径

### 3. 椭圆形
椭圆形使用`<ellipse></ellipse>`标签进行绘制，与圆形的绘制方法类似。

示例图：

![ellipseDemo.png](../assets/1500315-b29604550ab6c5a5.png)

示例代码如下：
```
<svg width="200" height="200">
  <ellipse cx="50" cy="50" rx="40" ry="20" fill="yellow"></ellipse>
</svg>
```
参数说明：
* cx：圆心的x坐标
* cy：圆心的y坐标
* rx：水平方向上的半径
* ry：垂直方向上的半径

### 4. 线段
线段使用`<line></line>`标签进行绘制

示例代码如下：
```
<svg width="200" height="200">
  <line x1="10" y1="10" x2="90" y2="90" stroke="yellow"></line>
</svg>
```
参数说明：
* x1：起点的x坐标
* y1：起点的y坐标
* x2：终点的x坐标
* y2：终点的y坐标

### 5. 折线与多边形
折线与多边形的绘制方法类似，都是用points属性设置各个点的坐标。

折线使用`<polyline></polyline>`标签进行绘制，而多边形使用`<polygon></polygon>`标签进行绘制，且多边形会将起点与终点连接起来，折线不会。

示例图：

![demo.png](../assets/1500315-51374f4f24f990e6.png)

示例代码如下：
```
/* 图一 折线，不会将起点与终点连接 */
<svg width="200" height="200">
  <polyline points="50,10 80,90 10,30 90,30 20,90" stroke="#fb3" stroke-width="3" fill="transparent"></polyline>
</svg>

/* 图二 多边形，将起点与终点连接 */
<svg width="200" height="200">
  <polygon points="50,10 80,90 10,30 90,30 20,90" stroke="#fb3" stroke-width="3" fill="transparent"></polygon>
</svg>
```
参数说明：
* points：设置各个点的坐标，各组坐标之间使用**空格**分割，x坐标与y坐标之间使用**逗号**分割

### 6. 路径
路径使用`<path></path>`标签进行绘制，使用`d`属性控制路径的类型及绘制。路径的功能最多，前面的所有图形均可使用路径进行绘制。

`d`属性值的书写格式有两种，可以使用逗号分割坐标，如：`d="M10, 10"`，也可使用空格的形式，如：`d="M 10 10"`

**注意：大写字母：表示坐标系中使用绝对坐标，小写字母：使用相对坐标（相对当前画笔所在的点）** 

**移动类**参数：
* M：moveto，将画笔移动到指定坐标，如：`d="M10, 10"`，表示将画笔移动到坐标（10，10）的位置。

**绘制直线类**参数：
* L：lineto，绘制直线到指定坐标，如：`d="M10, 10 L 80 80"`，表示绘制一条起点坐标为（10，10），终点坐标为（80，80）的直线。
* H：horizontal lineto，绘制水平直线到指定坐标，如：`d="M10, 10 H 100"`，表示绘制一条起点坐标为（10，10），终点坐标为（100，10）的直线，注意：H只需要设置一个值，如果设置多个值，则取最后一个值。
* V：vertical lineto，绘制垂直直线到指定坐标，如：`d="M10, 10 V 100"`，表示绘制一条起点坐标为（10，10），终点坐标为（10，100）的直线，注意：V只需要设置一个值，如果设置多个值，则取最后一个值。

**绘制曲线类**参数：
* C：curveto，绘制三次方贝塞尔曲线到终点坐标，中间经过两个控制点控制曲线的弧度，所以需指定三个坐标来绘制曲线，如：`d="M10,10 C40,5 40,140 100,100"`
* S：shorthand/smooth curveto，绘制平滑三次方贝塞尔曲线到终点坐标，与上一条三次方贝塞尔曲线相连，第一个控制点为上一条曲线第二个控制点的对称点，所以还需指定一个控制点坐标和终点坐标，如：`d="M10,10 C40,5 40,140 100,100 S140,180 160,160"`，如果不与贝塞尔曲线相连，即：`d="M10,10 S140,180 160,160"`，则绘制的图线接近于二次贝塞尔曲线。
* Q：quadratic Bezier curveto，绘制二次贝塞尔曲线到终点坐标，中间经过一个控制点控制曲线的弧度，如：`d="M10,10 Q40,140 100,100"`
* T：shorthand/smooth quadratic Bezier curveto，绘制平湖二次贝塞尔曲线到终点坐标，与上一条二次贝塞尔曲线相连，控制点为上一条曲线控制点的对称点，所以还需指定一个终点坐标，如：`d="M10,10 Q40,140 100,100 T160,160"`，如果不与贝塞尔曲线相连，即：`d="M10,10 T160,160"`，则绘制的图线是一条直线。

示例图：

![demo.png](../assets/1500315-2a522d6bae797328.png)

示例代码如下：
```
/* 图一 三次方贝塞尔曲线 */
<svg width="200" height="200">
  <path d="M10,10 C40,5 40,140 100,100" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
</svg>

/* 图二 三次方贝塞尔曲线，与上一条曲线相连 */
<svg width="200" height="200">
  <path d="M10,10 C40,5 40,140 100,100 S140,180 160,160" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
</svg>

/* 图三 二次贝塞尔曲线 */
<svg width="200" height="200">
  <path d="M10,10 Q40,140 100,100" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
</svg>

/* 图四 二次方贝塞尔曲线，与上一条曲线相连 */
<svg width="200" height="200">
  <path d="M10,10 Q40,140 100,100 T160,160" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
</svg>
```

**绘制弧线类**参数：
* A：el liptical arc，绘制椭圆曲线到指定坐标，需设置的参数有：
  1. rx ry：x轴方向半径、y轴方向半径
  2. x-axis-rotation：x轴与水平顺时针方向夹角 
  3. large-arc-flag：角度弧线大小(1:大 0:小) 
  4. sweep-flag：绘制方向(1:顺时针 0:逆时针到终点) 
  5. x y：终点坐标

示例图：

![demo.png](../assets/1500315-5bf35f95531be178.png)

示例代码：
```
<svg width="500" height="500">
    <path d="M50,50 A60 30 0 1,0 150,50 Z" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
  </svg>    
```
分析：起点坐标（50，50），终点坐标（150，50），角度为0。角度弧线大小 large-arc-flag为1，选择大弧度，根据下面分析图，即选择红色的弧线，又绘制方向sweep-flag为0，为逆时针，即从起点沿逆时针防线绘制到终点，所以红色弧线位于下方。

![分析图](../assets/1500315-7bd11452437008f6.png)

注意：当 (起点与终点之间的直线距离／2) > (椭圆的水平半径) 时，角度为0的情况下，此时椭圆会等比放大，到相等为止。


**闭合类**参数：
* Z：closepath，绘制直线将终点与起点连接

**再次提醒：大写字母：表示坐标系中使用绝对坐标，小写字母：使用相对坐标（相对当前画笔所在的点）** 

## 文字元素
在svg中使用`<text></text>`标签绘制文字。

示例图：

![textDemo.png](../assets/1500315-67ce79f2ebda5ec5.png)

示例代码如下：
```
<svg width="200" height="200">
  <text x="10" y="10" dx="10" dy="10" textLength="100" rotate="20">示例文字</text>
</svg>
```
参数说明：
* x：文字的X坐标
* y：文字的Y坐标
* dx：相对于当前位置x方向的距离
* dy：相对于当前位置y方向的距离
* textLength：文字的显示长度（不足则拉长，反之则压缩）
* rotate：旋转角度，也可以使用`transform="rotate(30)"`

**文本路径**

如果想实现文字沿着路径排列，可使用`< textPath ></textPath >`标签。需要提前定义好路径`path`，并指定ID，`textPath`使用`xlink:href`定义文字要匹配的路径。

效果图：

![textpathDemo.png](../assets/1500315-22a4f32af60d8e90.png)

示例代码如下：
```
<svg width="200" height="200">
  <path id="textPath1" d="M100,100 C140,50 140,240 200,200 S240,280 360,360" stroke="#fb3" stroke-width="4px" fill="transparent"></path>
  <text x="10" y="10" dx="-10" dy="-10" rotate="20">
    <textPath xlink:href="#textPath1" textLength="300">
      很扭曲的测试示例文字
    </textPath>
  </text>
</svg>
```

## 特殊元素
### 1. 克隆元素 use
`use`标签用来克隆其他元素，克隆后的元素不能修改样式。
示例图：

![useDemo.png](../assets/1500315-b28cc14485d07e15.png)

示例代码：
```
<svg>
  <rect id="rect1"
        x="10" y="10" width="100" height="100"
        stroke="#5588aa" stroke-width="5"
        fill="transparent"
  ></rect>
  <use x="20" y="20" xlink:href="#rect1"></use>
  </svg>
```
参数说明：
* x：相对被克隆元素x轴偏移量
* y：相对被克隆元素y轴偏移量
* xlink:href：指向被克隆元素的ID

###  2. 模版元素 symbol
`symbol`标签用定义模版，需要结合`use`标签使用，模版在未被使用之前，不会展示在页面上。模版内部可包含多个元素

示例代码：
```
<svg>
  <symbol id="template1">
    <rect x="10" y="10" width="100" height="100"
          stroke="#5588aa" stroke-width="5"
          fill="transparent"
    ></rect>
  </symbol>
  <use x="20" y="20" xlink:href="#template1"></use>
  </svg>
```

###  3. 组元素 g
`group`的简写，用来创建分组，组内所有的元素都会继承`g`的属性，可以嵌套使用，也可以和`use`标签结合使用。另外可使用transform属性定义控制整个组的位置。

示例代码：
```
<svg>
  <g stroke="#5588aa" stroke-width="5" fill="transparent">
    <rect x="10" y="10" width="100" height="100"></rect>
    <rect x="120" y="120" width="100" height="100"></rect>
  </g>
</svg>
```
`g`标签内部的两个矩形，都会继承`g`标签的样式。

###  4. 裁剪元素 clipPath
`clipPath`元素主要用来剪裁元素，`clipPath`元素定义范围外的内容将不会被展示。另外要注意写在`<clipPath></clipPath>`标签内部的元素不会被显示，clipPath标签需要放在defs标签内。其他元素在引用clipPath元素时，需要使用`clip-path="url(#ID)"`。

示例代码如：
```
<svg height="200" width="200">
    <defs>
      <clipPath id="clip">
        <rect width="100" height="100"></rect>
      </clipPath>
    </defs>
    <circle cx="90" cy="90" r="90" clip-path="url(#clip)" stroke="none" fill="yellow" />
  </svg>
```
分析图：

![clipPathDemo.png](../assets/1500315-edfb2ffe237735a7.png)

最终效果图：

![clipPathDemo2.png](../assets/1500315-6d7664a8541af973.png)
###  5. tspan元素
类似`span`标签，如果想为`text`内文字单独设计样式，可使用 `tspan`标签
示例图：

![tspanDemo.png](../assets/1500315-ee713e3025e95550.png)

示例代码：
```
<svg>
  <text x="100" y="100" stroke="#5588aa" textLength="200">
    测试文字<tspan stroke="#ffbb33">单独</tspan>样式
  </text>
</svg>
```
###  6. 超链接元素
类似` a `，使用`xlink:href`指定链接地址
如：
```
<svg height="30" width="200">
  <a xlink:href="https://github.com/junruchen/junruchen.github.io/wiki/SVG基础" 
target="_blank">
    <text x="100" y="100" fill="#ffbb33">SVG基础</text>
  </a>
</svg>
```

###  7. 可重复利用的图形元素 defs
`definitions`缩写，用来定义可重复利用的元素，使用场景如使用`marker`实现线段箭头（见下文 8. 标记元素marker），渐变效果实现等等

### 8. 标记元素marker
可依附于`<path> <line> <polyline> <polygon>`元素上，写在`<des></des>`标签内部，常见的用法是为线段添加箭头。当然也可以为图形元素添加其他内容(如终点处添加圆形、矩形等)
示例图：

![markDemo1.png](../assets/1500315-482846a6a64c93d1.png)

示例代码如下：
```
<svg width="200" height="200">
  <defs>
    <marker 
      id="markerDemo1"
      viewBox="0 0 12 12"
      refX= "6"
      refY="6"
      markerUnits="strokeWidth"
      markerWidth="12"
      markerHeight="12"
      orient="auto">
     <path d="M2,2 L10,6 L2,10 L4,6 L2,2" fill="black"></path>
    </marker>
  </defs>

  <line 
    x1="10" y1="10" 
    x2="160" y2="160"
    stroke="blue" stroke-width="2"
    marker-end="url(#markerDemo1)"></line>
</svg>
```
参数说明：
* viewBox：坐标系区域
* refX refY：viewBox内的基准点，绘制时该点在线上
* makerUnits：标记大小的基准，取值有两个[ strokeWidth| userSpaceOnUse ]，可以是以线的宽度为基准，也可选择以线前端的大小为基准。标记大小根据基准等比放大或者缩小
* markerWidth markerHeight：标记的大小
* orient：绘制方向，auto或者角度值
* id：标记ID

分析图：

![分析图.png](../assets/1500315-880da83d8875dac7.png)

在使用`marker`绘制的箭头时，可使用`marker-start`，`marker-mid`，`marker-end`来控制箭头的位置。
* marker-start：路径起点处绘制箭头
* marker-mid：路径所有的中间端点处绘制箭头，没有中间点，则该属性无效，如上图中的直线，只有终点和起点，使用该属性无效
* marker-end：路径终点处绘制箭头

多个箭头效果图：

![markerDemo2.png](../assets/1500315-420678fef2844d8f.png)

代码：
```
<svg width="200" height="200">
  <defs>
    <marker 
      id="markerDemo2"
      viewBox="0 0 12 12"
      refX= "6"
      refY="6"
      markerUnits="strokeWidth"
      markerWidth="12"
      markerHeight="12"
      orient="auto">
     <path d="M2,2 L10,6 L2,10 L4,6 L2,2" fill="black"></path>
    </marker>
  </defs>

  <path 
    d="M20,70 T80,100 T160,80 T300,120 T200,90"     
    stroke="blue" stroke-width="2" fill="transparent"
    marker-start="url(#markerDemo2)"
    marker-mid="url(#markerDemo2)"
    marker-end="url(#markerDemo2)"></path>
</svg>
```

### 9. 笔刷元素 pattern
可用来制作纹理背景，写在`<defs></defs>`标签内部。

示例图：

![patternDemo.png](../assets/1500315-d2c2c16c5c68252a.png)

代码：
```
 <svg>
  <defs>
    <pattern id="p1" x="0" y="0" width="0.2" height="0.2">
      <circle cx="10" cy="10" r="5" fill="#fb3"></circle>
      <rect x="18" y="18" width="10" height="10" fill="#58a"></rect>
      <polygon points="30 10 60 50 0 50" fill="#58a"></polygon>
    </pattern>
  </defs>
  <rect x="0" y="0" width="200" height="200" fill="url(#p1)"</rect>
</svg>
```

参数说明：
* x y：笔刷的坐标
* width height：笔刷的大小，上述例子中，0.2表示占rect图形元素的50%，也可以使用百分比表示。
* patternUnits：指定`pattern`标签上的单位计算，取值：`[objectBoundingBox | userSpaceOnUse]`，`objectBoundingBox`表示想对图形自身坐标系计算，`userSpaceOnUse`表示想对原始坐标系计算
* patternContentUnits：指定`pattern`标签内部的元素长度、位置的单位计算，取值：`[objectBoundingBox | userSpaceOnUse]`，`objectBoundingBox`表示想对图形自身坐标系计算，`userSpaceOnUse`表示想对原始坐标系计算


## 滤镜元素
使用`filter`标签来标记滤镜，需放在`defs`标签内部，其他元素通过ID引用滤镜。
如：

```
<svg height="110" width="110">
  <defs>
    <filter id="f1" x="0" y="0">
      <feGaussianBlur in="SourceGraphic" stdDeviation="15" />
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"  fill="yellow" filter="url(#f1)" />
</svg>
```
说明：
1. filter：引用的滤镜
2. x y 用来定义滤镜相对于图形元素的位置，如：x="0.2"，相当于图形元素宽度的20%，也可以使用百分比表示。
3. feGaussianBlur：`feGaussianBlur `表示模糊滤镜
4. in：应用的对象，[SourceGraphic | SourceAlpha]，SourceGraphic表示效果应用于整个RGBA图像，SourceAlpha表示使用alpha通道进行效果处理。
5. in2：in3... 应用多个对象，in2="某对象"，使用result输出的对象
6. result：输出对象
7. stdDeviation：定义模糊程度

如：
```
<svg height="120" width="120">
  <defs>
    <filter id="f1" x="0" y="0" width="200%" height="200%">
      <feOffset result="offOut" in="SourceGraphic" dx="20" 
dy="20" />
      <feBlend in="SourceGraphic" in2="offOut" 
mode="normal" />
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"
  fill="yellow" filter="url(#f1)" />
</svg>
```
效果图：

![filter.png](../assets/1500315-04436afc2b62e5eb.png)

### 1. feBlend
### 2. feColorMatrix
### 3. feComponentTransfer
### 4. feComposite
### 5. feConvolveMatrix
### 6. feDisplacementMap
### 7. feFlood
### 8. feGaussianBlur
### 9. feImage
### 10. feMerge
### 11. feMorphology
### 12. feOffset
### 13. feSpecularLighting
### 14. feTile
### 15. feTurbulence
### 16. feDiffuseLighting
### 17. feDistantLight
### 18. fePointLight
### 19. feSpotLight

## 渐变元素
渐变代码写在`defs`标签内部，其他元素使用`url`来指定使用的渐变ID
### 1. 线性渐变 linearGradient

示例图：

![linearGradientDemo.png](../assets/1500315-ff531bcdfdf85fd1.png)
示例代码：
```
<svg>
   <defs>
     <linearGradient id="demo1"
                     x1="0%" y1="0%"
                     x2="0%" y2="100%">
       <stop offset="0%" stop-color="#5588aa" stop-opacity="1" />          
       <stop offset="100%" stop-color="#ffbb33" stop-opacity="1" />
     </linearGradient>
   </defs>
   <rect x="20" y="20" width="100" height="100" fill="url(#demo1)"></rect>
 </svg>
```
参数说明：
* x1 y1 x2 y2：定义渐变的方向
* gradientUnits：用来控制x1 y1 x2 y2的参照对象，取值：[objectBoundingBox | userSpaceOnUse]，objectBoundingBox：默认值，表示参考图形自身坐标系计算；userSpaceOnUse表示参考原始坐标系计算。如下图，均用`x1="0" y1="0" x2="0" y2="10%"`，第一个使用`objectBoundingBox`参考自身坐标系，`y2="10%"`计算的数值大，所以渐变区域也要大。

![gradientUnits.png](../assets/1500315-2d3d9c78b09fd24d.png)

* `stop`标签：`offset`用来指定渐变位置，`stop-color`用来指定该位置的颜色，`stop-opacity`用来控制颜色透明度，可以设置多个`stop`标签

注意：
* 当y1和y2相等，而x1和x2不等时，生成水平渐变色
* 当y1和y2不等，而x1和x2相等时，生成垂直渐变色
* 当y1和y2不等，而x1和x2也不等，生成斜向渐变色

如 `x1="50%" x2="30%" y1="0%" y2="0%"`：

![demo.png](../assets/1500315-0ac556ed9c39b1a9.png)

### 2. 径向渐变 radialGradient
示例图：
![demo2.png](../assets/1500315-109844b7e83c226a.png)

示例代码：
```
<svg>
  <defs>
    <radialGradient id="demo2" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
      <stop offset="0%"  stop-color="#5588aa"/>
      <stop offset="100%" stop-color="#ffbb33"/>
    </radialGradient>
  </defs>
  <rect x="20" y="20" width="100" height="100" fill="url(#demo2)"></rect>
</svg>
```

参数说明：
* cx cy：定义渐变的圆心
* r：定义渐变半径
* fx fy：定义渐变的焦点，可实现类似聚光灯的效果
* gradientUnits：用来控制cx cy r fx fy等的参照对象，取值：[objectBoundingBox | userSpaceOnUse]，与线性渐变一致。
* `stop`标签：`offset`用来指定渐变位置，`stop-color`用来指定该位置的颜色，`stop-opacity`用来控制颜色透明度，可以设置多个`stop`标签