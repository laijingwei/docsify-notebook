## HTML基础

- [基础](#html)
- [HTML5](#html5)
- [语义化](#html-semantic)

------

### <a name="html"></a>基础部分

1、Doctype作用

```
用于告知浏览器解析器采用哪种文档标准解析文档
```

2、标准模式与兼容模式的区别

```
* 标准模式下的排版和JS运作模式均以浏览器支持的最高标准运行

* 兼容模式下页面以宽松的向后兼容的方式显示，模拟老式浏览器的行为以防止站点无法工作
```

3、列举常见的块级元素、行内元素以及空(void)元素

```
* 块级元素：div h1-h6 p hr br header footer article aside table tr ul ol li dl dd dt

* 行内元素：a span strong i img input textarea select label td th

* 空(void)元素: img hr input br mate link col
```

4、页面导入样式时，link与@import有什么区别

```
1）link是XHTML标签，无兼容性问题；除了可以加载css外，还可以定义rss，定义rel连接属性等；@import 由css2.1提出，支持IE5以上，只能用于加载css

2）页面加载时，link中引入的css会同时被加载，而外部样式文件使用@import引用的css会等到页面被加载完再加载

3）可以通过JS操作dom的形式插入link标签来改变样式，而@import方式不可以

4）@import必须写在除@charset外的其他任何css规则之前，否则将被浏览器忽略。如果@import之后还有其他样式，则比如在语句结尾加上分号

总结：慎用@import方式，可以避免考虑@import的愈发规则和注意事项，避免产生资源下载顺序混乱以及http请求过多的问题
```

5、对浏览器内核的理解

```
分为两部分：渲染引擎和JS引擎。

* 渲染引擎主要负责网页的内容，如获取html内容，加入css等

* JS引擎主要用于服务解析和执行javascript来实现网页的动态效果
```

6、常见的浏览器内核

```
* Webkit内核: Safari, Google Chrome, Opera, 百度、猎豹等浏览器

* Trident内核: IE浏览器

* Gecko内核: Firefox浏览器

* Presto内核: Opera mini移动端浏览器
```

7、DOM文档的加载顺序
```
解析HTML结构

加载外部脚本和样式文件

解析并执行脚本代码

DOM树构建完成(DOMContentLoaded)

加载图片以及外部文件

页面加载完毕(load)
```

8、浏览器的执行过程

```
加载，根据请求的URL进行域名解析，向服务器端发送请求，接受响应文件(HTML JS CSS 图片等)

解析，对加载到的资源进行语法解析，构建响应的数据结构(DOM树，CSS样式规则，JS对象属性表等)

渲染，对各个元素进行位置计算、样式计算等，然后根据渲染树完成页面布局

总结：过程之间会有交叉，不是完全独立
```

9、script标签的defer与async属性的不同点

![示例图](../assets/1500315-3321dd314dd75034.png)

```
* 无defer或者async属性时，按照文档自上而下解析，当解析到script元素时，立即加载，且等到执行完成后继续解析DOM

* defer属性表示会立即异步下载脚本文档，且等到DOM解析完毕，DOMContentLoaded事件触发之前执行脚本

* async属性表示会立即异步下载脚本文件，下载完成后，立即停止解析DOM，执行脚本文件，直至执行完毕，继续解析DOM
```

------

### <a name="html5"></a>HTML5

1、HTML5 为什么只需要写`<!DOCTYPE HTML>`

```
HTML5不基于SGML，因此不需要对DTD进行引用，但是需要使用doctype来规范浏览器的行为。

* SGML(Standard Generalized Markup Language) 标准通用标记语言

* DTD(Document Type Definition) 文档类型定义
```

2、简述HTML5增加了哪些新特性？

[HTML5新增标签属性详细说明](https://github.com/junruchen/junruchen.github.io/wiki/HTML-HTML5%E6%96%B0%E5%A2%9E%E6%A0%87%E7%AD%BE%E5%B1%9E%E6%80%A7%E6%95%B4%E7%90%86)

```
主要是关于位置、图像、存储、多任务等功能的增加

* 新标签：语义化结构标签(如 header、footer、nav等)、表单类型(如 email、url等)、媒体标签(如 audio、video等)、其他功能性标签(如 mark标记文本、progress进度条、canvas定义图形等)

* 新属性：常见标签属性的增加(如 link标签的sizes属性、input标签的autofocus属性等)、全局属性(如 hidden隐藏、data-*自定义数据属性等)

* 存储：localStorage、sessionStorage

* 新技术：webWorker、webscoket、Geolocation
```

3、简述HTML5移除了哪些元素？

```
* 纯表现类元素：basefont、big、center、font、s等

* 可用性产生负面影响的元素：frame、noframes等
```

4、如何处理浏览器的兼容性问题？

```
* 可以借助IE6-8支持document.createElement创建标签的特性使浏览器支持HTML5新标签；

* 使用成熟的框架html5shim
```

9、HTML5的离线储存怎么使用，工作原理能不能解释一下？

 10、浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢？ 

11、请描述一下 cookies，sessionStorage 和 localStorage 的区别？

---

### <a name="html-semantic"></a>HTML语义化问题(面试必问)

1、简述一下对HTML语义化的理解

```
用正确的标签做正确的事
* 代码更可读，利于代码维护
* 对SEO更友好
```

2、如何实现HTML语义化

 
 12、iframe有那些缺点？ 
13、Label的作用是什么？是怎么用的？（加 for 或 包裹） 
14、HTML5的form如何关闭自动完成功能？
 15、如何实现浏览器内多个标签页之间的通信? (阿里) 
16、webSocket如何兼容低浏览器？(阿里)
 17、页面可见性（Page Visibility）API 可以有哪些用途？
 18、如何在页面上实现一个圆形的可点击区域？
 19、实现不使用 border 画出1px高的线，在不同浏览器的Quirksmode和CSSCompat模式下都能保持同一效果。 
20、网页验证码是干嘛的，是为了解决什么安全问题？
 21、title与h1的区别、b与strong的区别、i与em的区别？
22、什么是cookie隔离【请求资源时如何才能不带cookie】
23、解释png\jpg\gif图片格式，分别什么时候用，对webp有没有了解
24、web开发中会话跟踪的方法
25、img标签的title与alt的区别
