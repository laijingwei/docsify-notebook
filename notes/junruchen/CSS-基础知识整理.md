层叠样式表(Cascading Style Sheets)

- [盒模型](#boxmodel)
- [选择器](#selector)
- [权重与优先级](#weight)
- [继承](#inherit)

----------

### <a name="boxmodel"></a>盒模型

盒模型包含四部分：margin、border、padding、content。如果不使用doctype声明，浏览器默认使用自己的模式解析。如IE使用IE盒模型，firefo则使用标准盒子模型等。

标准盒子模型

![标准盒子模型.png][image1]

IE盒子模型的区别是，content区域包含border和padding

![IE盒子模型.png][image2]


### <a name="selector"></a>选择器
选择器分类：

- 元素选择器
- 通配符选择器 *
- 类选择器
- 属性选择器
    - [attribute] 匹配带指定属性的元素
    - [attribute=value] 匹配带指定属性和值的元素
    - [attribute^=value] 匹配属性值以指定值开头的每个元素，如：`h1[class^=bar]` 匹配class以bar开头的h1元素
    - [attribute$=value] 匹配属性值以指定值结尾的每个元素
    - [attribute*=value] 匹配属性值中包含指定值的每个元素
    - [attribute~=value] 匹配属性值中包含指定值的元素， 必须匹配整个的单词
    - [attribute|=value] 匹配属性值以指定值开头的元素，必须匹配整个单词，或者是`-`前的整个单词
- 后代选择器
    - 匹配后代元素 如：`h1 span`，匹配h1后的所有span标签
    - 匹配子元素 如：`h1 > span`，匹配h1后的所有span子标签
    - 匹配相邻兄弟元素 如：`h1 + .bother`
    - 匹配同父级的后面的兄弟节点 如：`h1 ~ .bother`
- 伪类选择器(针对元素的状态)
    - 使用顺序可以是：:link、:visited、:focus、:hover、:active，因为如果 `:link`和`:visited`放在最后，那所有的元素都会是已访问或者未访问的状态，设置好的`:focus` `:hover` `:active`失效，所以 `:link`和`:visited`最好放置在前面。
    - 链接伪类 `:link` `:visited`
    - 动态伪类 `:focus` `:hover` `:active`
    - 元素伪类 `:first-child`等
- 伪元素选择器(必须放在出现该伪元素的选择器的后面)
    - :first-letter 块级元素的首字母样式
    - :first-line 首行样式
    - :after 元素之后
    - :before 元素之前

**伪类与伪元素区分**

伪类：用于向某些选择器添加特殊的效果，如：:link :active，（在原有的元素上添加类别）伪类的效果可以通过添加一个实际的类来达到

伪元素：用于将特殊的效果添加到某些选择器，如：:after :before，（添加新元素后加以标识）伪元素的效果需要通过添加一个实际的元素才能达到 

### <a name="weight"></a>权重与优先级
权重等级

 - 內联样式 1000
 - ID选择器 0100
 - 类选择器、属性选择器、伪类选择器 0010
 - 元素选择器、伪元素选择器 0001
 - 通配符选择器 0000


优先级计算

 - !important > 內联样式 > 高权重 > 低权重
 - !important > id > class > tag
 - 同权重：內联样式 > 嵌入样式表 > 外部样式表

 
### <a name="inherit"></a>继承 inherit
继承均是沿着dom树向下继承，只有一个特殊情况，即body的背景内容会向上传播到html。

不可继承的属性(与盒模型、position�相关�的)：
 - margin，padding等
 - border，border-radius、box-shadow等
 - float，width，height等

可继承属性(与基本样式设计有关的)：
 - 字体相关，字体颜色、字体大小等
 - 行高
 - 背景颜色等


4、居中
```
  普通元素水平居中（已知宽）：
  margin： 0 auto；
  
  绝对定位absolute元素居中：
      1、（已知宽高）借助 left/top 和 margin-left/margin-top
      2、使用 top:50%, left:50%, transform: translate(-50%, -50%)  translate百分比是相对于自身宽度高度
      3、flex布局
      4、display:table与display:table-cell
         table-cell：让标签元素以表格单元格的形式呈现，类似于td标签
      <div class="toast-container">
        <div class="toast-box">
          <div class="box"></div>
        </div>
      </div>

      <style>
        .toast-container {
            position: fixed;
            width: 100%;
            height: 100%;
            display: table;
        }
        .toast-box {
            display: table-cell;
            vertical-align: middle;
        }
        .box {
            margin: auto;
            width: 100px;
            height: 100px;
            background: #dd0000;
        }
      </style>
```
5、position各个值的定位原点
```
  absolute：绝对定位，相对第一个值不是static的元素定位
  relative：相对定位，相对其正常位置定位
  fiexd：固定定位，相对浏览器窗口
  static：默认值，无定位
  inherit：继承父级position值
```
6、display值介绍
```
  block：块类型，可设置宽高，换行展示
  inline：行内类型，不可设置宽高，同行展示
  inline-block：默认宽度为元素宽度，可设置宽高，同行展示
  none：像行内元素类型一样显示
  table：块级表格
  list-item：像块类型元素一样显示，并添加样式列表标记
  inherit：继承父级
```
7、动画的最小时间间隔最好是多少
```
  多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms
```
8、关于line-height
```
  1）normal 默认值，跟随用户浏览器，与元素字体关联
  2）<number> 如line-height:1.5，假设文字大小20像素，实际行高为 20*1.5
  3）<length> 如line-height:15px;line-height:1.5em [px/pt/em/rem]
  4）<percent>如line-height:150，假设文字大小20像素，实际行高为 20*150%
  5）继承 inherit[IE8+]
  
  注意：
     line-height:1.5，子元素可以继承，根据自己的字体大小进行计算；
     而line-height:150或者line-height:1.5rem，子元素继承，但是不会根据自身字体大小进行计算。 
```
9、元素被设置为float后，display属性的值会自动变成block。

10、:after和:before
```
  之后添加用after；之前用before；
```
11、BFC 块级格式化上下文［block formatting context］
```
  1、BFC是什么
    块级格式化上下文
    样式上：与普通容器无异；
    功能上：可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素
  2、触发BFC的条件(以下任意一个即可)
    浮动元素，float 除none以外的值；
    绝对定位元素，position（absolute，fixed）；
    display为inline-blocks，table-cells，table-captions，table-caption(css3)；
    overflow为hidden，auto，scroll；
  3、BFC的特性
    1）可包含浮动元素
      内部有浮动元素，父容器设置overflow为hidden，auto，scroll即可清除浮动，只有ie7+支持
      清除浮动[兼容IE6]：
        {
          .clearfix｛zoom：1；｝
          .clearfix:after{content: ‘’ ; display:table; clear: both;}
         }
     只是局部可使用.clearfix｛_zoom：1；overflow: hidden;｝ 注意副作用
    2）可阻止元素被浮动元素覆盖等
```
12、浮动元素导致高度塌陷的解决方法
```
  父级设置 overflow：hidden／scroll／auto
  父级元素为 BFC
  父级元素设置height
```
13、外边距合并
```
  即垂直方向上设置margin会合并，如果margin值不一样则选高度大的那一个。
```
14、浏览器兼容性问题
```
  1、各个浏览器的默认设置不同，可选择初始化CSS样式，重现设置；
  2、background-position-x/background-position-x在版本稍低的firefox中不支持，可选择使用background-position
```

[image1]: ../assets/1500315-3deb84742151e74d.png
[image2]: ../assets/1500315-74686c292b221f54.png

