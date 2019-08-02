[Web Sockets封装案例](https://github.com/junruchen/junruchen.github.io/tree/master/dailyPractice/business/websocket)

Web Sockets的目标：在一个单独的持续连接上提供全双工、双向通信

Web Sockets使用自定义的协议，与http一样，是应用层的协议

好处是：
- 能够在客户端、服务端发送非常少量的数据，不必担心`HTTP字节级`的开销
- 传递数据包小，更适用于移动端，对于移动端，带宽和网络延迟是一个关键问题

`坏处是：制定协议的时间比制定JS API的时间都长`

与HTTP的不同之处：
- http只能由客户端发起，而webSocket是双向的
- webSocket传输的数据包相对于http而言很小，很适合移动端使用
- 没有同源限制，可以跨域共享资源

支持的浏览器：Firfox6+ Safari5+ Chrome IOS 4+版本的Safari

### 使用
1、创建WebSockets实例
```
var ws = new WebSockets('ws://example.com')
```
需要注意的是：
- URL的模式：`ws://`，加密情况下为：`wss://`
- 必须是绝对URL，也就是完整的URL

2、创建实例后，会立即尝试连接，与XMLHttpRequest类似，存在一个readyState属性表示当前状态。
- WebSocket.OPENING(0) 正在建立连接
- WebSocket.OPEN(1) 已经建立连接
- WebSocket.CLOSEING(2) 正在关闭连接
- WebSocket.CLOSE(3) 已经关闭连接

3、发送数据与接收数据
使用send()方法发送数据，接收到的数据时会触发message事件
```
ws.send('hello')
ws.onmessage = function (event) {
  console.log(event.data)
}
```
注意：
- send发送数据时，数据必须是纯文本的格式
- message返回的数据也是字符串的格式
- WebSocket对象不支持DOM2级事件侦听器，必须使用DOM0级 对每个事件分别处理

其他事件
- open 成功建立连接时触发
- error 发生错误时触发，连接不能继续
- close 连接关闭时触发，只要close的event对象有格外的信息
  - wasClean 是否明确关闭
  - code 服务器返回的数值状态码
  - reason 字符串，包含服务端返回的信息



