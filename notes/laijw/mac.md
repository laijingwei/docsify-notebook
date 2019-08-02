# Mac 开发环境搭建

## 安装准备

VMware Workstation Pro v15.0.0
Unlocker v3.0.0
MacOS Mojave 10.14

## 安装 VMware

安装VMware Workstation Pro

关闭VMware ，打开任务管理器，并找到后台进程，右键-结束所有VMware的进程

![][image1]

找到解锁工具，右键-以管理员身份运行win-install.cmd,脚本运行完毕会自动关闭

![][image2]

## 创建虚拟机

打开VMware，创建新的虚拟机，这次我选择“典型”

![][image3]

安装来源是macOS Mojave 10.14懒人版文件，注意浏览的时候文件类型要选择所有文件

系统类型是MAC OS 10.14,如果没有以上的解锁操作，选项里是没有MAC OS可选的

由于安装后系统文件会很大，我们要把默认的位置换成c盘以外的位置

## 安装 MacOS

以下的几步默认即可，如果后续觉得配置不够，可以自行调整，配置完毕，不要急着打开虚拟机，找到刚才虚拟机系统文件路径下的macOS 10.14.vmx，用记事本打开，在 smc.present = "TRUE" 后添加（smc.version = "0"）(建议您复制，不包括括号) 后保存

![][image4]
![][image5]

打开虚拟机，等待进度条加载完毕

![][image6]

语言选择简体中文，同意条款，继续安装

![][image7]

到这一步点击上方“实用工具”里的磁盘工具

![][image8]

单击左侧的vmware虚拟硬盘，然后找到上方的“编辑”-“抹掉”，名称随便

![][image9]

关闭磁盘工具，右侧会多出我们刚才分出来的一个磁盘，选择这个磁盘并继续
待安装完成，国家选择中国，键盘选择简体中文，不传输信息，apple id稍后设置，创建用户名和密码

![][image10]

## 联网

右键我的电脑，点击“管理”，找到“服务”项

![][image11]

查看服务中的VMWare NAT Sevise以及VMnetDHCP服务是否启动，如果没启动，启动即可

![][image12]

## 安装 vmware tools

全部设置完毕即可进入系统，首先推出安装磁盘，然后在vmware上方“虚拟机”选择安装vmware tools，安装完vmware tools重启系统即可实现全屏和文件共享功能（如果提示系统扩展被阻挡，请在偏好设置—安全与隐私中选择允许再次安装

![][image13]

## 与主机共享文件

点击设置，选中虚拟机设置中的选项–共享文件夹，把右侧总是启用勾上

![][image14]

进入mac系统，然后打开顶部的finder，选择偏好设置。在finder偏好设置窗口选在边栏，找到设备里面的XX的mac

![][image15]

关闭finder偏好设置窗口，打开finder，在左侧找到设备下的 xx的mac并点击。在右侧中找到 VMware shared folders（这个就是与主机共享文件存放的地方）

![][image16]

## Homebrew

Command Line Tools 选择

![][image17]

```bash
# 安装
xcode-select --install

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 更换清华大学镜像源
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
brew update

# 安装 nodejs
brew install node
brew install watchman

# 安装 yarn
brew install yarn
```

## 快捷键

![][image18]

| 按键               | 名称        |
| ------------------ | ----------- |
| <kbd>&#8984;</kbd> | Command     |
| <kbd>&#8963;</kbd> | Control     |
| <kbd>&#8997;</kbd> | Option, Alt |
| <kbd>&#8679;</kbd> | Shift       |

| 快捷键                                                   | 功能                   |
| -------------------------------------------------------- | ---------------------- |
| <kbd>&#8984;</kbd> + <kbd>M</kbd>                        | 将目前使用的窗口最小化 |
| <kbd>&#8984;</kbd> + <kbd>Q</kbd>                        | 关闭当前应用程序       |
| <kbd>&#8984;</kbd> + <kbd>W</kbd>                        | 将当前窗口关闭         |
| <kbd>&#8984;</kbd> + <kbd>I</kbd>                        | 常规信息               |
| <kbd>&#8984;</kbd> + <kbd>&#9003;</kbd>                  | 移到废纸篓             |
| <kbd>&#8984;</kbd> + <kbd>Shift</kbd> + <kbd>3</kbd>     | 截图(当前屏幕)         |
| <kbd>&#8984;</kbd> + <kbd>Shift</kbd> + <kbd>4</kbd>     | 截图(自由选取范围)     |
| <kbd>&#8984;</kbd> + <kbd>&#8997;</kbd> + <kbd>Esc</kbd> | 强行退出死机程序       |

## Terminal 命令

```bash
# Finder 打开目录
open .

```

## React Native 开发环境

```bash
# 中国镜像
npm config set registry https://registry.npm.taobao.org --global
npm config set disturl https://npm.taobao.org/dist --global
yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global

# 脚手架
yarn global add react-native-cli

# 初始化项目
react-native init MyApp --version 0.44.3

cd MyApp
react-native run-ios
```

