Footer应用场景
1. 自适应内容高度展示在页面最底部
2. 固定于浏览器窗口底部

### Footer 自适应内容高度展示在页面最底部的实现方式
**1、absolute定位**

兼容IE7+

注意：`div.container` 设置最小高度为100%，以保证当内容区高度小于浏览器高度时，footer仍位于底部

页面结构：
```
<body>
  <div class="container">
    <div class="content"></div>
    <footer class="footer"></div>
  </div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%
}
.container {
  position: relative;
  min-height: 100%;
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  background-color: #ccc;
}
.footer {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #666;
}
```
**2、借助margin**

兼容IE7+

借助margin的实现方式有两种，一种是在 `div.content` 使用 `margin-bottom: -50px;`；另一种则是在 `div.footer` 使用 `margin-top: -50px;`

两种方式都需要使用占位元素，以防止content区域的内容被footer覆盖。

页面结构：
```
<body>
  <div class="content">
    <div class="ph"></div>
  </div>
  <footer class="footer"></div>
</body>
```
**方式一**样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  min-height: 100%;
  margin-bottom: -50px;
  background-color: #ccc;
}
.footer {
  width: 100%;
  height: 50px;
  background-color: #666;
}
.ph {
  height: 50px; /*占位元素，与footer高度一致*/
}
```
**方式二**样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  min-height: 100%;
  background-color: #ccc;
}
.footer {
  width: 100%;
  height: 50px;
  margin-top: -50px;
  background-color: #666;
}
.ph {
  height: 50px; /*占位元素，与footer高度一致*/
}
```
**3、借助padding**

兼容IE7+

使用padding实现footer置底，需要为 `div.content` 元素增加一个父元素，且需为 `div.footer` 元素设置 `margin-top: -50px` 来抵消使用padding产生的高度

页面结构：
```
<body>
  <div class="container">
    <div class="content"></div>
  </div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%
}
.container {
  width: 100%;
  min-height: 100%;
  background-color: #ccc;
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  padding-bottom: 50px;
}
.footer {
  width: 100%;
  height: 50px;
  margin-top: -50px; /*用来抵消content使用padding产生的高度*/
  background-color: #666;
}
```
**4、使用calc计算属性**

兼容IE9+，另外webkit内核浏览器使用clac()时，应加前缀'-webkit'

calc的用法比较简单，但是需要注意 'calc' 与 '(' 之间不要有空格，另外运算符前后应该有空格。如：min-height: calc(100% - 50px);

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  min-height: calc(100% - 50px);
  background-color: #ccc;
}
.footer {
  width: 100%;
  height: 50px;
  background-color: #666;
}
```

**5、使用flex布局**

兼容IE11+

flex布局与前面介绍的几种方式相比，footer的高度设置更加灵活，不需要设计计算，也不需要占位符。

另外，flex布局可见[Flex布局属性详解](https://github.com/junruchen/junruchen.github.io/wiki/CSS-Flex%E5%B8%83%E5%B1%80%E5%B1%9E%E6%80%A7%E6%95%B4%E7%90%86)，flex布局扩展用法可见[Flex布局常见应用](https://github.com/junruchen/junruchen.github.io/wiki/CSS-Flex%E5%B8%83%E5%B1%80%E5%B8%B8%E8%A7%81%E5%BA%94%E7%94%A8)

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  -webkit-flex-direction: column; 
}
.content {
  flex: 1;
  -webkit-flex: 1;
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  background-color: #ccc;
}
.footer {
  width: 100%;
  height: 50px;
  background-color: #666;
}
```
**6、使用grid网格布局**

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
  display: grid;
  grid-template-rows: 1fr auto;
}
.content {
  width: 100%;
  height: 500px; /*高度可由内容撑开*/
  background-color: #ccc;
}
.footer {
  grid-row-start: 2;
  grid-row-end: 3;
  width: 100%;
  height: 50px;
  background-color: #666;
}
```


### Footer固定于浏览器窗口底部的实现方式
**1、fixed定位**

兼容IE7+

fixed定位是最常见的实现方式

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
}
.content {
  width: 100%;
  height: 500px;
  background-color: #ccc;
}
.footer{
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #666;
}
```

**2、absolute定位**

兼容IE6+

absolute定位只能将footer置于底部，还需要将 `div.content` 设置为高度固定的可滚动区域，同理上述实现位于页面底部footer的方式，如：flex布局、absolute定位，calc计算属性，都可转换为固定在浏览器窗口底部的方法。

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
}
.content {
  width: 100%;
  height: 100%;
  overflow-y: auto;
  background-color: #ccc;
}
.footer{
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #666;
}
```

**3、flex布局**

兼容IE11+

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  -webkit-flex-direction: column; 
}
.content {
  flex: 1;
  -webkit-flex: 1;
  width: 100%;
  height: 100%;
  overflow-y: auto;
  background-color: #ccc;
}
.footer{
  width: 100%;
  height: 50px;
  background-color: #666;
}
```

**4、calc计算属性**

兼容IE9+

页面结构：
```
<body>
  <div class="content"></div>
  <footer class="footer"></div>
</body>
```
样式代码：
```
html {
  height: 100%;
}
body {
  height: 100%;
}
.content {
  width: 100%;
  height: calc(100% - 50px);
  overflow-y: auto;
  background-color: #ccc;
}
.footer{
  width: 100%;
  height: 50px;
  background-color: #666;
}
```