- [HTML5 新增属性详解](#html5-details1)
- [HTML5 新增标签详解](#html5-details2)
- [HTML5 新增全局属性详解](#html5bese-details3)

----------

### <a name="html5-details1"></a>HTML5 新增标签详解
HTML5增加了主要增加了一些结构标签，媒体标签，表单标签以及一些功能性标签。

1、 结构标签
```
* section 定义文档中的节，如果章节，页眉页脚等，可与h1、h2等标签结合使用，表示文档结构 
* article 定义页面独立的内容区域，如一篇文章
* aside 定义页面的侧边栏内容
* header 定义文档的头部区域
* hgroup 对页面中一个内容区块的标题进行整合
* footer 定义页脚，如作者姓名、地址等
* nav 定义导航部分
* figure 定义独立的流内容，如图像、图标、照片、代码等
```
2、表单标签

需要注意兼容性问题，使用时需严格测试，大部分标签只有高版本浏览器支持。
```
* email 输入邮件地址，提交表单时会自动验证是否合法，如： <input type="email">
* url 输入url地址，提交表单时会自动验证是否合法，如： <input type="url">
* number 输入域为数字，如： 
  <input type="number" max="10">
  特有属性介绍：
      max：设定最大值
      min：设定最小值
      pattern：验证输入字段的模式
      required：不可为空
      step：规定合法的间隔

* range 包含一定范围内数字值的数字域
  <input type="range" min="1" max="10">
  特有属性介绍：
      max：设定最大值
      min：设定最小值
      step：规定合法的间隔

* date 从日期选择器中选择一个日期，如： <input type="date">
* datetime-local 从日期选择器中选择一个日期和时间，如： <input type="datetime-local">
* month 选择一个月份，如： <input type="month">
* week 选择一个周，如： <input type="week">
* search 搜索，如： <input type="search">
* color 颜色选取，可获取颜色相应的十六进制颜色值，如： <input type="color" value="#FFFFFF"> 
```

3、媒体标签

```
* video 定义视频，IE9+，目前只支持MP4、Ogg、WebM格式，如：
  <video src="movie.mp4" controls>您的浏览器不支持video标签</video>
  或者：
  <video width="320" height="240" controls>
      <source src="movie.mp4" type="video/mp4">
      <source src="movie.ogg" type="video/ogg">
      您的浏览器不支持video标签
  </video>
  属性介绍：
      src：视频URL
      autoplay：视频就绪后马上播放
      controls：向用户展示控件，如播放按钮
      height：定义播放器高度
      width：定义播放器宽度
      loop：是否循环播放
      muted：静音
      poster：值为URL，规定点击播放按钮前展示的图像 
      preload：视频在页面加载时就进行加载，并预备播放，如使用autoplay属性，则忽略该属性

* audio 定义音频，IE9+，目前只支持MP3、Ogg、Wav格式，如
  <audio src="music.mp4" controls>您的浏览器不支持audio标签</audio>
  或者：
  <video width="320" height="240" controls>
      <source src="music.mp3" type="audio/mp4">
      <source src="music.ogg" type="audio/ogg">
      您的浏览器不支持audio标签
  </video>  
  属性介绍：
      src：音频URL
      autoplay：视频就绪后马上播放
      controls：向用户展示控件，如播放按钮
      loop：是否循环播放
      muted：静音
      preload：视频在页面加载时就进行加载，并预备播放，如使用autoplay属性，则忽略该属性

* embed 定义嵌入的内容，可以是各种类型的内容，如插件、视频、音频等等
  <embed src="demo.swf" />
  属性介绍：
      src：内容URL
      hight：嵌入内容的高度
      width：嵌入内容的宽度
      type： 嵌入内容的MIME类型，如：application/x-shockwave-flash
      还有一些其它属性可以根据引入的内容类型来选择使用，如当引用内容为音频或视频时，可使用autoplay、loop、volume[音量调节]等属性。
```

4、新增其他功能标签

```
* mark 标记文本，IE9+，如：<mark>被标记文本</mark>
* progress 进度条，IE9+，如：<progress value＝"10" max="100"></progress>
* time 标记时间，方便搜索引擎搜索，IE9+，如：
  <time datetime="2016-02-14">情人节</time>
  还可以设置 pubdate 属性，来表示该时间为文档的创建时间，注意兼容性问题。

* ruby 注释，rt内为注释的内容，rp内为浏览器不支持时展示的内容
  <ruby>
      字
      <rt>zi</rt>
      <rp>当浏览器不支持时，展示内容</rp>
  </ruby>

* canvas 标签定义图形，比如图表和其他图像。该标签基于 JavaScript 的绘图 API
* command 定义命令按钮，如单选按钮、复选框或者按钮，兼容性极差，IE9支持
* details 用于描述文档或文档的某个部分的细节，类似于下拉列表，兼容性较差，chrome与Safari支持，如：
  <details>
      <summary>指定的标题，用户点击标题时展示下面的所有内容，内容可以是任何形式的内容</summary>
      <div>
          <p>内容描述</p>
      </div>
  </details>
  当增设open属性时，描述内容默认展示。
  <details open>
      <summary>指定的标题，用户点击标题时展示下面的所有内容，内容可以是任何形式的内容</summary>
      <div>
          <p>内容描述</p>
      </div>
  </details>

* dialog 定义对话框，如提示框，兼容性较差，chrome与Safari支持，如：
  <dialog>内容</dialog>
  当增设open属性时，对话框显示。
  <dialog open>内容</dialog>

* keygen 加密，新的web标准中已经废弃
* output 计算结果输出展示，IE不支持，如：
  属性介绍：
    name：定义唯一名称，提交表单时使用
    for： 计算中使用的元素
  <form oninput="x.value=parseInt(a.value)+parseInt(b.value)"> 
      0
      <input type="range" id="a" value="50">
      100+
      <input type="number" id="b" value="50">
      =
      <output name="x" for="a b"></output>
  </form>

* menu 菜单，目前主流浏览器不支持
```

---

### <a name="html5-details2"></a>HTML5 新增属性详解

1、sizes 定义链接属性的大小，只对rel="icon"起作用，宽度高度之间用x或者X分隔，如：
```
  <link src="demo.ico" rel="icon" sizes="20x20">
```

2、base 为页面上所有的相对链接规定默认URL或默认目标，如：
```
  一个页面最多只能有一个base标签，且必须位于head标签内，最好放置在第一行。
  <base href="http://www.junru.com/images/" target="_blank">
  <body>
      <img src="demo.png">
      <a href="www.baidu.com">将在新窗口打开，因为base的target属性为_blank</a>
  </body>
```

3、input标签新增属性
```
  新增属性：
    autocomplete：是否启动自动完成功能；
    autofocus：页面加载时自动获取焦点；
    height：设置type＝image的高度；
    width：设置type＝image宽度；
    required：必填；
    placeholder：提示文字；
    pattern：指定输入格式，如pattern="[0-9]";
    multiple：允许多个值；
    list：引用包含输入字段的预定义选项的 datalist；
    max：规定输入字段的最大值；
    maxlength：规定输入字段中的字符的最大长度。
    min：最小值
    form：input 元素所属的一个或多个表单，值必须是form_id；
    formaction：可以覆盖form的action属性；
    formenctype：覆盖表单的 enctype 属性；
    formmethod：覆盖表单的 method 属性；
    formnovalidate：覆盖表单的 novalidate 属性，如果使用该属性，则提交表单时不进行验证。
    formtarget：覆盖表单的 target 属性。
```

4、a 超链接，注意：如果没有href属性，则hreflang、media、rel、target、type不可用。
```
  新增属性：
    download：指定下载链接
    media：指定媒介类型
    type：指定MIME类型
```

5、ol 有序列表，如：
```
  新增属性：
    reserved：倒叙
  <ol start="20" reversed>
    <li>one</li>
    <li>two</li>
    <li>three</li>
  </ol>
```

6、style 内嵌样式，如：
```
  作用范围为父级下的所有元素。
  <div>
    <style>
      h1{color:red;}
      p{font-size:20px;}
    </style>
    <h1>标题</h1>
    <p>内容</p>
  </div>
```

7、iframe
```
  新增属性介绍：
    seamless：使iframe看起来是父文档的一部分，无边框，无边距
    srcdoc：指定页面中html内容展示在iframe中，src失效
    sandbox：禁止一些行为，禁止表单提交，禁止运行js脚本等，有四个参数可指定允许的操作。
```

8、script，新增async属性，规定异步执行脚本（仅适用于外部脚本）

script标签async与defer属性的区别(蓝色：js脚本加载的时间；红色：js脚本执行的时间；绿色：html解析的时间)：

![示例图](http://static.mxnt.net/img/1500315-3321dd314dd75034.png) 
```
1. 没有async与defer参数时，浏览器会立即加载并执行js脚本，按照文档的顺序依次执行；
2. defer：文档的加载与js脚本的加载同时执行，等文档所有元素解析完成后，DomContentLoaded事件触发致歉才执行js脚本
3. async： 文档与js脚本的加载与执行是并行进行的，即异步执行。
```

---

### <a name="html5-details3"></a>HTML5 新增全局属性详解
1、data-* 自定义数据属性，属性名中不要包含大写字母，如：```<p data-type=“content">内容</p>```

2、hidden 隐藏

3、spellcheck拼写验证［错误画红线］<textarea spellcheck=“true"></textarea>

4、contenteditable 指定元素可编辑，如：```<p contenteditable=“true">内容</p>```

5、draggable 指定元素可拖动，具体需结合ondragstart等属性来使用，如：
```
  <p draggable=“true">内容</p>
  
  简单的拖动效果实现：
    <div id="box" ondrop="drop(event)" ondragover="allowDrop(event)"></div> 
    <p draggable=“true" id="drag" ondragstart="drag(event)">拖动的内容</p>
  代码说明：
    1. 拖动数据：ondragstart指定了被拖动的数据
    function drag(event){
      event.dataTransfer.setData("Text",ev.target.id);
      //数据类型text，可拖动元素ID为drag
    }

    2. 放到何处： ondragover指定了在何处放置被拖动的数据
    function allowDrop(event){
      event. preventDefault( );
    }

    3. 放置： ondrop 放置时调用drop函数
    function drop(event){
      ev.preventDefault();
      var data=ev.dataTransfer.getData("Text");
      ev.target.appendChild(document.getElementById(data));
    }
```
