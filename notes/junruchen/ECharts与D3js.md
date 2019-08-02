推荐一篇文章：[《我涉及的数据可视化的实现技术和工具
》](http://www.cnblogs.com/zhangdi/p/3690284.html?utm_source=tuicool&utm_medium=referral) 对目前实现数据可视化的技术和工具进行了详细的对比与分析。

最近分别使用了基于canvas的ECharts和以svg为核心的D3进行常见图表的绘制，下面分别对这两个工具的使用，进行整理。

[点击可查看可视化 Demo (针对D3、EChart的图表实现)](https://github.com/junruchen/junruchen.github.io/tree/master/chart)

## ECharts
ECharts官网的教程十分的详细，根据需要的图表类型，传入相应的数据即可。

另外ECharts支持自定义主题，一般图表的样式都可以实现。如果项目中需要大量常规图表，建议使用。
* [ECharts Examples](http://echarts.baidu.com/examples.html)，提供大量实例，基本的图表类型都能找到。
* [ECharts 使用文档 教程](http://echarts.baidu.com/tutorial.html#5%20%E5%88%86%E9%92%9F%E4%B8%8A%E6%89%8B%20ECharts)，包括使用教程，API，配置项等等。
* [ECharts 主题构建工具](http://echarts.baidu.com/theme-builder/)，可构建通用主题，在初始化实例时，注册即可。

## D3
D3是一个可以基于数据来操作文档的JavaScript库。可以帮助你使用HTML,CSS,SVG以及Canvas来展示数据。D3遵循现有的Web标准，可以不需要其他任何框架独立运行在现代浏览器中，它结合强大的可视化组件来驱动DOM操作。

如果项目中需要一些特殊的图表，如流程图、数据库拓扑等，它可以帮助快速实现这些图表效果。
* [SVG基础](https://github.com/junruchen/junruchen.github.io/wiki/SVG%E5%9F%BA%E7%A1%80)，包含svg属性介绍以及svg内部元素基础内容。
* [D3 API文档](https://github.com/d3/d3/wiki)，内包含低版本、高版本的多语言文档。
* [D3 图表demo](https://github.com/d3/d3/wiki/Gallery)，基本的图表类型实例都能找到。