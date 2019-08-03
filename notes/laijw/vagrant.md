# Vagrant

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
