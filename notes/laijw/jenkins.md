# Jenkins

Jenkins 是一款业界流行的开源持续集成工具，广泛用于项目开发，具有自动化构建、测试和部署等功能。只需要在本地发起一个git提交，剩下的单元测试，打包构建，代码部署，邮件提醒等功能全部自动化完成，让持续集成、持续交付、持续部署变得简单易操作，真正解决人工构建部署的诸多问题。

### 安装

请先确保已安装 java

1. 安装JDK

```bash
yum install -y java
```

2. 安装jenkins

添加Jenkins库到yum库，Jenkins将从这里下载安装。

```bash
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
yum install -y jenkins
```

3. 配置jenkis的端口

```bash
vi /etc/sysconfig/jenkins
```

找到修改端口号：

`JENKINS_PORT="8080"`

4. 启动 jenkins

`service jenkins start/stop/restart`

- 安装成功后Jenkins将作为一个守护进程随系统启动
- 系统会创建一个"jenkins"用户来允许这个服务，如果改变服务所有者，同时需要修改/var/log/jenkins, /var/lib/jenkins, 和/var/cache/jenkins的所有者
- 启动的时候将从/etc/sysconfig/jenkins获取配置参数
- 默认情况下，Jenkins运行在8080端口，在浏览器中直接访问该端进行服务配置
- Jenkins的RPM仓库配置被加到/etc/yum.repos.d/jenkins.repo
- 初始密码在：/var/lib/jenkins/secrets/initialAdminPassword

### Generic Webhook Trigger

首先我们要实现一个git钩子功能，就是我们向github/码云等远程仓库push我们的代码时，jenkins能知道我们提交了代码，这是自动构建自动部署的前提，钩子的实现原理是在远端仓库上配置一个Jenkins服务器的接口地址，当本地向远端仓库发起push时，远端仓库会向配置的Jenkins服务器的接口地址发起一个带参数的请求，jenkins收到后开始工作。

1. 打开刚创建的任务，选择配置，添加远程仓库地址，配置登录名及密码及分支。

![添加仓库地址]http://static.mxnt.net/img/162c4b63c9152782.png)

2. 安装Generic Webhook Trigger Plugin插件（系统管理-插件管理-搜索Generic Webhook Trigger Plugin）如果可选插件列表为空，点击高级标签页，替换升级站点的URL为：`http://mirror.xmission.com/jenkins/updates/update-center.json`并且点击提交和立即获取。

3. 添加触发器
第2步安装的触发器插件功能很强大，可以根据不同的触发参数触发不同的构建操作，比如我向远程仓库提交的是master分支的代码，就执行代码部署工作，我向远程仓库提交的是某个feature分支，就执行单元测试，单元测试通过后合并至dev分支。灵活性很高，可以自定义配置适合自己公司的方案，这里方便演示我们不做任何条件判断，只要有提交就触发。在任务配置里勾选Generic Webhook Trigger即可

![添加触发器]http://static.mxnt.net/img/162c4c36ea15b935.png)

4. 仓库配置钩子 此处以码云为例，github的配置基本一致，进入码云项目主页后，点击管理-webhooks-添加，会跳出一个这样的框来。

![仓库配置钩子]http://static.mxnt.net/img/162c4cfe042bba32.png)

URL格式为 `http://<User ID>:<API Token>@<Jenkins IP地址>:端口/generic-webhook-trigger/invoke` userid和api token在jenkins的系统管理-管理用户-admin-设置里，这是我的

![URL格式]http://static.mxnt.net/img/162c4d8b530af3a0.png)

Jenkins IP地址和端口是你部署jenkins服务器的ip地址，端口号没改过的话就是8080。
密码填你和上面userid对应的密码，我这里是root。
下面的几个选项是你在仓库执行什么操作的时候触发钩子，这里默认用push。
点击提交完成配置。

5. 测试钩子

![测试钩子]http://static.mxnt.net/img/162c4df2c9b49941.png)

