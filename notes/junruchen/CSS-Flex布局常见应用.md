如果想了解更多关于Flex布局的内容，可以查看[Flex布局属性整理][link2]

### 目录
* 满屏“品”字布局
* 居左居右布局[上下居中]
* 栅格系统

### 1、满屏“品”字布局
【某前端面试题】要求，盒子500*500，顶部盒子width为100%，高度为250，下面两个盒子宽度各占一半，高度占满剩下的所有高度。

效果图：

![满屏“品”字布局][image1]

分析：
首先上下两层盒子，第一层高度固定为250px，第二个盒子高度要求占满，所以要使用flex布局；另外这两层盒子是垂直排列的，所以要设置布局的方向。

代码：
```
    //dom结构
    <div class="box">
        <div class="box-item">Item1</div>
        <div class="box-item">
            <div class="item">Item2</div>
            <div class="item">Item3</div>
        </div>
    </div>

    //样式设计
    .box{
        width: 500px;
        height:500px;
        border: 1px solid;

        display: flex;
        flex-direction: column;
    }
    .box .box-item:first-child{  /* 根据要求设置上面第一层的宽度高度 */
        width: 100%;
        height: 250px;
    }
    .box .box-item:last-child{ 
        flex: 1;  /* 高度占满 */
        display: flex;
        flex-direction: row;
    }
    .item{
        width: 50%;
    }
```
### 2、居左居右布局[上下居中]
【某前端面试题】要求：间距为20像素，上下居中，两个子元素居左，一个子元素居右，父级元素宽度不固定，只能使用flex布局。

效果图:

![demo.png][image2]

分析：

* 父级元素使用flex布局，上下居中使用align-items控制；
* 第三个子元素居右采用：margin-left:auto 实现。

[效果预览][link1]

主要代码：
```
    //dom结构
    <div class="box">
        <div class="box-item"></div>
        <div class="box-item"></div>
        <div class="box-item"></div>
    </div>

    //样式设计
    .box{
        ...

        display: flex;
        align-items: center;
    }
    .box .box-item:last-child{
        margin-left: auto;
    }
```

### 3、栅格系统
栅格系统是自适应系统中最为常见的布局

**基础栅格**

要求：每一行等宽登高，且自适应容器宽度

效果图:

![demo.png][image3]

分析：

* 父级元素使用flex布局；
* 子元素不需要设置宽度，只需要设置 `flex-basis: 50%` 或者  `flex-grow: 1`  就可以实现均分效果。

**非等宽栅格**

要求：行中可以给某一项单独设置宽度，剩下的项平分剩余空间

![demo.png][image4]

* 父级元素使用flex布局；
* 除特殊项外子元素不需要设置宽度，只需要设置 `flex-grow: 1`就可以实现均分效果。`flex-grow` 设置扩展比例，即剩余空间的分配比率。

[image1]: ../assets/1500315-c0710d355d691c8e.png
[image2]: ../assets/1500315-1cb4ec255177082b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500
[image3]: ../assets/1500315-e9906573f6325f8d.png
[image4]: ../assets/1500315-3780035bcf9976e4.png

[link1]: (https://junruchen.github.io/css/demo/css-flex-usage1.html)
[link2]: (https://github.com/junruchen/junruchen.github.io/wiki/CSS-Flex%E5%B8%83%E5%B1%80%E5%B1%9E%E6%80%A7%E6%95%B4%E7%90%86)