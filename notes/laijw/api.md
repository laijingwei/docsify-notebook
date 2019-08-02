# 接口规范

## 开发流程

![](../assets/2062729-46838a6013bfc55d.png)

## HTTP API 协议

### RESTful

Representational State Transfer, RESTful 一组架构约束条件和原则, 在 2000 年由 Roy Fielding 提出

![](../assets/1547513768123.png)

###  GraphQL

GraphQL 是一个用于 API 的查询语言, 在 2015 年由 Facebook 开源

![](../assets/1547513768234.png)

## 规范原则

- 接口返回数据即显示：前端仅做渲染逻辑处理；
- 渲染逻辑禁止跨多个接口调用；
- 前端关注交互、渲染逻辑，尽量避免业务逻辑处理的出现；
- 请求响应传输数据格式：JSON，JSON数据尽量简单轻量，避免多级JSON的出现；

![](../assets/2062729-cbc42c9b88dd22a9.png)


## Laravel 分页名词翻译

**响应 JSON释义**

```js
{
   "total": 50, //记录总条数
   "per_page": 15, //每页显示的记录条数
   "current_page": 1, //当前页
   "last_page": 4, //总页数
   "first_page_url": "http://laravel.app?page=1",
   "last_page_url": "http://laravel.app?page=4",
   "next_page_url": "http://laravel.app?page=2",
   "prev_page_url": null,
   "path": "http://laravel.app",
   "from": 1, //当前页的第一条
   "to": 15, //当前页的最后一条
   "data":[
        {
            // Result Object
        },
        {
            // Result Object
        }
   ]
}
```

**paginate 方法**

| 方法                                                    | 描述                                                       |
| ------------------------------------------------------- | ---------------------------------------------------------- |
| $results->count()                                       | 获取当前页的项目数                                         |
| $results->currentPage()                                 | 获取当前页的页码                                           |
| $results->firstItem()                                   | 获取结果集分片中第一项的编号                               |
| $results->getOptions()                                  | 获取分页选项                                               |
| $results->getUrlRange($start, $end)	创建分页 URL 的范围 |
| $results->hasMorePages()                                | 判断是否还有足够多的项目用于分页                           |
| $results->lastItem()                                    | 获取结果集分片中最后一项的编号                             |
| $results->lastPage()                                    | 获取最后一页的页码(使用 simplePaginate 时无效)             |
| $results->nextPageUrl()                                 | 获取下一页的 URL                                           |
| $results->onFirstPage()                                 | 判断是否在第一页                                           |
| $results->perPage()                                     | 每页显示的项目数                                           |
| $results->previousPageUrl()                             | 获取上一页的 URL                                           |
| $results->total()                                       | 判断存储器中匹配的所有项目总数(使用 simplePaginate 时无效) |
| $results->url($page)                                    | 获取给定页码的分页 URL                                     |


## 请求基本格式

### GET请求

```
xxx/login?body={"username":"admin","password":"123456","captcha":"scfd","rememberMe":1}
```

### POST请求

![](../assets/2062729-9fe293e81fba56a2.png)

## 响应格式

### 响应基本格式

```js
{
    code: 200,
    data: {
        message: "success"
    }
}
```
### 响应实体格式

```js
{
    code: 200,
    data: {
        message: "success",
        entity: {
            id: 1,
            name: "XXX",
            code: "XXX"
        }
    }
}
```
> data.entity: 响应返回的实体数据

### 响应列表格式

```js
{
    code: 200,
    data: {
        message: "success",
        list: [
            {
                id: 1,
                name: "XXX",
                code: "XXX"
            },
            {
                id: 2,
                name: "XXX",
                code: "XXX"
            }
        ]
    }
}
```
> data.list: 响应返回的列表数据

### 响应分页格式
```js
{
    code: 200,
    data: {
        recordCount: 2,
        message: "success",
        totalCount: 2,
        pageNo: 1,
        pageSize: 10,
        list: [
            {
                id: 1,
                name: "XXX",
                code: "H001"
            },
            {
                id: 2,
                name: "XXX",
                code: "H001"
            } ],
        totalPage: 1
    }
}
```
> - data.recordCount: 当前页记录数
> - data.totalCount: 总记录数
> - data.pageNo: 当前页码
> - data.pageSize: 每页大小
> - data.totalPage: 总页数

### 下拉框、复选框、单选框
```js
{
    code: 200,
    data: {
        message: "success",
        list: [{
            id: 1,
            name: "XXX",
            code: "XXX",
            isSelect: 1
        }, {
            id: 1,
            name: "XXX",
            code: "XXX",
            isSelect: 0
        }]
    }
}
```


## 接口错误状态码

![](../assets/2019-02-23-09-04-20.png)

### 前端接收错误状态码

```js
  if (err && err.response) {
    switch (err.response.status) {
      case 400:
        err.message = '错误请求'
        break
      case 401:
        err.message = '未授权，请重新登录'
        break
      case 403:
        err.message = '拒绝访问'
        break
      case 404:
        err.message = '请求错误,未找到该资源'
        break
      case 405:
        err.message = '请求方法未允许'
        break
      case 408:
        err.message = '请求超时'
        break
      case 500:
        err.message = '服务器端出错'
        break
      case 501:
        err.message = '网络未实现'
        break
      case 502:
        err.message = '网络错误'
        break
      case 503:
        err.message = '服务不可用'
        break
      case 504:
        err.message = '网络超时'
        break
      case 505:
        err.message = 'http版本不支持该请求'
        break
      default:
        err.message = `连接错误${err.response.status}`
    }
  } else {
    err.message = '连接服务器失败'
  }
```
