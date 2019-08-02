Flex布局
* `display: flex;` 将对象作为弹性伸缩盒展示，用于块级元素
* `display: inline-flex;` 将对象作为弹性伸缩盒展示，用于行内元素

注意兼容问题：
* webkit内核浏览器应使用前缀`-webkit`
* IE浏览器，可以很好的兼容IE11+版本，对于IE10只有部分可以兼容，且使用时需增加`-ms`，IE10浏览器中容器定义成弹性伸缩盒时，需使用`display: -ms-flexbox`

示例的dom结构：
```
<div class="box"> <!--容器-->
  <div class="item">1</div> <!--子项-->
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```
示例的基础样式：
```
.box {
  width: 200px;
  height: 200px;
  background-color: #58a;
}
.item {
  width: 50px;
  height: 50px;
  margin: 2px;
  background-color: #fb3;
}
```
### Flex 作用于Box容器上的6个属性介绍
**1、flex-direction**

用于指定Flex主轴的方向，继而决定 Flex子项在Flex容器中的位置

取值：row | row-reverse | column | column-reverse
* row：默认值，表示水平方向从左到右排列，此时水平方向轴线为主轴
* row-reverse：与row相反
* column：表示垂直方向从上到下排列，此时垂直方向轴线为主轴
* column-reverse：与column相反

`flex-direction`四种取值的效果图如下：

![row.png][image1]
![column.png][image2]

**2、flex-wrap**

用于指定Flex子项是否换行

取值：nowrap | wrap | wrap-reverse
* nowrap：默认值，表示不换行，Flex子项可能会溢出
* wrap：表示换行，溢出的Flex子项会被放到下一行
* wrap-reverse：表示反方向换行

`flex-wrap`三种取值的效果图如下：

![wrap.png][image3]

从示例图中不难发现，换行以后两行之间产生了很大的间距，这个问题，在后面介绍的 `align-content` 属性中可以得到很好的解决。

**3、flex-flow**

复合属性，是`flex-direction` 和 `flex-wrap` 的简写属性，是用于指定Flex子项的排列方式

**4、justify-content**

用于指定主轴(水平方向)上Flex子项的对齐方式

取值：flex-start | flex-end | center | space-between | space-around
* flex-start：默认值，表示与行的起始位置对齐
* flex-end：表示与行的结束位置对齐
* center：表示与行中间对其
* space-between：表示两端对齐，中间间距相等。要注意特殊情况，当剩余空间为负数或者只有一个项时，效果等同于`flex-start`
* space-around：表示间距相等，中间间距是两端间距的2倍。要注意特殊情况，当剩余空间为负数或者只有一个项时，效果等同于`center`

`justify-content` 的前三种取值的效果图如下：

![normal.png][image4]

`justify-content` 取值为 `space-between` 的效果图如下(注意特殊情况下效果等同于flex-start)：

![space-between.png][image5]

`justify-content` 取值为 `space-around` 的效果图如下(注意特殊情况下效果等同于center)：

![space-around.png][image6]

**5、align-items**

用于指定侧轴(垂直方向)上Flex子项的对齐方式

取值：stretch | flex-start | flex-end | center | baseline
* stretch：默认值，当Flex子项未设置高度或者高度值为auto时，stretch起作用，将Flex子项高度设置为行高度。这里需要注意，在只有一行的情况下，行的高度为容器的高度，即Flex子项高度为容器的高度
* flex-start：表示与侧轴开始位置对齐
* flex-end：表示与侧轴的结束位置对齐
* center：表示与侧轴中间对其
* baseline：表示基线对齐，当行内轴与侧轴在同一线上，即所有Flex子项的基线在同一线上时，效果等同于`flex-start`

`align-items` 取值为 `stretch` 的效果图如下：

![stretch.png][image7]

`align-items` 取值为 `flex-start flex-end center` 的效果图如下：

![normal.png][image8]

`align-items` 取值为 `baseline` 的效果图如下：

![baseline.png][image9]

**6、align-content**

该属性只作用于**多行**的情况下，用于多行的对齐方式

取值：stretch | flex-start | flex-end | center | space-between | space-around
* stretch：默认值，当Flex子项未设置高度或者高度值为auto时，stretch起作用，将Flex子项高度设置为行高度。
* flex-start：表示各行与侧轴开始位置对齐，第一行紧靠侧轴开始边界，之后的每一行都紧靠前面一行
* flex-end：表示各行与侧轴的结束位置对齐，最后一行紧靠侧轴结束边界，之后的每一行都紧靠前面一行
* center：表示各行与侧轴中间对其
* space-between：表示两端对齐，中间间距相等。要注意特殊情况，当剩余空间为负数时，效果等同于`flex-start`
* space-around：表示各行之间间距相等，中间间距是两端间距的2倍。要注意特殊情况，当剩余空间为负数时，效果等同于`center`

再次强调：该属性只作用于多行的情况，在只有一行的Flex容器上无效，另外该属性可以很好的处理，换行以后相邻行之间产生的间距。

`align-content` 各个取值的效果图如下：

![align-content.png][image10]


