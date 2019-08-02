`Ajax`的核心是`XMLHttpRequest`对象

使用`XMLHttpRequest`对象要注意一个兼容性问题，`XMLHttpRequest`对象只支持IE7及以上版本。

- XMLHttpRequest对象的使用
- XMLHttpRequest对象使用的一些注意事项
- XMLHttpRequest对象 2级

### XMLHttpRequest对象的使用

1、创建XMLHttpRequest对象实例
```
var xhr = new XMLHttpRequest()
```
2、使用open()方法启动一个请求以备发送
```
xhr.open('get', 'example.php', false)
```
- 第一个参数是请求类型
- 第二个参数是请求的URL
- 第三个参数是是否为异步请求
3、使用send()方法将请求划分到服务器
```
xhr.send(null)
```
- 参数为请求主体发送的数据，为必填项，当不需要发送数据时，使用null

4、收到响应后，响应的数据会自动填充XMLHttpRequest对象的属性，相关属性如下：
- responseText 作为响应主体会返回的文本
- responseXML 如果响应内容类型为'text/xml'或者'application/xml'，则该属性保存包含响应数据的XML DOM文档
- status 响应的HTTP状态
- statusText HTTP状态说明

5、在多数情况下，请求为异步的，可检测XMLHttpRequest对象的`readystate`属性来判断当前阶段：
- 0 表示未初始化，尚未调用open()方法
- 1 启动，已经调用open()方法，还未调用send()
- 2 发送，已经调用send()方法，但未收到响应
- 3 接收，收到部分响应
- 4 完成，已经收到全部的响应数据，且可以在客户端使用了

可使用`onreadyStateChange`事件监听状态变化，注意为保证兼容性，要在open方法之前使用。

6、`abort()`方法，可以在接收到响应之前，取消异步请求。调用这个方法后，XMLHttpRequest对象会停止触发事件，且不再允许访问任何与响应有关的对象属性。

7、设置自定义请求头，可使用`setRequestHeader()`方法实现，方法要写在open()方法后，send()方法之前才可以。
8、获取响应头的信息
- getResponseHeader() 参数为头部字段的名称，可获取指定头部字段的值
- getAllResponseHeaders() 获取一个包含所有头部信息的长字符串

完整的示例如下：
```
var xhr = new XMLHttpRequest()
xhr.onreadyStateChange = function () {
  if (xhr.readystate === 4) {
    if (xhr.status === 304 || (xhr.status >= 200 && xhr.status < 300)) {
      console.log('type: success, result: ', xhr.responseText)
    } else {
      console.log('type: error, errCode:', xhr.status)
    }
  }
}
xhr.open('get', 'example.php', true)
xhr.·setRequestHeader('testHeader', 'testHeaderVal')
xhr.send(null)
```

### XMLHttpRequest对象使用的一些注意事项
#### get方法
需要注意URL后面参数的名称和值都必须经过encodeURIComponent才可以

#### post方法
如果需要发送整个表单数据，需要设定content-type，并借助serialize()函数来实现

如：
```
var xhr = new XMLHttpRequest()
xhr.onreadyStateChange = function () {
  if (xhr.readystate === 4) {
    if (xhr.status === 304 || (xhr.status >= 200 && xhr.status < 300)) {
      console.log('type: success, result: ', xhr.responseText)
    } else {
      console.log('type: error, errCode:', xhr.status)
    }
  }
}
xhr.open('post', 'example.php', true)
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencolde')
var form = document.getElementById('form')
xhr.send(serialize(form))
```

### XMLHttpRequest对象 2级
#### FormData类型
- 为序列化表单以及创建与表格格式相同的数据提供便利
- 不需要再设置请求头的信息，也不需要再借助serialize()函数
- 支持的浏览器：Firfox4+ Safari5+ Chrome ANdroid3+版本的WebKit

如上post的例子，可以修改为：
```
var xhr = new XMLHttpRequest()
xhr.onreadyStateChange = function () {
  if (xhr.readystate === 4) {
    if (xhr.status === 304 || (xhr.status >= 200 && xhr.status < 300)) {
      console.log('type: success, result: ', xhr.responseText)
    } else {
      console.log('type: error, errCode:', xhr.status)
    }
  }
}
xhr.open('post', 'example.php', true)
var form = document.getElementById('form')
xhr.send(new FormData(form))
```

#### 增加timeout超时属性
- 设定请求在等待响应多少毫秒后终止，IE8及之后版本增加了该属性。
- 同时提供ontimeout的监听函数，当规定时间内未完成响应时，触发该事件。

如上post的例子，可以修改为：
```
var xhr = new XMLHttpRequest()
xhr.onreadyStateChange = function () {
  if (xhr.readystate === 4) {
    try {
      if (xhr.status === 304 || (xhr.status >= 200 && xhr.status < 300)) {
        console.log('type: success, result: ', xhr.responseText)
      } else {
        console.log('type: error, errCode:', xhr.status)
      }
    } catch () {
      console,log('增加异常捕获')
    }
  }
}
xhr.open('post', 'example.php', true)
xhr.timeout = 1000
xhr.ontimeout = function () {
  console.log('超时处理')
}
var form = document.getElementById('form')
xhr.send(new FormData(form))
```

#### 在send()方法之前，open()方法使用overrideMinmeType()方法，可以重写响应的MIME类型
#### 增加进度事件
- loadstart 接收到响应的第一个字节时触发
- progress 接收响应期间持续不断的触发
- error 请求发生错误时触发
- abort 调用abort方法而终止连接时触发
- load 接收到完整响应数据时触发
- loadend 通讯完成或者在load\abort\error后触发

注意：
- 每个请求都从触发loadstart开始，各个事件的监听写在open()方法之前
- 支持前5个事件的浏览器：Firfox3.5+ Safari4+ Chrome ANdroid版本的WebKit IOS版本的Safari
- Opera11+ IE8+ 只支持load
- 目前没有浏览器支持loadend事件
- 使用load事件时，仍然要检测status属性，才能确保数据是否真的可用
- 使用progress事件时，event对象会增加三个额外的属性： 进度信息是否可用 `lengthComputable`，接收到的字节数 `position` ，根据Content-Length响应头确定的预计字节数 `totalSize`
