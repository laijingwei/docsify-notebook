客户端检测是一种补救措施，也是一种行之有效的开发策略。主要用来规避或者突破不同浏览器之间的差异。

完整的判断当前引擎、浏览器、平台的检测代码，请参考[client.js](https://github.com/junruchen/junruchen.github.io/tree/master/tool/client)

#### 目录
- 能力检测
- 怪癖检测
- 用户代理检测

### 能力检测
又称特性检测。不是检测浏览器的类型，而是检测浏览器具备哪些能力。

能力检测需要注意的问题
- 1、先检测达成目的最常用的特性
- 2、检测某个或者某几个特性并不能确定浏览器，根据浏览器的不同将能力组合起来才是更可取的方式(如判断浏览器是否支持DOM1级规定的能力等)。
- 3、必须检测实际要用到的特性，即一个特性存在，不意味着另一个特性也存在，如下例子：

```
function getWindowWidth () {
  if (document.all) { // 假设IE浏览器
    return document.documentElement.clientWidth
  } else {
    return window.innerWidth
  }
}
```
上述例子中，存在的问题是：Opera同时支持`document.all`、`window.innerWidth`

### 怪癖检测
和能力检测不同，怪癖检测用来识别浏览器的特殊行为，即检测浏览器存在测缺陷。

如IE8以及更早的版本中，如果某个实例属性与`[[Enumerable]]`标记为false的某个原型属性同名，则该实例属性不会出现在`for-in`循环中。可使用以下代码检测是否存在此问题：
```
var hasDontEnumQuirk =function () {
  var o = {toString: function () {}}
  for (var key in o) {
    if (key == 'toString') {
      return false
    }
  }
  return true
}
```

另一个经常需要检测的问题，Safari3之前的版本会枚举被隐藏的属性，可使用下面代码检测该问题：
```
var hasEnumShadowsQuirk =function () {
  var o = {toString: function () {}}
  var count = 0
  for (var key in o) {
    if (key == 'toString') {
      count++
    }
  }
  return (count > 1)
}
```

### 用户代理检测
通过检测用户代理字符串来确定实际使用的浏览器。

在每一次的HTTP请求中，用户代理字符串是作为响应首部发送的，且该字符串可通过JavaScript的`navigator.userAgent`属性访问。

在客户端，用户代理检测一般被当作一种万不得已才用的做法，其优先级排在能力检测或怪癖检测之后。