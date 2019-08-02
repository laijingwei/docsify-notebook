`Ajax`的核心是`XMLHttpRequest`对象

- [XMLHttpRequest对象](https://github.com/junruchen/junruchen.github.io/wiki/JS-XMLHttpRequest)
- 跨域资源共享问题
- Ajax的扩展Comet
- SSE
- [与服务器进行全双工、双向通讯的信道---Web Sockets](https://github.com/junruchen/junruchen.github.io/wiki/JS-WebSockets)

### 跨域资源共享问题
通过XMLHttpRequest实现Ajax通讯有一个主要限制，来源于跨域安全策略。默认情况下，只能访问同一个域中的资源。

#### 方案一 CORS 跨源资源共享
是W3C的一个工作草案，定一个在比如访问跨源资源时，服务器与浏览器如何沟通

基本思想：使用自定义HTTP头，让浏览器与服务器进行沟通，从而决定请求或响应是否应该成功。

下面是一段兼容浏览器的CORS代码，支持IE10+
```
function createCORSRequest(method, url) {
  var xhr = new XMLHttpRequest()
  if ('withCredentials' in xhr) { // Firfox3.5+ Safari4+ Chrome IE10+
    xhr.open(method, url, true)
  } else if (typeof xDomainRequest !== 'undefined') { // IE8
    xhr = new xDomainRequest()
    xhr.open(method, url)
  } else {
    return null
  }
  return xhr
}
```

#### 方案二 图片
如：
```
var img = new Image()
img.onload = img.onerror = function () {
  console.log('Done')
}
img.src = 'http://example.com?name=test'
```

缺点：
- 只能是get请求
- 单向通信，不能访问服务器的响应文本
- 容易被浏览器缓存

#### 方案三 JSONP
(JSON width padding) (填充式JSON、参数式JSON)，与JSON类似，是被包含在函数调用中的JSON，目前很少会用了。

由两部分组成，毁掉函数和数据，需要借助script标签实现，如：
```
function handleResponse (res) {
  console.log(res)
}
var script = document.createElement('script')
script.src = 'http://example.com?callback=handleResponse'
document.body.insertBefore(script, document.body.firstChild)
```

- 与图片方式相比较，优点是可以获取响应数据
- 缺点1：是在其他域中执行，有可能加带恶意代码
- 缺点2：确定JSONP是否失败困难，可使用window.onerror方法，但需要注意兼容性问题
- 缺点3：只能发送get请求

#### 方案四 [Web Sockets](https://github.com/junruchen/junruchen.github.io/wiki/JS-WebSockets)

### Ajax的扩展Comet
Ajax是一种从页面向服务器请求数据的技术，Comet是一种服务器向页面推送数据的技术，能够让信息近乎实时的被推送到页面上。

实现Comet方式：`长轮询`，`流`
#### 长轮询
类似与短轮询的翻版。页面发起一个到服务器的请求，然后服务器一直保持连接打开，知道有数据可以发送。发送完数据之后，浏览器关闭连接，之后又发送一个到服务器的新的请求。这个持续的过程就是长轮询。

无论是短轮询还是长轮询，都要先发起对浏览器的连接。两者最大的区别是服务器如何发送数据。短轮询是服务器立即响应，而长轮询则是等待发送响应。

轮询的优势是所有的浏览器都可以实现，使用XHR与setTimeout()就可以实现

#### HTTP流
与轮询不同，整个过程只是用一个HTTP连接。浏览器向服务器发送一个请求，而服务器保持连接代开，然后周期性的向浏览器发送数据。实际上就是后端进行轮询。

在Firfox Safari Chrome Opera中，可以通过监听readyStateChange事件并检测readyState的值是否为3，就可以实现HTTP流。
- 当readyState为3时，说明收到新的数据，但是仍未结束，此时可以记录上一次的位置，来获取最新的数据。
- 当readyState为4时，表示结束

如：
```
function createStreamingClient(url, progress, finished) {
  var xhr = new XMLHttpRequest(), received = 0
  xhr.open('get', url, true)
  xhr.onreadyStateChange = function () {
    var result;
    if (xhr.readyState === 3) {
      result = xhr.responseText.substring(received)
      received += result.length
      progress(result)
    } else if (xhr.readyState === 4) {
      finished(xhr.responseText)
    }
  }
  return xhr
}

var client = createStreamingClient('example.php', function(data){
  console.log('progress', data)
}, function(data){
  console.log('Done', data)
})
```

### SSE(Server-Sent Events 服务器发送事件)
SSE API用于创建到服务器的单向连接，服务器通过这个连接可以发送任意数量的数据。支持短轮询、长轮询、HTTP流。

服务器响应的MIME必须是`text/event-stram`

#### 使用
1、创建新的EventSource对象
```
var source = new EventSource('example.php')
```
EventSource实例有一个readyState属性：
- 0 正在连接服务器
- 1 连接打开
- 2 连接关闭

提供三个事件
- open 在建立连接时触发
- message 在接触到新事件时触发，存在event对象，返回的数据以文本的形式存在event.data中
- error无法建立连接时触发

如：
```
source.onmessage = function (event) {
  console.log(event.data)
}
```

当断开连接时，会自动重新连接。

使用`close()` 可以立即断开连接且不能重新连接