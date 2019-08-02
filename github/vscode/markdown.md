# Markdown 基本要素
这篇文件意在简要介绍 [GitHub Flavored Markdown 写作](https://guides.github.com/features/mastering-markdown/)。      

## 什么是 Markdown?  
`Markdown` 是一种文本格式。你可以用它来控制文档的显示。使用 markdown，你可以创建粗体的文字，斜体的文字，添加图片，并且创建列表 等等。基本上来讲，Markdown 就是普通的文字加上 `#` 或者 `*` 等符号。  

## 语法说明

### 标题
```markdown
# 这是 <h1> 一级标题
## 这是 <h2> 二级标题
### 这是 <h3> 三级标题
#### 这是 <h4> 四级标题
##### 这是 <h5> 五级标题
###### 这是 <h6> 六级标题
```

如果你想要给你的标题添加 `id` 或者 `class`，请在标题最后添加 `{#id .class1 .class2}`。例如：  
```markdown
# 这个标题拥有 1 个 id {#my_id}
# 这个标题有 2 个 classes {.class1 .class2}
```
> 这是一个 MPE 扩展的特性。  

### 强调
```markdown
*这会是 斜体 的文字*
_这会是 斜体 的文字_

**这会是 粗体 的文字**
__这会是 粗体 的文字__

_你也 **组合** 这些符号_

~~这个文字将会被横线删除~~
```

### 列表
#### 无序列表
```markdown
* Item 1
* Item 2
  * Item 2a
  * Item 2b
```

#### 有序列表
```markdown
1. Item 1
1. Item 2
1. Item 3
   1. Item 3a
   1. Item 3b
```

### 添加图片  
```markdown
![GitHub Logo](/images/logo.png)
Format: ![Alt Text](url)
```

### 链接  
```markdown
http://github.com - 自动生成！
[GitHub](http://github.com)
```

### 引用
```markdown
正如 Kanye West 所说：

> We're living the future so
> the present is our past.

```

### 分割线  
```markdown
如下，三个或者更多的

---

连字符

***

星号

___

下划线
```

### 行内代码
```markdown  
我觉得你应该在这里使用
`<addr>` 才对。
```

### 代码块
你可以在你的代码上面和下面添加 <code>\`\`\`</code> 来表示代码块。

#### 语法高亮
你可以给你的代码块添加任何一种语言的语法高亮  

例如，给 ruby 代码添加语法高亮：

    ```ruby
    require 'redcarpet'
    markdown = Redcarpet.new("Hello World!")
    puts markdown.to_html
    ```

会得到下面的效果：

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

#### 代码块 class（MPE 扩展的特性）
你可以给你的代码块设置 `class`。

例如，添加 `class1 class2` 到一个 代码块：

    ```javascript {.class1 .class}
    function add(x, y) {
      return x + y
    }
    ```

##### 代码行数
如果你想要你的代码块显示代码行数，只要添加 `line-numbers` class 就可以了。

例如：

    ```javascript {.line-numbers}
    function add(x, y) {
      return x + y
    }
    ```

将会得到下面的显示效果：

![screen shot 2017-07-14 at 1 20 27 am](https://user-images.githubusercontent.com/1908863/28200587-a8582b0a-6832-11e7-83a7-6c3bb011322f.png)


##### 高亮代码行数

你可以通过添加 `highlight` 属性的方式来高亮代码行数：

````markdown
```javascript {highlight=10}
```

```javascript {highlight=10-20}
```

```javascript {highlight=[1-10,15,20-22]}
```
````

### 任务列表   
```markdown  
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
```

### 表格
```markdown  
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
```

## 扩展的语法
### 表格  
![screen shot 2017-07-15 at 8 16 45 pm](https://user-images.githubusercontent.com/1908863/28243710-945e3004-699a-11e7-9a5f-d74f6c944c3b.png)

### Emoji & Font-Awesome

> 只适用于 `markdown-it parser` 而不适用于 `pandoc parser`。    
> 缺省下是启用的。你可以在插件设置里禁用此功能。  

```
:smile:
:fa-car:
```

### 上标
```markdown
30^th^
```

### 下标
```markdown
H~2~O
```

### 脚注
```markdown
Content [^1]

[^1]: Hi! This is a footnote
```

### 缩略  
```markdown  
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
The HTML specification
is maintained by the W3C.
```

### 标记  
```markdown
==marked==
```

### CriticMarkup  
CriticMarkup 缺省是禁用的，你可以通过插件设置来启动它。    
有关 CriticMarkup 的更多信息，请查看 [CriticMarkup 用户指南](http://criticmarkup.com/users-guide.php).    

这里有 5 种基本语法：

* 添加 `{++ ++}`
* 删除 `{-- --}`
* 替换 `{~~ ~> ~~}`
* 注释 `{>> <<}`
* 高亮 `{== ==}{>> <<}`

> CriticMarkup 仅可用于 markdown-it parser，不与 pandoc parser 兼容。  

## 参考
* [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
* [Daring Fireball: Markdown Basics](https://daringfireball.net/projects/markdown/basics)


# 图像

**Markdown Preview Enhanced** 内部支持 `flow charts`, `sequence diagrams`, `mermaid`, `PlantUML`, `WaveDrom`, `GraphViz`，`Vega & Vega-lite`，`Ditaa` 图像渲染。
你也可以通过使用 [Code Chunk](zh-cn/code-chunk.md) 来渲染 `TikZ`, `Python Matplotlib`, `Plotly` 等图像。

> Please note that some diagrams doesn't work well with file export like PDF, pandoc, etc.

## Flow Charts

这一特性基于 [flowchart.js](http://flowchart.js.org/)。
* `flow` 代码快中的内容将会被 [flowchart.js](http://flowchart.js.org/) 渲染。

![screenshot from 2017-11-25 21-43-02](https://user-images.githubusercontent.com/1908863/33236942-aa809c1c-d229-11e7-9c4b-9a680fd852ed.png)

## Sequence Diagrams

这一特性基于 [js-sequence-diagrams](https://bramp.github.io/js-sequence-diagrams/)。
* `sequence` 代码快中的内容将会被 [js-sequence-diagrams](https://bramp.github.io/js-sequence-diagrams/) 渲染。
* 支持两个主题 `simple`（默认主题）和 `hand`。

![screenshot from 2017-11-25 21-47-41](https://user-images.githubusercontent.com/1908863/33236972-4f190f98-d22a-11e7-842f-d9c4a74d2118.png)


## Mermaid

Markdown Preview Enhanced 使用 [mermaid](https://github.com/knsv/mermaid) 来渲染流程图和时序图。
- `mermaid` 代码块中的内容将会渲染 [mermaid](https://github.com/knsv/mermaid) 图像。
- 查看 [mermaid 文档](http://knsv.github.io/mermaid/#flowcharts-basic-syntax) 了解更多如果创建图形。
![screen shot 2017-06-05 at 8 04 58 pm](https://cloud.githubusercontent.com/assets/1908863/26809423/42afb410-4a2a-11e7-8a18-57e7c67caa9f.png)

三个 mermaid 主题是支持的，并且你可以在 [插件设置](zh-cn/usages.md?id=package-settings) 中设置主题：
* `mermaid.css`
* `mermaid.dark.css`
* `mermaid.forest.css`
![screen shot 2017-06-05 at 8 47 00 pm](https://cloud.githubusercontent.com/assets/1908863/26810274/555562d0-4a30-11e7-91ca-98742d6afbd5.png)

你还可以通过 `Markdown Preview Enhanced: Open Mermaid Config` 命令打开 mermaid 配置文件。


## PlantUML

Markdown Preview Enhanced 使用 [PlantUML](http://plantuml.com/) 来创建各种图形。（**Java** 是需要先被安装好的）
- 你可以安装 [Graphviz](http://www.graphviz.org/)（非必需）来辅助生成各种各种图形。
- `puml` 或者 `plantuml` 代码块中的内容将会被 [PlantUML](http://plantuml.com/) 渲染。

![screen shot 2017-06-05 at 8 05 55 pm](https://cloud.githubusercontent.com/assets/1908863/26809436/65414084-4a2a-11e7-91ee-7b03b0496513.png)

如果代码中 `@start...` 没有被找到，那么 `@startuml ... @enduml` 将会被自动添加。

## WaveDrom

Markdown Preview Enhanced 使用 [WaveDrom](http://wavedrom.com/) 来渲染 digital timing diagram.
- `wavedrom` 代码块中的内容将会被 [WaveDrom](https://github.com/drom/wavedrom) 渲染。

![screen shot 2017-06-05 at 8 07 30 pm](https://cloud.githubusercontent.com/assets/1908863/26809462/9dc3eb96-4a2a-11e7-90e7-ad6bcb8dbdb1.png)

## GraphViz
Markdown Preview Enhanced 使用 [Viz.js](https://github.com/mdaines/viz.js) 来渲染 [dot 语言](https://tinyurl.com/kjoouup) 图形。
- `viz` 或者 `dot` 代码块中的内容将会被 [Viz.js](https://github.com/mdaines/viz.js) 渲染。
- 你可以通过 `{engine="..."}` 来选择不同的渲染引擎。 引擎 `circo`，`dot`，`neato`，`osage`，或者 `twopi` 是被支持的。默认下，使用 `dot` 引擎。

![screen shot 2018-03-18 at 3 18 17 pm](https://user-images.githubusercontent.com/1908863/37570596-a565306e-2abf-11e8-8904-d73306f675ec.png)

## Vega 和 Vega-lite
Markdown Preview Enhanced 支持 [vega](https://vega.github.io/vega/) 以及 [vega-lite](https://vega.github.io/vega-lite/) 的**静态**图像.
* `vega` 代码块中的内容将会被 [vega](https://vega.github.io/vega/) 渲染。
* `vega-lite` 代码块中的内容将会被  [vega-lite](https://vega.github.io/vega-lite/) 渲染。
* `JSON` 以及 `YAML` 的输入是支持的。

![screen shot 2017-07-28 at 7 59 58 am](https://user-images.githubusercontent.com/1908863/28718265-d023e1c2-736a-11e7-8678-a29704f3a23c.png)

你也可以 [@import](zh-cn/file-imports.md) 一个 `JSON` 或者 `YAML` 文件作为 `vega` 图像，例如：

```markdown
@import "your_vega_source.json" {as="vega"}
@import "your_vega_lite_source.json" {as="vega-lite"}
```

## Ditaa
Markdown Preview Enhanced 支持 [ditaa](https://github.com/stathissideris/ditaa)。

(**Java** 是需要先被安装好的)

`ditaa` 整合于 [code chunk](zh-cn/code-chunk.md), for example:
<pre>
  ```ditaa {cmd=true args=["-E"]}
  +--------+   +-------+    +-------+
  |        | --+ ditaa +--> |       |
  |  Text  |   +-------+    |diagram|
  |Document|   |!magic!|    |       |
  |     {d}|   |       |    |       |
  +---+----+   +-------+    +-------+
      :                         ^
      |       Lots of work      |
      +-------------------------+
  ```
</pre>

> <kbd>shift-enter</kbd> 来运行 code chunk。
> 设置 `{hide=true}` 来隐藏代码块。
> 设置 `{run_on_save=true}` 启动当文件保存时，渲染 ditaa 图像。

![screen shot 2017-07-28 at 8 11 15 am](https://user-images.githubusercontent.com/1908863/28718626-633fa18e-736c-11e7-8a4a-915858dafff6.png)

---

如果你只是想要显示代码块而不想画图，则只要在后面添加 `{code_block=true}` 即可：

    ```mermaid {code_block=true}
    // 你的 mermaid 代码
    ```

---

你可以为图像的容器添加属性。
例如：

    ```puml {align="center"}
    a->b
    ```

将会把 puml 的图像放在中间。

---

当你保存你的 markdown 文件到 [GFM Markdown](zh-cn/markdown.md) 时， 所有图像将会被保存为 png 文件到 `imageFolderPath` 文件夹。
你可以设置导出文件的文件名 `{filename="图片.png"}`。

例如：

    ```mermaid {filename="我的mermaid.png"}
    ...
    ```

