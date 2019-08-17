# Go 开发者路线图

## 安装

[下载地址](https://golang.org/dl/)

局域网安装包`\\192.168.1.100\nas\exe`

[Go 资源大全中文版](github/awesome/awesome-go-cn)

## Hugo

### docdock

```bash
hugo new site blog
cd blog
git init
git submodule add https://github.com/vjeantet/hugo-theme-docdock.git themes/docdock
git submodule init
git submodule update
cp themes/docdock/exampleSite/config.toml .

hugo new post/hello.md
hugo server -D
```

###  ananke

```bash
hugo new site blog
cd blog/themes
git clone https://github.com/budparr/gohugo-theme-ananke.git
copy themes\gohugo-theme-ananke\exampleSite\config.toml .

hugo new post/hello.md
hugo server -D
```


## Code Server

> [Code Server](https://github.com/cdr/code-server/releases)，在线版本的 VS Code

### 安装

```bash
cd /home
wget https://github.com/cdr/code-server/releases/download/1.1156-vsc1.33.1/code-server1.1156-vsc1.33.1-linux-x64.tar.gz
tar -xvf code-server1.1156-vsc1.33.1-linux-x64.tar.gz
mv code-server1.1156-vsc1.33.1-linux-x64 code-server
cd code-server
```

### lib64

> code-server 依赖的 C++ 编译器

```bash

cd /home

# 此处我的安装路径为 /home/lib64
wget https://adbin.top/packages/lib64.tar.gz
tar -xvf lib64.tar.gz

cd /usr/lib64
cp libstdc++.so.6 libstdc++.so.6.bak
rm libstdc++.so.6

# ln -s (对应路径)/libstdc++.so.6.0.25（对应版本即可，gcc8.2.0带的是libstdc++.so.6.0.25） libstdc++.so.6
ln -s /home/lib64/libstdc++.so.6.0.25 libstdc++.so.6

# 赋予权限
chmod -R 777 ./code-server
```

### 启动

```bash

# 启动目录
./code-server /www/wwwroot/a805/front/ --no-auth

https://localhost:8443/

# 字体配置
Consolas, ‘Courier New’, monospace
```


## gosuv

> [gosuv](https://github.com/codeskyblue/gosuv)，GO语言重写的类supervisor的一个进程管理程序

```bash
# 安装
curl https://raw.githubusercontent.com/codeskyblue/gosuv/master/get.sh | bash

# 启动
gosuv start-server

http://localhost:11313/
```

## webhook

> [webhook](https://github.com/adnanh/webhook)，使用 Go 语言写的 webhook

```bash
./webhook -hooks hooks.json -port 8444 -hotreload -verbose
```

**hooks.json**

```json
[
  {
    "id": "test",
    "execute-command": "/home/webhook/redeploy.sh",
    "command-working-directory": "/home/webhook",
    "response-message": "I got the payload!"
  }
]
```


## Hugo

> [Hugo](https://github.com/gohugoio/hugo)，基于 Go 的博客编译器

```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.55.6/hugo_0.55.6_Linux-64bit.tar.gz
tar -zxvf ./hugo_0.55.6_Linux-64bit.tar.gz
cp ./hugo /usr/local/bin/
```

## Gogs

> [Gogs](https://github.com/gogs/gogs)，基于 Go 的 Git 服务器，类似项目有 [Gitee](https://github.com/go-gitea/gitea)

```bash
adduser git
su git
cd ~
tar -zxvf /home/nas/zip/gogs_linux_amd64.tar.gz -C /home/git

https://localhost:3000/
```

## FRP

> [FRP](https://github.com/fatedier/frp)，内网穿透工具，类似项目有 [NPS](https://github.com/cnlh/nps)

```bash
# 服务端启动 frps
./frps -c ./frps.ini

# 客户端启动 frpc
./frpc -c ./frpc.ini
```

## Annie

> [Annie](https://github.com/iawia002/annie)，视频下载工具

```bash
annie -F list.txt
```

## File Browser

> [File Browser](https://github.com/filebrowser/filebrowser)，基于 Go 的开源网盘

```bash
tar -zxvf /home/nas/go/linux-amd64-filebrowser.tar.gz -C /home/filebrowser/
cd /home/filebrowser/
./filebrowser -r / -a 0.0.0.0 -p 4000
admin/admin

https://localhost:4000/
```

## bandzip

> 开源解压软件

```bash
# 压缩
bc a -fmt:zip hello .

# 解压
bc x hello.zip
```



## 路线图

![Roadmap](../assets/golang-developer-roadmap-zh-CN.png)

## 资源

1. 先决条件

   - [Go](https://golangbot.com/)
   - [SQL](https://www.w3schools.com/sql/default.asp)

2. 通用开发技能

   - 学习 GIT，在 GitHub 上建立一些仓库，与其它人分享你的代码
   - 了解 HTTP(S) 协议，request 方法（GET, POST, PUT, PATCH, DELETE, OPTIONS）
   - 不要害怕使用 Google，[Google 搜索的力量](http://www.powersearchingwithgoogle.com/)
   - 看一些和数据结构以及算法有关的书籍
   - 学习关于认证的基础实现
   - 面向对象原则等等

3. 命令行工具
   1. [cobra](https://github.com/spf13/cobra)
   2. [urfave/cli](https://github.com/urfave/cli)

4. 网页框架 + 路由

   1. [Echo](https://github.com/labstack/echo)
   2. [Beego](https://github.com/astaxie/beego)
   3. [Gin](https://github.com/gin-gonic/gin)
   4. [Revel](https://github.com/revel/revel)
   5. [Chi](https://github.com/go-chi/chi)

5. 数据库

   1. 关系型
      1. [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-2017)
      2. [PostgreSQL](https://www.postgresql.org/)
      3. [MariaDB](https://mariadb.org/)
      4. [MySQL](https://www.mysql.com/)
      5. [CockroachDB](https://www.cockroachlabs.com/)
   2. 云数据库
      - [CosmosDB](https://docs.microsoft.com/en-us/azure/cosmos-db)
      - [DynamoDB](https://aws.amazon.com/dynamodb/)
   3. 搜索引擎
      - [ElasticSearch](https://www.elastic.co/)
      - [Solr](http://lucene.apache.org/solr/)
      - [Sphinx](http://sphinxsearch.com/)
   4. NoSQL
      - [MongoDB](https://www.mongodb.com/)
      - [Redis](https://redis.io/)
      - [Apache Cassandra](http://cassandra.apache.org/)
      - [LiteDB](https://github.com/mbdavid/LiteDB)
      - [RavenDB](https://github.com/ravendb/ravendb)
      - [CouchDB](http://couchdb.apache.org/)

6. 对象关系映射框架

   1. [Gorm](https://github.com/jinzhu/gorm)
   2. [Xorm](https://github.com/go-xorm/xorm)

7. 高速缓存

   1. [GCache](https://github.com/bluele/gcache)
   2. 分布式缓存
      1. [Go-Redis](https://github.com/go-redis/redis)
      2. [GoMemcached](https://github.com/bradfitz/gomemcache)

8. 日志

   1. 日志框架
      - [Zap](https://github.com/uber-go/zap)
      - [ZeroLog](https://github.com/rs/zerolog)
      - [Logrus](https://github.com/sirupsen/logrus)
   2. 日志管理系统
      - [Sentry.io](http://sentry.io)
      - [Loggly.com](https://loggly.com)

9. 实时通讯
   1. [Socket.IO](https://socket.io/)

10. API 客户端

    1. REST
       - [Gentleman](https://github.com/h2non/gentleman)
       - [GRequests](https://github.com/kennethreitz/grequests)
       - [heimdall](https://github.com/heimdal/heimdal)
    2. [GraphQL](https://graphql.org/)
       - [gqlgen](https://github.com/99designs/gqlgen)
       - [graphql-go](https://github.com/graph-gophers/graphql-go)

11. 最好知道

    - [Validator](https://github.com/chriso/validator.js/)
    - [Glow](https://github.com/pytorch/glow)
    - [GJson](https://github.com/tidwall/gjson)
    - [Authboss](https://github.com/volatiletech/authboss)
    - [Go-Underscore](https://github.com/ahl5esoft/golang-underscore)

12. 测试

    1. 单元，行为，集成测试
       1. [GoMock](https://github.com/golang/mock)
       2. [Testify](https://github.com/stretchr/testify)
       3. [GinkGo](https://github.com/onsi/ginkgo)
       4. [GoMega](https://github.com/onsi/gomega)
       5. [GoCheck](https://github.com/go-check/check)
       6. [GoDog](https://github.com/DATA-DOG/godog)
       7. [GoConvey](https://github.com/smartystreets/goconvey)
    2. 端对端测试
       - [Selenium](https://github.com/tebeka/selenium)
       - [Endly](https://github.com/viant/endly)

13. 任务调度

    - [Gron](https://github.com/roylee0704/gron)
    - [JobRunner](https://github.com/bamzi/jobrunner)

14. 微服务

    1. 消息代理
       - [RabbitMQ](https://www.rabbitmq.com/tutorials/tutorial-one-go.html)
       - [Apache Kafka](https://kafka.apache.org/)
       - [ActiveMQ](https://github.com/apache/activemq)
       - [Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview)
    2. 消息总线
       - [Message-Bus](https://github.com/vardius/message-bus)
    3. 框架
         - [GoKit](https://github.com/go-kit/kit)
         - [Micro](https://github.com/micro/go-micro)
         - [rpcx](https://github.com/smallnest/rpcx)
    4. RPC
         - [Protocol Buffers](https://github.com/protocolbuffers/protobuf)
         - [gRPC-Go](https://github.com/grpc/grpc-go)
         - [gRPC-Gateway](https://github.com/grpc-ecosystem/grpc-gateway)

15. [Go-模式](https://github.com/tmrts/go-patterns)

## 备忘录

```go
/*******************************************************************************
 * Golang CHEATSHEET (中文速查表)  -  by chlins (created on 2018/02/14)
 * Version: 3, Last Modified: 2018/03/07 19:51
 * https://github.com/skywind3000/awesome-cheatsheets
 ******************************************************************************/



 /******************************************************************************
  * Go 编译器命令
  *****************************************************************************/
go command [arguments]                              // go 命令 [参数]
go build                                            // 编译包和依赖包
go clean                                            // 移除对象和缓存文件
go doc                                              // 显示包的文档
go env                                              // 打印go的环境变量信息
go bug                                              // 报告bug
go fix                                              // 更新包使用新的api
go fmt                                              // 格式规范化代码
go generate                                         // 通过处理资源生成go文件
go get                                              // 下载并安装包及其依赖
go install                                          // 编译和安装包及其依赖
go list                                             // 列出所有包
go run                                              // 编译和运行go程序
go test                                             // 测试
go tool                                             // 运行给定的go工具
go version                                          // 显示go当前版本
go vet                                              // 发现代码中可能的错误



/*******************************************************************************
 * Hello World
 ******************************************************************************/
// main.go
package main                                        // 包名

import "fmt"                                        // 导入fmt包

func main() {                                       // 主函数
    fmt.Println("Hello World")                      // 打印输出
}
// go run main.go                                   // 直接运行
// go build && ./main                               // 先编译成二进制文件再运行



/*******************************************************************************
 * 操作符
 ******************************************************************************/
// 算数操作符
+ - * / %                                           // 加 减 乘 除 取余
& | ^ &^                                            // 位与 位或 位异或 位与非
<< >>                                               // 左移 右移
// 比较操作
== !=                                               // 等于 不等于
< <=                                                // 小于 小于等于
> >=                                                // 大于 大于等于
// 逻辑操作
&& || !                                             // 逻辑与 逻辑或 逻辑非
// 其他
& * <-                                              // 地址 指针引用 通道操作



/*******************************************************************************
 * 声明
 ******************************************************************************/
a := 1                                              // 直接给一个未声明的变量赋值
var b int                                           // var 变量名 数据类型 来声明
var c float64
// 注意：使用var声明过的变量不可再使用 := 赋值
a = 2
const d = 1                                         // 常量




/*******************************************************************************
 * 数据类型
 ******************************************************************************/
s := "hello"                                       // 字符
a := 1                                             // int
b := 1.2                                           // float64
c := 1 + 5i                                        // complex128
// 数组
arr1 := [3]int{4, 5, 6}                           // 手动指定长度
arr2 := [...]int{1, 2, 3}                         // 由golang自动计算长度
// 切片
sliceInt := []int{1, 2}                           // 不指定长度
sliceByte := []byte("hello")
// 指针
a := 1
point := &a                                      // 将a的地址赋给point


/*******************************************************************************
 * 流程控制
 ******************************************************************************/
// for
i := 10
for i > 0 {
    println(i--)
}
// if else
if i == 10 {
    println("i == 10")
} else {
    println("i != 10")
}
// switch
switch i {
case 10:
    println("i == 10")
default:
    println("i != 10")
}


/*******************************************************************************
 * 函数
 ******************************************************************************/
// 以func关键字声明
func test() {}

f := func() {println("Lambdas function")}     // 匿名函数
f()

func get() (a,b string) {                    // 函数多返回值
    return "a", "b"
}
a, b := get()




/*******************************************************************************
 * 结构体
 ******************************************************************************/
// golang中没有class只有struct
type People struct {
  Age int                                  // 大写开头的变量在包外可以访问
  name string                              // 小写开头的变量仅可在本包内访问
}
p1 := People{25, "Kaven"}                 // 必须按照结构体内部定义的顺序
p2 := People{name: "Kaven", age: 25}      // 若不按顺序则需要指定字段

// 也可以先不赋值
p3 := new(People)
p3.Age = 25
p3.name = "Kaven"


/*******************************************************************************
 * 方法
 ******************************************************************************/
// 方法通常是针对一个结构体来说的
type Foo struct {
  a int
}
                                        // 值接收者
func (f Foo) test() {
  f.a = 1                              // 不会改变原来的值
}
                                      // 指针接收者
func (f *Foo) test() {
  f.a = 1                            // 会改变原值
}



/*******************************************************************************
 * go 协程
 ******************************************************************************/
go func() {
    time.Sleep(10 * time.Second)
    println("hello")
}()                                // 不会阻塞代码的运行 代码会直接向下运行
// channel 通道
c := make(chan int)
// 两个协程间可以通过chan通信
go func() {c <- 1}()              // 此时c会被阻塞 直到值被取走前都不可在塞入新值
go func() {println(<-c)}()
// 带缓存的channel
bc := make(chan int, 2)
go func() {c <- 1; c <-2}()      // c中可以存储声明时所定义的缓存大小的数据，这里是2个
go func() {println(<-c)}()



/*******************************************************************************
 * 接口
 ******************************************************************************/
// go的接口为鸭子类型，即只要你实现了接口中的方法就实现了该接口
type Reader interface {
    Reading()                  // 仅需实现Reading方法就实现了该接口
}

type As struct {}
func (a As) Reading() {}      // 实现了Reader接口

type Bs struct {}
func (b Bs) Reading() {}      // 也实现了Reader接口
func (b Bs) Closing() {}




/*******************************************************************************
 * 一些推荐
 ******************************************************************************/
// 入门书籍
《Go学习笔记》                // 雨痕的
《Go语言实战》                // 强烈推荐
// 网上资料
https://github.com/astaxie/build-web-application-with-golang    // 谢大的
https://github.com/Unknwon/the-way-to-go_ZH_CN                  // 无闻
https://github.com/Unknwon/go-fundamental-programming           // 无闻教学视频
// 第三方类库
https://golanglibs.com/
// 大杂烩
https://github.com/avelino/awesome-go



/*******************************************************************************
 * References
 ******************************************************************************/
https://github.com/a8m/go-lang-cheat-sheet
https://github.com/LeCoupa/awesome-cheatsheets
```