## 虚拟机扩容

虚拟机--->设置--->硬盘

![][image19]

打开之后，界面如下图，修改“最大硬盘大小”即可（这里的最大硬盘大小是包括之前的硬盘大小），修改完成后点击扩展即可

![][image20]

开启虚拟机，打开“磁盘工具”（Finder--->应用程序--->实用工具或者可以通过Launchpad查找），选择“分区”，如下图，修改"大小"，然后点击应用，等待分区完成即可

![][image21]

## hosts

打开终端（应用程序——实用工具），运行：

```bash
sudo vi /etc/hosts

0.0.0.0 account.jetbrains.com
```
![][image22]

屏幕上会提示你输入密码（输入密码的时候不会有任何字符显示，甚至*都不会显示，输完之后按回车就是了），打开 hosts 文件之后按 i 键进入插入模式（可理解为编辑模式，如下图所示，会有「INSERT 」提示，即可插入编辑的意思），然后按照你的需要对该文件进行编辑，编辑完成之后按 ESC 键退出插入模式，之后按「 :wq+回车」保存退出，记得英文的冒号也是要输入的哦。

![][image23]

## WebStorm 重置配置

关闭WebStorm

```bash
cd ~/Library/Preferences/

rm -rf WebStorm2018.3
# WebStormXX 根据版本定。查看该文件夹全拼的办法。

ls | grep -i WebStorm
```
找到该文件夹的名字后执行第三步操作。完成之后重启 webstorm。所有的配置全部还原了。



## Quasar IOS 打包步骤

### 准备

* 在 window 端将 Quasar 项目代码上传 git


* 进入 mac 端，在 WWW 文件夹下打开 cmd，运行如下命令

```bash
sh ok.sh
```

![][image24]

* 选择项目编号并选择操作

![][image25]

### 编译

* 等待项目自动构建，构建完再次`sh ok.sh`并选择操作`2: 用 Xcode 打开文件夹`，进如项目后首先将`Automatically manage signing`选项取消选择，再勾选
* 然后选择 Team

![][image26]

### 打包

* 选择`IOS simulators`点击`Generic IOS Device`

![][image27]

* 点击三星彩，选择`Edit Scheme`

![][image28]

* 修改`Build Configuration`为`Release`

![][image29]

* 选择菜单栏`Archive`，开始构建`IPA`

![][image30]

### 导出

* 点击`Distribute App`

![][image31]

* 选择`Development`

![][image32]

* 下一步

![][image33]

* 下一步

![][image34]

* 点击`Export`

![][image35]

* 选择导出的文件夹，默认桌面

![][image36]


[image1]: ../assets/2019-02-15-23-12-28.png
[image2]: ../assets/2019-02-15-23-12-57.png
[image3]: ../assets/2019-02-15-23-13-28.png
[image4]: ../assets/2019-02-15-23-17-09.png
[image5]: ../assets/2019-02-15-23-17-16.png
[image6]: ../assets/2019-02-15-23-17-41.png
[image7]: ../assets/2019-02-15-23-17-56.png
[image8]: ../assets/2019-02-15-23-18-06.png
[image9]: ../assets/2019-02-15-23-18-17.png
[image10]: ../assets/2019-02-15-23-18-39.png
[image11]: ../assets/2019-02-15-23-20-15.png
[image12]: ../assets/2019-02-15-23-20-21.png
[image13]: ../assets/2019-02-15-23-20-01.png
[image14]: ../assets/2019-02-15-23-21-25.png
[image15]: ../assets/2019-02-15-23-21-31.png
[image16]: ../assets/2019-02-15-23-21-37.png
[image17]: ../assets/2019-02-15-23-21-17.png
[image18]: ../assets/2019-02-13-21-57-10.png
[image19]: ../assets/2019-02-15-23-20-37.png
[image20]: ../assets/2019-02-15-23-20-49.png
[image21]: ../assets/2019-02-15-23-20-59.png
[image22]: ../assets/2019-02-16-20-54-48.png
[image23]: ../assets/2019-02-16-20-55-19.png
[image24]: ../assets/2019-05-19-11.30.19.png
[image25]: ../assets/2019-05-19-11.31.09.png
[image26]: ../assets/2019-05-19-10.52.06.png
[image27]: ../assets/2019-05-19-10.53.35.png
[image28]: ../assets/2019-05-19-10.55.10.png
[image29]: ../assets/2019-05-19-10.55.34.png
[image30]: ../assets/2019-05-19-10.56.26.png
[image31]: ../assets/2019-05-19-10.58.32.png
[image32]: ../assets/2019-05-19-10.59.01.png
[image33]: ../assets/2019-05-19-10.59.23.png
[image34]: ../assets/2019-05-19-10.59.43.png
[image35]: ../assets/2019-05-19-11.00.00.png
[image36]: ../assets/2019-05-19-11.00.14.png
