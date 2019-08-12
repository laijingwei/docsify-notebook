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

## filebrowser

```bash
tar -zxvf /home/nas/go/linux-amd64-filebrowser.tar.gz -C /home/filebrowser/
cd /home/filebrowser/
./filebrowser -r / -a 0.0.0.0 -p 4000
admin/admin

https://localhost:4000/
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

> [gosuv](https://github.com/codeskyblue/gosuv)，GO语言重写的类supervisor的一个进程管理程序

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
echo "Web站点路径：$gitPath"

#判断项目路径是否存在
if [ -d "$gitPath" ]; then
  cd $gitPath
  git pull origin master
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
