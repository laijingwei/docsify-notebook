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

## Web 研发模式的演变

### 简单明快的早期时代
![](../assets/63918611gw1efj2vqv7htj20f20ajta4.jpg)

### 后端为主的 MVC 时代
![](../assets/63918611gw1efj2vset36j20f009stad.jpg)

### Ajax 带来的 SPA 时代
![](../assets/63918611gw1efj2vtkiivj20ey0aj0ue.jpg)

### 前端为主的 MVVM（Model-View-ViewModel） 时代
![](../assets/63918611gw1efj2vu7wcvj20f00agdhq.jpg)
![](../assets/63918611gw1efj2vv9crfj20f10amabl.jpg)

### Node 带来的全栈时代
![](../assets/63918611gw1efj2vvjwtfj20ge0gzab9.jpg)


> - [前后分离接口规范](https://www.jianshu.com/p/c81008b68350?from=timeline)
> - [Web 开发模式的演变](http://blog.jobbole.com/65509/)


## Chrome

```js
chrome://about
chrome://serviceworker-internals
```

[微信开发者调试](http://debugtbs.qq.com/)
