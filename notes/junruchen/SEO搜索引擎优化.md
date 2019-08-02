# SEO(Search Engine Optimization)

SEO 主要就是通过对网站的关键词，主题，链接，结构，标签，排版等各方面进行优化，使搜索引擎更容易搜索到网站的内容，并且让网站的各个网页在搜索引擎（ Google 、百度、 Yahoo ……）中获得较高的评分，从而获得较好的排名。

主流的搜索引擎有 google，baidu，yahoo，各个搜索引擎之间还有自己细微的差别，所以想做在所有搜索引擎中排名靠前是比较困难的，所谓的SEO大多说针对单一的搜索引擎，并且国内外以google为目的SEO占多数。需要注意的是，SEO是一个长期系统的过程，根据网上的经验大概是3-6个月才能看到成果，所以做SEO一定要有恒心。

实现搜索引擎优化的方式包括【**关键词策略**】【**URL优化**】【**网页结构优化**】【**网站结构优化以及链接策略**】等等

## 关键字策略
mate标签内部的

## URL优化
img， a, link script 
 
## 网页结构优化
语义化，以及特定所搜引擎指定的结构

## 网站结构优化
### Robot协议
指定搜索引擎不能抓取的目录和文件等信息，放在根目录下，域名`/robot.txt`可访问即可

如：（表示所有的搜索引擎都不能抓取以下目录中的文件）
```
User-agent:*
Disallow:/admin/
Disallow:/facebook/
Disallow:/xiaonei/
Disallow:/51/
Disallow:/wifi/
SiteMap: http://www.hehexiao.com/sitemap.xml
```
`User-agent:*` 表示对所有的搜索引擎有效，如：`User-agent：Baiduspider`，表示百度搜索引擎不可以抓取目录的信息（百度：Baiduspider、谷歌：Googlebot）

注意：
* 即使网站上面所有的内容，都希望搜索引擎抓取到，也要设置一个空的robot文件。因为搜索引擎抓取网站时，第一个抓取的文件就是robot文件，如果这个文件不存在，搜索引擎访问时，服务器上就会有一条 404 的错误日志，多个搜索引擎抓取页面信息时，就会产生很多的 404 错误。所以，即使什么内容都不写，最好也创建一个 **robots.txt** 文件放到网站的根目录下。

* 设置不被搜索引擎抓取的文件目录，比如后台管理文件、程序脚本、附件、数据库文件、编码文件、样式表文件、模板文件、导航图片和背景图片，都是没有必要让搜索引擎抓取。当然针对不同业务的网站，需要结合自己的业务，限制搜索引擎对一些页面抓取，像一些电子商务的网站，购物车，后台管理页面，包含地址信息的页面是不能设置为可以被搜索引擎抓取的。

* 对服务器的影响：浪费我们的一些带宽资源，服务器资源

### Sitemap 站点地图协议

通过 **Sitemap** 可以让搜索引擎全面收录站点网页地址，了解站点网页地址的权重分布以及站点内容更新情况。可以是 **HTML** 或者 **XML** 格式的文件，但必须采用 **utf-8** 编码。

 **HTML** 格式就是把网站上所有访问 **URL** 罗列到一个文件内即可。这种形式不能告诉搜索引擎站点页面的权重分布，也不能告诉搜索引擎站点内容的更新情况。所以大多数支持 **Sitemap** 协议的网站都是采用 **XML** 格式进行描述， **XML** 格式的 **Sitemap** 一共用到 6 个标签，其中关键标签包括链接地址、更新时间、更新频率和索引优先权。

#### 1、Sitemap协议内容

如：
```
<urlset xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd">
	<url>
		<loc>http://www.hehexiao.com/</loc>
		<lastmod>2009-07-13T04:20-08:00</lastmod>
		<priority>1.00</priority>
		<changefreq>daily</changefreq>
	</url>
	<url>
		<loc>http://www.hehexiao.com/about.php</loc>
		<lastmod>2009-07-13T04:20-08:00</lastmod>
		<priority>0.80</priority>
		<changefreq>daily</changefreq>
	</url>
</urlset>
```
* **changefreq**：页面更新频率，`[always | hourly | daily | weekly | monthly | yearly]`，随时更新／按小时更新／按天更新／按周更新／按月更新／按年更新

* **lastmod**：页面的最后修改时间，非必填项。搜索引擎根据此项与`changefreq`相结合，判断是否要重新抓取`loc`指向的内容

* **loc**：页面永久链接地址，可以是静态页面，也可是动态页面

* **priority**：优先等级，0.0-1.0之间，一般首页1.0分，二级页面0.8，详情0.64.即使所有的页面都很重要，也不要都设置成1.0

注意：可以使用[站点生成器](http://jingyan.baidu.com/album/cd4c2979df975b756e6e60ec.html?picindex=2)，直接生成 **Sitemap** 协议

#### 2、Sitemap协议设置

站点设置 **Sitemap** 协议，通知搜索引擎的方式有两种

* 在robot中引入，注意要写绝对路径；
* 自行注册，如：可通过Google网站管理员工具，注册到Google 

**注意**：百度中，Sitemap必须命名为：sitemap_baidu.xml而不是Sitemap.xml

## 链接策略
外链等