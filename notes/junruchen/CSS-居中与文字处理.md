### 居中
居中是布局中最常遇到的问题，情景不同实现居中的方法也不同，下面分别介绍不同场景下居中的实现方式。另外最常见的水平居中，使用 `margin: 0 auto;` 实现，这个就不再详细介绍了。[点击查看所有居中测试](https://junruchen.github.io/css/demo/css-center-demo.html)

#### 元素宽高固定情况
可使用 `margin` 结合 `top left` 实现。

代码：
```
.box{
  position: relative;
  width: 200px;
  height: 100px;
  background-color: #fb3;
}

.item{
  width: 50px;
  height: 50px;
  background-color: #58a;
  
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -25px 0 0 -25px;
}
```
效果图：

![固定宽高居中.png](http://static.mxnt.net/img/1500315-2dd6238097b782e4.png)

#### 元素宽高不固定情况
**使用 `transform` 结合 `top left` 实现。**
注意：`translate` 必须提供两个值，如果值提供一个值，则该值只作用域X轴，Y轴偏移量为0.

代码：
```
.box{
  position: relative;
  width: 200px;
  height: 100px;
  background-color: #fb3;
}

.item{
  background-color: #58a;
  color: white;
  font-size: 12px;
  
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

dom结构：
<div class="box">
  <div class="item">宽高由元素撑开</div>
</div>
```
效果图：

![transform实现居中.png](http://static.mxnt.net/img/1500315-63d6473a207e4083.png)

**使用 `flex` 布局**

代码：
```
.box{
  display: flex;
  display: -webkit-flex;
  justify-content: center;
  -webkit-justify-content: center;
  align-items: center;
  -webkit-items: center;
  width: 200px;
  height: 100px;
  background-color: #fb3;
}

.item{
  background-color: #58a;
  color: white;
  font-size: 12px;
}
```

**使用 `table-cell` 属性**

注意：三层结构，父级需指定 `display: table;` 属性； 二层元素需设置 `display: table-cell; vertical-align: middle;`；最后一层自元素需要设置宽度以及借助 `margin: 0 auto;` 实现。

代码：
```
.box{
  display: table;
  width: 200px;
  height: 100px;
  background-color: #fb3;
}

.item-box{
  display: table-cell;
  vertical-align: middle;
}

.item{
  margin: 0 auto;
  width: 100px;
}

dom结构：
<div class="box">
  <div class="item-box">
    <div class="item">宽高由元素撑开</div>
  </div>
</div>
```

### 文字处理
文字处理是页面排版中常遇到的问题，而最常见的则是文字换行、文字溢出省略处理以及文字居中。[点击查看所有文字处理测试](https://junruchen.github.io/css/demo/css-text-processing.html)
#### 文字换行
一般情况，都会采用 `word-break：break-all;` 或者 `word-wrap：break-word;` 进行文字换行，那么这两个属性到底有什么区别呢？

看图：

![不同方式对比.png](http://static.mxnt.net/img/1500315-8a2975d5ba307495.png)

第一行采用的是 `word-wrap：break-word;` 的方式进行换行处理， 第二行采用的是 `word-break：break-all;` 。很明显这两种方式的区别是：

`word-wrap`   **先对行尾的单词进行换行，如果换行后单词的长度仍大于盒子的长度，则单词内换行；**

`word-break` **直接进行单词内换行**

在平常的网页排版中，可根据需求选择换行方式。

#### 文字居中
对于单行文字来说，水平方向上的居中一般采用 `text-align: center;` 的方式，垂直方向上的居中一般借助于 `line-height` 实现。对于多行文本，则借助于盒子的居中来实现【盒子的居中见文章开头部分】。

#### 文字溢出省略处理
**单行文本**

分三步，1 设置不换行， 2 设置溢出部分隐藏， 3 文本溢出时元素的状态

代码：
```
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
```
如：

![单行文本溢出处理.png](http://static.mxnt.net/img/1500315-662eca434caca372.png)

**多行文本**

css并没有很好的解决方法来实现多行文本的溢出处理，也可以使用js的方式实现，这里不作说明。

下面展示的方法只适用于WebKit浏览器及移动端【且三个属性必须结合一起使用】：
```
display: -webkit-box;           /*指定将该对象作为弹性伸缩盒子模型*/
-webkit-line-clamp: 3;          /*指定行数*/
-webkit-box-orient: vertical;   /*指定排列方式*/

overflow: hidden;
text-overflow: ellipsis;
```
如：

![多行文本溢出处理.png](http://static.mxnt.net/img/1500315-144bae862fb47de6.png)
