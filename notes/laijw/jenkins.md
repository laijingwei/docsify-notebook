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

![添加仓库地址](../assets/162c4b63c9152782.png)

2. 安装Generic Webhook Trigger Plugin插件（系统管理-插件管理-搜索Generic Webhook Trigger Plugin）如果可选插件列表为空，点击高级标签页，替换升级站点的URL为：`http://mirror.xmission.com/jenkins/updates/update-center.json`并且点击提交和立即获取。

3. 添加触发器
第2步安装的触发器插件功能很强大，可以根据不同的触发参数触发不同的构建操作，比如我向远程仓库提交的是master分支的代码，就执行代码部署工作，我向远程仓库提交的是某个feature分支，就执行单元测试，单元测试通过后合并至dev分支。灵活性很高，可以自定义配置适合自己公司的方案，这里方便演示我们不做任何条件判断，只要有提交就触发。在任务配置里勾选Generic Webhook Trigger即可

![添加触发器](../assets/162c4c36ea15b935.png)

4. 仓库配置钩子 此处以码云为例，github的配置基本一致，进入码云项目主页后，点击管理-webhooks-添加，会跳出一个这样的框来。

![仓库配置钩子](../assets/162c4cfe042bba32.png)

URL格式为 `http://<User ID>:<API Token>@<Jenkins IP地址>:端口/generic-webhook-trigger/invoke` userid和api token在jenkins的系统管理-管理用户-admin-设置里，这是我的

![URL格式](../assets/162c4d8b530af3a0.png)

Jenkins IP地址和端口是你部署jenkins服务器的ip地址，端口号没改过的话就是8080。
密码填你和上面userid对应的密码，我这里是root。
下面的几个选项是你在仓库执行什么操作的时候触发钩子，这里默认用push。
点击提交完成配置。

5. 测试钩子

![测试钩子](../assets/162c4df2c9b49941.png)

点击测试，如果配置是成功的，你的Jenkins左侧栏构建执行状态里将会出现一个任务。

![测试钩子](../assets/162c4e3169a3c1f3.png)

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

![返回信息](../assets/162c7bb52a7713be.png)

5. 点击构建后操作，增加构建后操作步骤，选择send build artificial over SSH， 参数说明：

```
Name:选择一个你配好的ssh服务器
Source files ：写你要传输的文件路径
Remove prefix ：要去掉的前缀，不写远程服务器的目录结构将和Source files写的一致
Remote directory ：写你要部署在远程服务器的那个目录地址下，不写就是SSH Servers配置里默认远程目录
Exec command ：传输完了要执行的命令，我这里执行了解压缩和解压缩完成后删除压缩包2个命令
复制代码
```

![参数说明](../assets/162c7c7caf0713f5.png)

### 配置列表

| UserID | API Token                          |
| ------ | ---------------------------------- |
| admin  | 11c4521c7c614bc86764e1a3917028aed7 |

**GitLab Web Hook**

```json
http://admin:11c4521c7c614bc86764e1a3917028aed7@47.106.99.207:19080/generic-webhook-trigger/invoke
```

释义：`http://<User ID>:<API Token>@<Jenkins IP地址>:端口/generic-webhook-trigger/invoke`
