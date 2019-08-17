CORS跨域请求
========

何为跨域请求
------

若请求的url的协议、域名、端口中的任意一个与当前的url不同，即为跨域请求。

跨域请求使得页面体验更好，但同时也带来了安全隐患。常见的一种网络攻击叫CSRF(Cross-site request forgery)。它的攻击原理大致如下：

1.  用户访问正常网站A，诸如某银行，登录进去，A生成cookie信息并返回给用户的浏览器
2.  保持网站A的登录状态，在同一个浏览器窗口的新tab页进入恶意网站B
3.  B网站的恶意代码被执行，要求跨域请求A网站的某些资源，诸如转账功能
4.  浏览器响应该请求，在用户不知情的情况下携带cookie信息，向A发出请求
5.  网站A根据用户的cookie信息核实用户身份，处理该请求，那么来自网站B的恶意请求被执行

CORS验证机制
--------

基于CSRF等安全隐患，浏览器会限制从脚本发出的跨域请求，虽然安全性更高，页面体验却差了。于是W3C推出了一种跨域的访问验证的机制，即CORS，这种机制支持跨域请求，且跨站数据传输更安全。

CORS验证机制需要客户端和服务的协同处理。

客户端处理机制
-------

浏览器会对所有跨域请求进行验证，分为简单请求验证处理和预检请求验证处理。那么对应的就有简单请求和非简单请求之分。

简单请求

若一个请求同时满足以下两个条件，那么则为简单请求。

-   请求方法为GET或HEAD或POST
-   请求头中的Content-Type值为application/x-www-form-urlencoded 或 multipart/form-data 或 text/plain

对于简单请求，浏览器直接发送该请求，在同一个请求中作跨域验证。怎么验证呢？在请求头上附上Origin属性，表明这是一个跨域请求。服务器接到请求，根据设定的跨域规则来验证，验证通过，返回Access-Control-Allow-Origin等以Access-Control-开头的响应头以及请求的资源，否则返回403状态码，且不会返回请求的资源。

![](https://user-gold-cdn.xitu.io/2019/5/6/16a8c06a3c66b0e6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

非简单请求

不为简单请求的跨域请求均为非简单请求。

非简单请求的跨域验证通过一个预检请求来验证，即在发送一个正式的跨域请求之前，发送一个预检请求，用来检查当前网页所在的域名是否在服务器的许可名单中以及可使用哪些请求方法，请求头字段。

预检请求

-   请求方法为OPTIONS
-   请求头字段包括 Origin, Access-Control-Request-Method(表明正式的跨域请求可能用到的方法)，Access-Control-Request-Headers(表明正式的跨域请求可能用到的头字段)

若预检请求通过验证，则响应字段里会包含如下字段：

> Access-Control-Allow-Origin：值为请求头中的origin值或*\
>\
> Access-Control-Allow-Methods: 表明可被支持的请求方法\
>\
> Access-Control-Allow-Headers: 表明可被支持的头信息字段\
>\
> Access-Control-Allow-Credentials: 当请求要求携带证书信息（例如cookie,授权信息等）验证，服务器端是否允许携带\
>\
> Access-Control-Max-Age: 本次预检请求的有效期，单位为秒

若预检请求没通过验证，则响应字段里不会包含以Access-Control-开头的响应字段，且不会发送正式的跨域请求

![](https://user-gold-cdn.xitu.io/2019/5/6/16a8c06a7aa93c84?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

正式的跨域请求

与简单请求一样，请求头中附带Origin

![](https://user-gold-cdn.xitu.io/2019/5/6/16a8c06a3c8f01e7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

携带证书信息的请求

一般情况下，跨域请求不携带证书信息。但若请求的证书模式（credentials mode）被设为include，那么表明该请求需要携带证书信息。请求的证书模式可通过xmlHttpRequest.withCredentials = true设置或调用fetch([url],{mode:"include"})实现。

在简单请求及正式的非简单请求中，请求头附带证书信息，响应头回应：Access-Control-Allow-Credentials：true，并返回请求资源。

![](https://user-gold-cdn.xitu.io/2019/5/6/16a8c06a3c2d0a30?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在预检请求中，请求头并不会附带证书，响应头会回应：Access-Control-Allow-Credentials:true。

![](https://user-gold-cdn.xitu.io/2019/5/6/16a8c06a3c9151e5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

有一点需注意：若服务器端同意请求携带信息，则Access-Control-Allow-Origin不能为*，只能为请求头中指定的Origin值。

服务器端机制
------

1.  检查http头部是否有Origin字段
2.  没有或不允许，则当作普通请求处理，结束
3.  若有且允许跨源，再看是否是预检请求（method为OPTIONS）
4.  是预检请求，返回Access-Control-Allow-Origin，Access-Control-Allow-Methods等信息，内容为空
5.  不是预检请求，返回Access-Control-Allow-Origin，Access-Control-Allow-Credentials等信息，内容为请求的资源。


客户端代理机制
-------

## Vue 服务器 Nginx 代理

> [Nginx 配置](/notes/laijw/linux?id=nginx)

```bash
# 跨域设置
	location ^~ /api/{
    	proxy_pass http://a582.mxnt.net/api/;
        proxy_cookie_path /api/ /;
        proxy_pass_header Set-Cookie;
        proxy_set_header Host a582.mxnt.net;
    }
```

## Vue 服务器 Apache 代理

> 可通过宝塔面板配置

```bash
#PROXY-START/api
	<IfModule mod_proxy.c>
	    ProxyRequests Off
	    SSLProxyEngine on
	    ProxyPass /api http://api.comeally.com/
	    ProxyPassReverse /api http://api.comeally.com/
    </IfModule>
	#PROXY-END/api
```

## Vue 本地 Node.js 代理

> config/index.js

```js
    proxyTable: {
      '/api2/': {
        target: 'http://a554.mxnt.net/',
        changeOrigin: true,
        logLevel: 'debug',
        pathRewrite: {
          '^/api2': ''
        }
      }
    },

    // Various Dev Server settings
    host: '0.0.0.0', // can be overwritten by process.env.HOST
    port: 8080, // can be overwritten by process.env.PORT, if port is in use, a free one will be determined
```

##  Vue History Nginx 重定向

```bash
# History 重定向
  location / {
    try_files $uri $uri/ /index.html;
    error_page  403  /index.html;
  }
```

## Node.js 反向代理

```bash
# 跨域设置
  location /
  {
      proxy_pass http://120.25.80.86:19751;
      proxy_pass_header Set-Cookie;
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header REMOTE-HOST $remote_addr;
      proxy_redirect off;
  }
  
  # 静态资源
  location ~ .*\.(js|css|jpg|png)$
  {
      proxy_pass http://120.25.80.86:19751;
  }
```
