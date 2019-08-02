# 开始 & 安装

### Node (CommonJS)

```shell
# 安装
npm install mockjs
```
   
```js
// 使用 Mock
var Mock = require('mockjs')
var data = Mock.mock({
    // 属性 list 的值是一个数组，其中含有 1 到 10 个元素
    'list|1-10': [{
        // 属性 id 是一个自增数，起始值为 1，每次增 1
        'id|+1': 1
    }]
})
// 输出结果
console.log(JSON.stringify(data, null, 4))
```

### Bower

<!-- If you'd like to use [bower](http://bower.io/), it's as easy as: -->

```shell
# 安装
npm install -g bower
bower install --save mockjs
```

```html    
<script type="text/javascript" src="./bower_components/mockjs/dist/mock.js"></script>
```

### RequireJS (AMD)

```js
// 配置 Mock 路径
require.config({
    paths: {
        mock: 'http://mockjs.com/dist/mock'
    }
})
// 加载 Mock
require(['mock'], function(Mock){
    // 使用 Mock
    var data = Mock.mock({
        'list|1-10': [{
            'id|+1': 1
        }]
    })
    // 输出结果
    document.body.innerHTML +=
        '<pre>' +
        JSON.stringify(data, null, 4) +
        '</pre>'
})
```
```js
// ==>
{
    "list": [
        {
            "id": 1
        },
        {
            "id": 2
        },
        {
            "id": 3
        }
    ]
}
```

[JSFiddle](http://jsfiddle.net/nzcsxd76/)

### Sea.js (CMD)

因为 Sea.js 社区尚未提供 webpack 插件，所以 Mock.js 暂**不完整**支持通过 Sea.js 加载。

一种变通的方式是，依然通过 Sea.js 配置和加载 Mock.js，然后访问全局变量 Mock。

```js
// 配置 Mock 路径
seajs.config({
    alias: {
        mock: 'http://mockjs.com/dist/mock.js'
    }
})

// 加载 Mock
seajs.use('mock', function(__PLACEHOLDER) {
    // 使用 Mock（全局变量）
    var data = Mock.mock({
        'list|1-10': [{
            'id|+1': 1
        }]
    });
    document.body.innerHTML +=
        '<pre>' +
        JSON.stringify(data, null, 4) +
        '</pre>'
})
```

[JSFiddle](http://jsfiddle.net/3za48nwd/1/)


### KISSY

```js
// 配置 Mock 路径
KISSY.config({
    packages: {
        mock: {
            base: 'http://mockjs.com/dist/'
        }
    }
})
// 加载 Mock
KISSY.use(['node', 'mock'], function (S, _, Mock) {
    // 使用 Mock
    var data = Mock.mock({
        'list|1-10': [{
            'id|+1': 1
        }]
    })
    // 输出结果
    KISSY.all('<pre>').text(JSON.stringify(data, null, 4))
        .appendTo('body')
})
```

[JSFiddle](http://jsfiddle.net/En2sX/2/)


### Random CLI

```shell
# 全局安装
$ npm install mockjs -g

# 执行
$ random url
# => http://rmcpx.org/funzwc

# 帮助
random -h
```