点击测试，如果配置是成功的，你的Jenkins左侧栏构建执行状态里将会出现一个任务。

![测试钩子]http://static.mxnt.net/img/162c4e3169a3c1f3.png)

另外，你也可以试下本地提交代码，提交代码后，jenkins也会开始一个任务,目前我们没有配置任务开始后让它做什么，所以默认它只会在你提交新代码后，将新代码拉取到jenkins服务器上。到此为止，git钩子我们配置完成。

### Publish Over SSH

1. 首先，先在Jenkins上装一个插件Publish Over SSH，我们将通过这个工具实现服务器部署功能。
2. 在要部署代码的服务器上创建一个文件夹用于接收Jenkins传过来的代码，我在服务器上建了一个testjenkins的文件夹。
3. Jenkins想要往服务器上部署代码必须登录服务器才可以，这里有两种登录验证方式，一种是ssh验证，一种是密码验证，就像你自己登录你的服务器，你可以使用ssh免密登录，也可以每次输密码登录，系统管理-系统设置里找到Publish over SSH这一项。

重点参数说明：

```bash
Passphrase：密码（key的密码，没设置就是空）
Path to key：key文件（私钥）的路径
Key：将私钥复制到这个框中(path to key和key写一个即可)

SSH Servers的配置：
SSH Server Name：标识的名字（随便你取什么）
Hostname：需要连接ssh的主机名或ip地址（建议ip）
Username：用户名
Remote Directory：远程目录（上面第二步建的testjenkins文件夹的路径）

高级配置：
Use password authentication, or use a different key：勾选这个可以使用密码登录，不想配ssh的可以用这个先试试
Passphrase / Password：密码登录模式的密码
Port：端口（默认22）
Timeout (ms)：超时时间（毫秒）默认300000

```

4. 配置完成后，点击Test Configuration测试一下是否可以连接上，如果成功会返回success，失败会返回报错信息，根据报错信息改正即可。

![返回信息]http://static.mxnt.net/img/162c7bb52a7713be.png)

5. 点击构建后操作，增加构建后操作步骤，选择send build artificial over SSH， 参数说明：

```
Name:选择一个你配好的ssh服务器
Source files ：写你要传输的文件路径
Remove prefix ：要去掉的前缀，不写远程服务器的目录结构将和Source files写的一致
Remote directory ：写你要部署在远程服务器的那个目录地址下，不写就是SSH Servers配置里默认远程目录
Exec command ：传输完了要执行的命令，我这里执行了解压缩和解压缩完成后删除压缩包2个命令
复制代码
```

![参数说明]http://static.mxnt.net/img/162c7c7caf0713f5.png)

### 配置列表

| UserID | API Token                          |
| ------ | ---------------------------------- |
| admin  | 11c4521c7c614bc86764e1a3917028aed7 |

**GitLab Web Hook**

```json
http://admin:11c4521c7c614bc86764e1a3917028aed7@47.106.99.207:19080/generic-webhook-trigger/invoke
```

释义：`http://<User ID>:<API Token>@<Jenkins IP地址>:端口/generic-webhook-trigger/invoke`



# 持续集成是什么

互联网软件的开发和发布，已经形成了一套标准流程，最重要的组成部分就是持续集成（Continuous integration，简称 CI）。

本文简要介绍持续集成的概念和做法。

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015092301.png)

一、概念
----

**持续集成指的是，频繁地（一天多次）将代码集成到主干。**

它的好处主要有两个。

> **（1）快速发现错误。**每完成一点更新，就集成到主干，可以快速发现错误，定位错误也比较容易。
> 
> **（2）防止分支大幅偏离主干。**如果不是经常集成，主干又在不断更新，会导致以后集成的难度变大，甚至难以集成。

**持续集成的目的，就是让产品可以快速迭代，同时还能保持高质量。**它的核心措施是，代码集成到主干之前，必须通过自动化测试。只要有一个测试用例失败，就不能集成。

