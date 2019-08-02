# 服务器

## Chrome

```js
chrome://about
chrome://serviceworker-internals
```

[微信开发者调试](http://debugtbs.qq.com/)

## 微擎 FTP 路径

```bash
/data/wwwroot/a554.mxnt.net/addons/ewei_shopv2/core/mobile/member
```

## SSH

```bash
# putty
-pw Aa86536@@ root@120.79.2.244
 
#  ssh
ssh root@192.168.1.100

# 554 部署
cd /www/wwwroot/a554m.mxnt.net
git pull origin master
```

## yum

```bash
# yum 中国镜像
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo

curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -

## Run `sudo yum install -y nodejs` to install Node.js 10.x and npm.
yum install -y nodejs

## You may also need development tools to build native addons:
yum install -y gcc-c++ make

## To install the Yarn package manager, run:
curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
yum install -y yarn

yum install -y git
yum install -y tree
tree -L 1
```

## OneinStack

```bash
# 安装命令
wget -c http://mirrors.linuxeye.com/oneinstack-full.tar.gz && tar xzf oneinstack-full.tar.gz && ./oneinstack/install.sh --nginx_option 1

# Nginx目录
cd /data/wwwroot

# OneinStack安装目录
cd /root/oneinstack

# Nginx 虚拟主机配置
cd /usr/local/nginx/conf/vhost

# Nginx SSL证书 
cd /usr/local/nginx/conf/ssl
```

## Rust tools

```bash
yum install -y rust cargo

# bat
cargo install bat
ln -s /root/.cargo/bin/bat /bin/bat

# fd
cargo install fd-find
ln -s /root/.cargo/bin/fd /bin/fd

# lsd
cargo install lsd
ln -s /root/.cargo/bin/lsd /bin/lsd
```

## Docker

> Docker 要求 CentOS 系统的内核版本高于 3.10 ，查看本页面的前提条件来验证你的CentOS 版本是否支持 Docker 。

通过 uname -r 命令查看你当前的内核版本

```bash
uname -r
```

安装一些必要的系统工具

```bash
yum install -y yum-utils device-mapper-persistent-data lvm2
```

添加软件源信息：

```bash
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

更新 yum 缓存：

```bash
yum makecache fast
```

安装 Docker-ce：

```bash
yum -y install docker-ce
```

启动 Docker 后台服务

```bash
systemctl start docker
```

中国镜像

```bash
cd /etc/docker
touch daemon.json
vim daemon.json

# 粘贴以下内容
{
  "registry-mirrors": ["http://hub-mirror.c.163.com"]
}
```

启动 [PlantUML Server](https://github.com/plantuml/plantuml-server)

```bash
docker run -d -p 8080:8080 plantuml/plantuml-server:jetty
```

启动 [Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/)

```bash
docker run -it --rm -p 4000:80 dockerpracticecn/docker_practice
```

> [Docker 命令大全](http://www.runoob.com/docker/docker-command-manual.html)
> 
> [Docker — 从入门到实践](https://yeasy.gitbooks.io/docker_practice/content/)


## Cent OS 常用命令

```bash
# 查看系统版本
cat /etc/redhat-release
uname -a

# 树形显示目录
tree -L 1 -C

# 查看内存排行
top
# 按 shift + M

# 从 '/' 开始进入根文件系统搜索文件和目录
find / -name file1

# YUM 软件包升级器
yum install ..
yum update ..
yum remove ..
yum search ..
```

## CURL

> Usage: curl [options...] <url>

```bash
# RESTful API

curl -X GET http://localhost:1337/test
curl -X POST http://localhost:1337/test -d "name=hello" -d "password=123456"
curl -X PATCH http://localhost:1337/test/5cb8338cf4b67d3718ae62f9 -d "name=hello" -d "password=123456"
curl -X DELETE http://localhost:1337/test?id=5cb8338cf4b67d3718ae62f9
```

## wget

> wget [参数列表] [目标软件、网页的网址] 

```bash
-V,–version 显示软件版本号然后退出； 
-h,–help显示软件帮助信息； 
-e,–execute=COMMAND 执行一个 “.wgetrc”命令 

-o,–output-file=FILE 将软件输出信息保存到文件； 
-a,–append-output=FILE将软件输出信息追加到文件； 
-d,–debug显示输出信息； 
-q,–quiet 不显示输出信息； 
-i,–input-file=FILE 从文件中取得URL； 

-t,–tries=NUMBER 是否下载次数（0表示无穷次） 
-O –output-document=FILE下载文件保存为别的文件名 
-nc, –no-clobber 不要覆盖已经存在的文件 
-N,–timestamping只下载比本地新的文件 
-T,–timeout=SECONDS 设置超时时间 
-Y,–proxy=on/off 关闭代理 

-nd,–no-directories 不建立目录 
-x,–force-directories 强制建立目录 

–http-user=USER设置HTTP用户 
–http-passwd=PASS设置HTTP密码 
–proxy-user=USER设置代理用户 
–proxy-passwd=PASS设置代理密码 

-r,–recursive 下载整个网站、目录（小心使用） 
-l,–level=NUMBER 下载层次 

-A,–accept=LIST 可以接受的文件类型 
-R,–reject=LIST拒绝接受的文件类型 
-D,–domains=LIST可以接受的域名 
–exclude-domains=LIST拒绝的域名 
-L,–relative 下载关联链接 
–follow-ftp 只下载FTP链接 
-H,–span-hosts 可以下载外面的主机 
-I,–include-directories=LIST允许的目录 
-X,–exclude-directories=LIST 拒绝的目录 
```

* 使用wget下载单个文件

```bash
wget http://cn.wordpress.org/wordpress-3.1-zh_CN.zip 
```

* 使用wget -O下载并以不同的文件名保存

```bash
wget -O wordpress.zip http://www.centos.bz/download.php?id=1080
```

* 使用wget -c断点续传

```bash
wget -c http://cn.wordpress.org/wordpress-3.1-zh_CN.zip
```

* 使用wget -b后台下载

```bash
wget -b http://cn.wordpress.org/wordpress-3.1-zh_CN.zip
```

* 使用wget -i下载多个文件
首先，保存一份下载链接文件

```bash
cat > filelist.txt
url1
url2
url3
url4
```

* 接着使用这个文件和参数-i下载

wget -i filelist.txt 

* 使用wget FTP下载
你可以使用wget来完成ftp链接的下载。
使用wget匿名ftp下载

```bash
wget ftp-url
```

使用wget用户名和密码认证的ftp下载

```bash
wget –ftp-user=USERNAME –ftp-password=PASSWORD url
```

## Nginx

### Nginx 配置文件

```bash
# 宝塔 nginx 配置文件
/etc/nginx/nginx.conf

# 宝塔 nginx 站点配置文件
/www/server/panel/vhost/nginx

# 重启服务
service nginx restart
systemctl restart nginx
nginx -t
nginx -s reload
```

### Nginx 反向代理

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

## 公共DNS
```bash
# 阿里云
223.5.5.5
223.6.6.6

# Google
8.8.8.8
8.8.4.4
```

## 服务器常见端口

| 端口  | 进程     |
| ----- | -------- |
| 21    | ftp      |
| 22    | ssh      |
| 23    | telnet   |
| 80    | http     |
| 443   | https    |
| 1433  | ms-sql-s |
| 2000  | hotel    |
| 3306  | mysql    |
| 3389  | mstsc    |
| 5900  | vnc      |
| 6379  | redis    |
| 8080  | webcache |
| 8888  | bt-panel |
| 27017 | mongo    |

## Vagrant

Vagrant是一款用来构建虚拟开发环境的外挂工具，可以简化虚拟机配置和管理。它底层支持VirtualBox、VMware、AWS等，非常适合使用php/python/ruby/java语言开发web应用，“代码在我机子上运行没有问题”这种说辞将成为历史。

> [官方文档](https://www.vagrantup.com/docs/cli/box.html)
> 
> [官方 box 镜像](https://app.vagrantup.com/boxes/search)

### Vagrant命令详解

| 命令                  | 作用                                                                   |
| --------------------- | ---------------------------------------------------------------------- |
| vagrant box add       | 添加box的操作                                                          |
| vagrant init          | 初始化box的操作，会生成vagrant的配置文件Vagrantfile                    |
| vagrant up            | 启动本地环境                                                           |
| vagrant ssh           | 通过ssh登录本地环境所在虚拟机                                          |
| vagrant halt          | 关闭本地环境                                                           |
| vagrant suspend       | 暂停本地环境                                                           |
| vagrant resume        | 恢复本地环境                                                           |
| vagrant reload        | 修改了Vagrantfile后，使之生效（相当于先 halt，再 up）                  |
| vagrant destroy       | 彻底移除本地环境                                                       |
| vagrant box list      | 显示当前已经添加的box列表                                              |
| vagrant box remove    | 删除相应的box                                                          |
| vagrant package       | 打包命令，可以把当前的运行的虚拟机环境进行打包                         |
| vagrant plugin        | 用于安装卸载插件                                                       |
| vagrant status        | 获取当前虚拟机的状态                                                   |
| vagrant global-status | 显示当前用户Vagrant的所有环境状态                                      |
| vagrant rsync-auto    | [自动同步映射目录](https://www.vagrantup.com/docs/cli/rsync-auto.html) |

> [Cent OS 7 box 下载地址](https://cloud.centos.org/centos/7/vagrant/x86_64/images/CentOS-7-x86_64-Vagrant-1902_01.VirtualBox.box)
>
> 局域网镜像`\\192.168.1.100\nas\iso\Vagrant`

### 步骤

### 离线安装

```bash
# 安装centos7 box
vagrant box add centos/7 ./CentOS-7-x86_64-Vagrant-1902_01.VirtualBox.box

# 初始化镜像
vagrant init centos/7

# 创建目录
mkdir Vagrant
cd Vagrant

# 启动系统
vagrant up

# SSH连接安装的虚拟机
vagrant ssh

# 打包分发
vagrant halt
vagrant status
vagrant package default --output  centos7.box  --vagrantfile Vagrantfile
```

### 在线安装

```bash
# ubuntu
vagrant init ubuntu/xenial64

# homestead
vagrant init laravel/homestead

# centos
vagrant init centos/7
```

### 服务器部署

#### 在CentOS 7上安装VirtualBox 5.1

尽管在www.howtoing.com上有几个关于安装virtualBox的教程（例如， [在CentOS 7上安装VirtualBox](https://www.howtoing.com/install-virtualbox-on-redhat-centos-fedora/) ），但是，我将很快通过virtualbox 5.1安装。

首先安装VirtualBox依赖项。

```bash
yum -y install gcc dkms make qt libgomp patch
yum -y install kernel-headers kernel-devel binutils glibc-headers glibc-devel font-forge
```

接下来添加VirtualBox库。

```bash
cd /etc/yum.repo.d/
wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
```

现在安装和构建内核模块。

```bash
yum install -y VirtualBox-5.1
/sbin/rcvboxdrv setup
```

#### 在CentOS 7上安装Vagrant

在这里，我们将使用[yum命令](https://www.howtoing.com/20-linux-yum-yellowdog-updater-modified-commands-for-package-mangement/)下载并安装Vagrant的最新版本（即在编写时为1.9.6）。

```bash
yum -y install https://releases.hashicorp.com/vagrant/1.9.6/vagrant_1.9.6_x86_64.rpm
```

创建一个目录，您将要安装您最喜欢的Linux发行版或操作系统。

```bash
mkdir ~/vagrant-home
cd ~/vagrant-home
```

安装您最喜欢的发行版或操作系统。

```bash
vagrant init ubuntu/xenial64
vagrant init centos/7
```

将在当前目录中创建一个名为**Vagrantfile**的文件。 此文件包含虚拟机的配置设置。


启动您的Ubuntu服务器。

`vagrant up`

等待下载完成。 这真的不需要太多时间。 你的互联网速度也算了。

有关可用的预配置框的列表，请访问<https://app.vagrantup.com/boxes/search>

#### 使用Virtualbox管理Vagrant Boxes

启动Virtualbox可以在Vagrantfile中定义的配置中查看预装的64位Ubuntu虚拟机加载到虚拟机中。 这就像任何其他VM：没有区别。

[![VirtualBox](https://www.howtoing.com/wp-content/uploads/2017/07/virtualbox.png)](https://www.howtoing.com/wp-content/uploads/2017/07/virtualbox.png)

如果要设置另一个框（例如**CentOS7** ），请使用您最喜爱的编辑器修改当前目录中的**Vagrantfile**文件（如果是Vagrantfile所在）。 我用[vi编辑](https://www.howtoing.com/vi-editor-usage/)我的工作。 紧接在第15行下方，输入：

```bash
config.vm.box =  "centos/7"
```

您还可以在Vagrantfile中设置尚未下载的框的IP地址以及主机名。 您可以为尽可能多地设置的框来执行此操作。

要设置静态IP地址，请取消注释第35行，并将IP地址更改为您的选择。

```bash
config.vm.network "private_network", ip:  "192.168.33.10"
```

[![Vagrantfile配置](https://www.howtoing.com/wp-content/uploads/2017/07/Vagrantfile-Configuration.png)](https://www.howtoing.com/wp-content/uploads/2017/07/Vagrantfile-Configuration.png)

完成此修改后，请输入以下命令以启动机器。

`vagrant up`

管理这个虚拟服务器是非常容易的。

`vagrant halt`


## Jenkins

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


## Samba

```bash
# 查询是否已经安装了Samba
rpm -qi samba

# 安装Samba
yum install -y samba

# 查看已经安装好的Samba的信息
rpm -qi samba

# 新建分享目录
mkdir /home/nas && chmod -R 777 /home/nas

# 备份配置文件
cp /etc/samba/smb.conf /etc/samba/smb.conf.bak

# 修改配置文件
vim /etc/samba/smb.conf

## [homes]、[printers]、[print$]都注释掉只保留[global]，load printers = no
[share]
comment = share
path = /home/share
public = yes
writable = yes
browseable = yes
available = yes
guest ok = yes

# 启动命令
systemctl start smb
systemctl status smb
systemctl enable smb
systemctl disable smb
systemctl stop smb
```


## 防火墙

```bash
# 防火墙放行端口
firewall-cmd --permanent --add-port=139/tcp
firewall-cmd --permanent --add-port=445/tcp

# 关闭防火墙
systemctl status firewalld
systemctl stop firewalld
systemctl disable firewalld
```

## Hugo

```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.55.6/hugo_0.55.6_Linux-64bit.tar.gz
tar -zxvf ./hugo_0.55.6_Linux-64bit.tar.gz
cp ./hugo /usr/local/bin/
```

## Gogs

```bash
adduser git
su git
cd ~
tar -zxvf /home/nas/zip/gogs_linux_amd64.tar.gz -C /home/git

https://localhost:3000/
```

## bandzip

```bash
# 压缩
bc a -fmt:zip hello .

# 解压
bc x hello.zip
```

## Termux

[Github](https://github.com/termux/termux-app)

```bash
# 连接远程仓库，获取软件包信息
$ apt update

# 更新本地已经安装的软件包
$ apt upgrade

# 安装 sl 软件包
$ apt install sl

# 运行
$ sl

# 访问本机存储
$ termux-setup-storage

# 安装软件包
$ pkg install [package name]

# 卸载软件包
$ pkg uninstall [package name]

# 列出所有软件包
$ pkg list-all

# 安装常用软件
$ pkg install nodejs
$ pkg install git
```

## chmod

```bash
mv /home/nas/docute-notebook /www/wwwroot
mv /home/nas/go/img/* /www/wwwroot/hugo-blog/static/assets/

# 权限
chmod -R 755 docute-notebook

# 用户
chown -R www docute-notebook

# 用户组
chgrp -R www docute-notebook
```

## code-server

### 安装

[下载地址](https://github.com/cdr/code-server/releases)

```bash
cd /home
wget https://github.com/cdr/code-server/releases/download/1.1156-vsc1.33.1/code-server1.1156-vsc1.33.1-linux-x64.tar.gz
tar -xvf code-server1.1156-vsc1.33.1-linux-x64.tar.gz
mv code-server1.1156-vsc1.33.1-linux-x64 code-server
cd code-server
```

### lib64

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

> GO语言重写的类supervisor的一个进程管理程序

```bash
# 安装
curl https://raw.githubusercontent.com/codeskyblue/gosuv/master/get.sh | bash

# 启动
gosuv start-server

http://localhost:11313/
```

## webhook

> [Github](https://github.com/adnanh/webhook)

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

## 宝塔 Webhook

> Gogs + 宝塔 Webhook

### sh 脚本

```bash
#!/bin/bash
echo ""

#输出当前时间
date --date='0 days ago' "+%Y-%m-%d %H:%M:%S"
echo "Start"

#判断宝塔WebHook参数是否存在
if [ ! -n "$1" ];
then 
  echo "param参数错误"
  echo "End"
  exit
fi

#git项目路径
gitPath="/home/nas/www/$1"

#git 网址
gitHttp="http://192.168.1.100:3000/laijw/$1.git"

echo "Web站点路径：$gitPath"

#判断项目路径是否存在
if [ -d "$gitPath" ]; then
  cd $gitPath

  #判断是否存在git目录
  if [ ! -d ".git" ]; then
    echo "在该目录下克隆 git"
    git clone $gitHttp gittemp
    mv gittemp/.git .
    rm -rf gittemp
  fi

  #拉取最新的项目文件
  git reset --hard origin/master
  git pull
  
  #设置目录权限
  chown -R www:www $gitPath
  echo "End"
  exit
else
  echo "该项目路径不存在"
  echo "End"
  exit
fi
```

### 生成钩子

```bash
http://192.168.1.100:8888/hook?access_key=iDO5X0LNRhMNn68v7e7StZGVCjigTxqQ1Lebkz7fBLZmLULS&param=sdsf-guide
```

!> 新增钩子后记得重启宝塔面板

## oh-my-zsh

### 安装

```bash
yum update && yum -y install zsh

sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 配置文件
vim ~/.zshrc

plugins=(
  git
  npm
  yarn
  bower
  yarn
  yum
)

# 查看shell列表
cat /etc/shells

# 切换shell为zsh
chsh -s /bin/zsh
```

### Aliases

| Alias     | Command                                              | Description                                                     |
| --------- | ---------------------------------------------------- | --------------------------------------------------------------- |
| ys        | `yum search`                                         | Search package                                                  |
| yp        | `yum info`                                           | Show package info                                               |
| yl        | `yum list`                                           | List packages                                                   |
| ygl       | `yum grouplist`                                      | List package groups                                             |
| yli       | `yum list installed`                                 | Print all installed packages                                    |
| ymc       | `yum makecache`                                      | Rebuild the yum package list                                    |
| yu        | `sudo yum update`                                    | Upgrade packages                                                |
| yi        | `sudo yum install`                                   | Install package                                                 |
| ygi       | `sudo yum groupinstall`                              | Install package group                                           |
| yr        | `sudo yum remove`                                    | Remove package                                                  |
| ygr       | `sudo yum groupremove`                               | Remove pagage group                                             |
| yrl       | `sudo yum remove --remove-leaves`                    | Remove package and leaves                                       |
| yc        | `sudo yum clean all`                                 | Clean yum cache                                                 |
| gaa       | git add --all                                        |                                                                 |
| gcmsg     | git commit -m                                        |                                                                 |
| gp        | git push                                             |                                                                 |
| ggpush    | git push origin "$(git_current_branch)"              |                                                                 |
| gpsup     | git push --set-upstream origin $(git_current_branch) |                                                                 |
| gst       | git status                                           |                                                                 |
| gl        | git pull                                             |                                                                 |
| ggl       | git pull origin $(current_branch)                    |                                                                 |
| gpristine | git reset --hard && git clean -dfx                   |                                                                 |
| y         | `yarn`                                               | The Yarn command                                                |
| ya        | `yarn add`                                           | Install a package in dependencies (`package.json`)              |
| yad       | `yarn add --dev`                                     | Install a package in devDependencies (`package.json`)           |
| yap       | `yarn add --peer`                                    | Install a package in peerDependencies (`package.json`)          |
| yb        | `yarn build`                                         | Run the build script defined in `package.json`                  |
| ycc       | `yarn cache clean`                                   | Clean yarn's global cache of packages                           |
| yga       | `yarn global add`                                    | Install packages globally on your operating system              |
| ygls      | `yarn global list`                                   | Lists global installed packages                                 |
| ygrm      | `yarn global remove`                                 | Remove global installed packages from your OS                   |
| ygu       | `yarn global upgrade`                                | Upgrade packages installed globally to their latest version     |
| yh        | `yarn help`                                          | Show help for a yarn command                                    |
| yi        | `yarn init`                                          | Interactively creates or updates a package.json file            |
| yin       | `yarn install`                                       | Install dependencies defined in `package.json`                  |
| yls       | `yarn list`                                          | List installed packages                                         |
| yout      | `yarn outdated`                                      | Check for outdated package dependencies                         |
| yp        | `yarn pack`                                          | Create a compressed gzip archive of package dependencies        |
| yrm       | `yarn remove`                                        | Remove installed packages                                       |
| yrun      | `yarn run`                                           | Run a defined package script                                    |
| ys        | `yarn serve`                                         | Start the dev server                                            |
| yst       | `yarn start`                                         | Run the start script defined in `package.json`                  |
| yt        | `yarn test`                                          | Run the test script defined in `package.json`                   |
| yuc       | `yarn global upgrade && yarn cache clean`            | Upgrade global packages and clean yarn's global cache           |
| yui       | `yarn upgrade-interactive`                           | Prompt for which outdated packages to upgrade                   |
| yup       | `yarn upgrade`                                       | Upgrade packages to their latest version                        |
| `npmg`    | `npm i -g`                                           | Install dependencies globally                                   |
| `npmS`    | `npm i -S`                                           | Install and save to dependencies in your package.json           |
| `npmD`    | `npm i -D`                                           | Install and save to dev-dependencies in your package.json       |
| `npmE`    | `PATH="$(npm bin)":"$PATH"`                          | Run command from node_modules folder based on current directory |
| `npmO`    | `npm outdated`                                       | Check which npm modules are outdated                            |
| `npmV`    | `npm -v`                                             | Check package versions                                          |
| `npmL`    | `npm list`                                           | List installed packages                                         |
| `npmL0`   | `npm ls --depth=0`                                   | List top-level installed packages                               |
| `npmst`   | `npm start`                                          | Run npm start                                                   |
| `npmt`    | `npm test`                                           | Run npm test                                                    |
| `npmR`    | `npm run`                                            | Run npm scripts                                                 |
| `npmP`    | `npm publish`                                        | Run npm publish                                                 |
| `npmI`    | `npm init`                                           | Run npm init                                                    |
| bi        | `bower install`                                      | Installs the project dependencies listed in bower.json          |
| bl        | `bower list`                                         | List local packages and possible updates                        |
| bs        | `bower search`                                       | Finds all packages or a specific package.                       |


### Commands

| Command               | Description                                                                                                                  |
| :-------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
| _tabs_                | Create a new tab in the current directory (macOS - requires enabling access for assistive devices under System Preferences). |
| _take_                | Create a new directory and change to it, will create intermediate directories as required.                                   |
| _x_ / _extract_       | Extract an archive (supported types: tar.{bz2,gz,xz,lzma}, bz2, rar, gz, tar, tbz2, tgz, zip, Z, 7z).                        |
| _zsh_stats_           | Get a list of the top 20 commands and how many times they have been run.                                                     |
| _uninstall_oh_my_zsh_ | Uninstall Oh-my-zsh.                                                                                                         |
| _upgrade_oh_my_zsh_   | Upgrade Oh-my-zsh.                                                                                                           |
| source ~/.zshrc       | Uptake new changes                                                                                                           |

---

| Alias   | Command                               |
| :------ | :------------------------------------ |
| _alias_ | list all aliases                      |
| ..      | cd ..                                 |
| ...     | cd ../..                              |
| ....    | cd ../../..                           |
| .....   | cd ../../../..                        |
| /       | cd /                                  |
| ~       | cd ~                                  |
| _cd +n_ | switch to directory number `n`        |
| _1_     | cd -                                  |
| _2_     | cd -2                                 |
| _3_     | cd -3                                 |
| _4_     | cd -4                                 |
| _5_     | cd -5                                 |
| _6_     | cd -6                                 |
| _7_     | cd -7                                 |
| _8_     | cd -8                                 |
| _9_     | cd -9                                 |
| _md_    | mkdir -p                              |
| _rd_    | rmdir                                 |
| _d_     | dirs -v (lists last used directories) |

See `~/.oh-my-zsh/lib/directories.zsh`