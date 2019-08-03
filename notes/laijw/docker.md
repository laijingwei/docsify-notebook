# Docker

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