Martin Fowler 说过，"持续集成并不能消除 Bug，而是让它们非常容易发现和改正。"

与持续集成相关的，还有两个概念，分别是持续交付和持续部署。

二、持续交付
------

**持续交付（Continuous delivery）指的是，频繁地将软件的新版本，交付给质量团队或者用户，以供评审。**如果评审通过，代码就进入生产阶段。

持续交付可以看作持续集成的下一步。它强调的是，不管怎么更新，软件是随时随地可以交付的。

三、持续部署
------

**持续部署（continuous deployment）是持续交付的下一步，指的是代码通过评审以后，自动部署到生产环境。**

持续部署的目标是，代码在任何时刻都是可部署的，可以进入生产阶段。

持续部署的前提是能自动化完成测试、构建、部署等步骤。它与持续交付的区别，可以参考下图。

![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015092302.jpg)

（[图片来源](http://blog.crisp.se/2013/02/05/yassalsundman/continuous-delivery-vs-continuous-deployment)）

四、流程
----

根据持续集成的设计，代码从提交到生产，整个过程有以下几步。

### 4.1 提交

流程的第一步，是开发者向代码仓库提交代码。所有后面的步骤都始于本地代码的一次提交（commit）。

### 4.2 测试（第一轮）

代码仓库对 commit 操作配置了钩子（hook），只要提交代码或者合并进主干，就会跑自动化测试。

测试有好几种。

> *   单元测试：针对函数或模块的测试
> *   集成测试：针对整体产品的某个功能的测试，又称功能测试
> *   端对端测试：从用户界面直达数据库的全链路测试

第一轮至少要跑单元测试。

### 4.3 构建

通过第一轮测试，代码就可以合并进主干，就算可以交付了。

交付后，就先进行构建（build），再进入第二轮测试。所谓构建，指的是将源码转换为可以运行的实际代码，比如安装依赖，配置各种资源（样式表、JS 脚本、图片）等等。

常用的构建工具如下。

> *   [Jenkins](http://jenkins-ci.org/)
> *   [Travis](https://travis-ci.com/)
> *   [Codeship](https://www.codeship.io/)
> *   [Strider](http://stridercd.com/)

Jenkins 和 Strider 是开源软件，Travis 和 Codeship 对于开源项目可以免费使用。它们都会将构建和测试，在一次运行中执行完成。

### 4.4 测试（第二轮）

构建完成，就要进行第二轮测试。如果第一轮已经涵盖了所有测试内容，第二轮可以省略，当然，这时构建步骤也要移到第一轮测试前面。

第二轮是全面测试，单元测试和集成测试都会跑，有条件的话，也要做端对端测试。所有测试以自动化为主，少数无法自动化的测试用例，就要人工跑。

需要强调的是，新版本的每一个更新点都必须测试到。如果测试的覆盖率不高，进入后面的部署阶段后，很可能会出现严重的问题。

### 4.5 部署

通过了第二轮测试，当前代码就是一个可以直接部署的版本（artifact）。将这个版本的所有文件打包（ `tar filename.tar *` ）存档，发到生产服务器。

生产服务器将打包文件，解包成本地的一个目录，再将运行路径的符号链接（symlink）指向这个目录，然后重新启动应用。这方面的部署工具有 [Ansible](http://www.ansible.com/)，[Chef](https://www.chef.io/chef/)，[Puppet](https://puppetlabs.com/) 等。

### 4.6 回滚

一旦当前版本发生问题，就要回滚到上一个版本的构建结果。最简单的做法就是修改一下符号链接，指向上一个版本的目录。

五、参考链接
------

*   Gergely Nemeth, [Continuous Deployment of Node.js Applications](https://blog.risingstack.com/continuous-deployment-of-node-js-applications/)
*   Codeship, [Continuous Integration Essentials](https://codeship.com/continuous-integration-essentials)