### Flex 作用于子项上的6个属性介绍
**1、order**

该属性用来指定Flex子项的排列顺序，数值越小，越靠前，可以为负数

取值：数值，默认值为0

**2、flex-grow**

用来指定Flex子项的扩展比例，不可以为负数，Flex容器会根据Flex子项设置的扩展比例作为比率来分配剩余空间

取值：数值，默认值为0，表示即使存在剩余空间，Flex子项也不会扩展

如下图中，按照1:3分配剩余空间：

![grow.png][image11]

**3、flex-shrink**

用来指定Flex子项的收缩比例，不可以为负数，Flex容器会根据Flex子项设置的收缩比例作为比率来收缩各个Flex子项

取值：数值，默认值为1，表示所有子项在剩余空间为负数时，等比例收缩

注意：`flex-shrink`只能在不换行的情况下使用

如下图中，按照1:3收缩：

![shrink.png][image12]

**4、flex-basis**

用来指定Flex子项的占据的空间，不可以为负数

取值：auto | length | percentage | content
* auto：默认值，计算规则：检索Flex子项是否设置了width值（或者height值，取决于flex-direction），如果设置了非auto的值，则使用width值（或者height值），若没有则使用content
* length：用长度值定义宽度，不可为负数
* percentage：使用百分比定义宽度，不可为负数

如下图中，为Item设置 `flex-basis: 50%; ` ,在按照1:3分配剩余空间：

![grow.png][image13]

容器宽度为200px，Item1原始宽度为50px，设置 `flex-basis: 50%; `后宽度变成100px，扩展后宽度为110.5px；而Item2原始宽度为50px，扩展后为81.5px，比例正好是1:3

注意：
1. 设置`flex-grow`进行分配剩余空间，或者使用`flex-shrink`进行收缩都是在flex-basis的基础上进行的；

2. 当`flex-basis`的值以及width（或者height）的值均为非auto时，
 * 1）若content长度同时大于`flex-basis`的值以及width（或者height）的值，此时以`flex-basis`与width（或者height）中值大的为准 ，**但是**，如果子项设置了`overflow: hidden;`或者`overflow: auto;`，此时以`flex-basis`值为准；
 * 2）若content长度同时小于`flex-basis`的值以及width（或者height）的值，此时以`flex-basis`值为准；
 * 3）若content长度小于`flex-basis`的值，大于width（或者height）的值，此时以`flex-basis`值为准；
 * 4）若content长度大于`flex-basis`的值，小于width（或者height）的值，此时以content自身长度值为准；

3. 当width（或者height）的值为auto时，且内容的长度大于`flex-basis`设置的值，此时以content自身长度值为准，且**不能进行flex-shrink收缩**。相反如果内容的长度小于`flex-basis`设置的值，则会使用`flex-basis`设置的值；
4. 当存在最小值 `min-width`（`min-height`）时，且 `flex-basis`的值小于最小值时，宽度以最小值为准，当 `flex-basis`的值大于最小值时，以 `flex-basis`的值为准

**5、flex**

复合属性，是`flex-grow` 、 `flex-shrink`  和 `flex-basis` 的简写属性，用来指定Flex子项如何分配空间

取值：none | 各拆分项属性
* none：0 0 auto
* auto：1 1 auto
* 1：1 1 0%
* 0 auto 或 initial：0 1 auto 即初始值

注意：
* flex-grow：默认值为0，若省略则被默认为1
* flex-shrink：默认值为1，省略时默认为1
* flex-basis：默认值为auto，省略时默认为0%

**6、align-self**

用来单独指定某Flex子项的对齐方式

取值：auto | flex-start | flex-end | center | baseline | stretch
* auto：默认值，查找父元素的`align-items`值，如果没有则取值为`stretch`
* 其他值同`align-items`

[flex属性用法示例][link1]

如果想了解更多关于Flex布局的内容，可以查看[Flex布局常见应用][link2]

[image1]: ../assets/1500315-ae4221ba84201761.png
[image2]: ../assets/1500315-0f557e69efb8d339.png
[image3]: ../assets/1500315-7d21694a786b11b6.png
[image4]: ../assets/1500315-697872b571e8bde8.png
[image5]: ../assets/1500315-8bbfb0edf27b8ce7.png
[image6]: ../assets/1500315-cedce0a496df3c74.png
[image7]: ../assets/1500315-e2f6331d9f1a960e.png
[image8]: ../assets/1500315-83fc5339890ff1f7.png
[image9]: ../assets/1500315-95e8d3492d9ad9bb.png
[image10]: ../assets/1500315-a7f3503e0c708b8d.png
[image11]: ../assets/1500315-174c4c96c1b7ff91.png
[image12]: ../assets/1500315-817e044ac869be24.png
[image13]: ../assets/1500315-6a9274535cf2f280.png

[link1]: https://junruchen.github.io/css/demo/css-flex-demo.html
[link2]: https://github.com/junruchen/junruchen.github.io/wiki/CSS-Flex%E5%B8%83%E5%B1%80%E5%B8%B8%E8%A7%81%E5%BA%94%E7%94%A8