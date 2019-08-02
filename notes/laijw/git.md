# Git 简介

> [Git 使用简易指南](http://www.bootcss.com/p/git-guide/)

- Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。
- Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。
- Git 与常用的版本控制工具 CVS, Subversion 等不同，它采用了分布式版本库的方式，不必服务器端软件支持。


## Git 与 SVN 区别

- GIT是分布式的，SVN不是：这是GIT和其它非分布式的版本控制系统，例如SVN，CVS等，最核心的区别。
- GIT把内容按元数据方式存储，而SVN是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn,.cvs等的文件夹里。
- GIT分支和SVN的分支不同：分支在SVN中一点不特别，就是版本库中的另外的一个目录。
- GIT没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比GIT缺少的最大的一个特征。
- GIT的内容完整性要优于SVN：GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。


## Gitlab

```
/etc/gitlab

# 以下为阿里云企业邮箱的配置

gitlab_rails['gitlab_email_from'] = 'git@wlizm.com'
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtpdm.aliyun.com"
gitlab_rails['smtp_port'] = 80
gitlab_rails['smtp_user_name'] = "git@wlizm.com"
gitlab_rails['smtp_password'] = "Sdsf2018git"
gitlab_rails['smtp_domain'] = "wlizm.com"
gitlab_rails['smtp_authentication'] = "login"
```

## Git 命令


```bash
# 创建版本库
git clone <url>                          //克隆远程版本库
git init                                 //初始化本地版本库

# 修改和提交
git status                               //查看状态
git diff                                 //查看变更内容
git status                               //跟踪所有改动过的文件
git add <file>                           //跟踪指定的文件
git mv <old> <new>                       //文件改名
git rm <file>                            //删除文件
git rm --cached <file>                   //停止跟踪文件但不删除
git commit -m "message"                  //提交所有更新过的文件及描述
git commit --amend                       //修改最后一次提交

# 查看提交历史
git log                                  //查看提交历史
git log -p <file>                        //查看指定文件的提交历史
git blame <file>                         //以列表形式查看指定文件的提交历史

# 撤销
git reset --hard HEAD                    //撤销工作目录中所有未提交文件的修改内容
git checkout HEAD <file>                 //撤销指定的未提交文件的修改内容
git revert <commit>                      //撤销指定的提交

# 分支与标签
git branch                               //显示所有本地分支
git checkout <branch/tag>                //切换到指定分支或标签
git branch <new-branch>                  //创建新分支
git branch -d <branch>                   //删除本地分支
git tag                                  //列出所有本地标签
git tag <tagname>                        //基于最新提交创建标签
git tag -d <tagname>                     //删除标签

# 合并与衍合
git merge <branch>                       //合并指定分支到当前分支
git rebase <branch>                      //衍合指定分支到当前分支

# 远程操作
git remote -v                            //查看远程版本库信息
git remote show <remote>                 //查看指定远程版本库信息
git remote add <remote> <url>            //添加远程版本库

git fetch <remote>                       //从远程库获取代码
git pull <remote> <branch>               //下载代码及快速合并
git push <remote> <branch>               //上传代码及快速合并
git push <remote> :<branch/tag-name>     //删除远程分支或标签
git push --tags                          //上传所有标签
```

## Git 配置

```bash
# git ssh公钥
ssh-keygen -t rsa -C "laijingwei1993@163.com"

# 重置本机git设置
git config --global credential.helper store

# 全局配置
git config --global user.email "laijingwei1993@163.com"
git config --global user.name "赖经纬"
```

## Git 提交三部曲

```bash
git add .
git commit -m "update"
git push origin master

# 首次提交远程仓库
git push -u origin master

# 当本地与远程分支均为默认分支名称时即本地为master，远程分支为origin
git push

# 删除本地缓存
git rm -r --cached .
```

## Git 部署
```bash
# CentOS部署
cd /www/wwwroot/laijw.mxnt.net
git pull origin master

# 当本地与远程分支均为默认分支名称时即本地为master，远程分支为origin
git pull
```

## Commitizen

```bash
npm install -g commitizen
cd .git

# npm
commitizen init cz-conventional-changelog --save-dev --save-exact

# yarn
commitizen init cz-conventional-changelog --yarn --dev --exact

git add .
git cz
git push
```

## gitignore

```bash
#               表示此为注释,将被Git忽略
*.a             表示忽略所有 .a 结尾的文件
!lib.a          表示但lib.a除外
/TODO           表示仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/          表示忽略 build/目录下的所有文件，过滤整个build文件夹；
doc/*.txt       表示会忽略doc/notes.txt但不包括 doc/server/arch.txt
 
bin/:           表示忽略当前路径下的bin文件夹，该文件夹下的所有内容都会被忽略，不忽略 bin 文件
/bin:           表示忽略根目录下的bin文件
/*.c:           表示忽略cat.c，不忽略 build/cat.c
debug/*.obj:    表示忽略debug/io.obj，不忽略 debug/common/io.obj和tools/debug/io.obj
**/foo:         表示忽略/foo,a/foo,a/b/foo等
a/**/b:         表示忽略a/b, a/x/b,a/x/y/b等
!/bin/run.sh    表示不忽略bin目录下的run.sh文件
*.log:          表示忽略所有 .log 文件
config.php:     表示忽略当前路径的 config.php 文件
 
/mtk/           表示过滤整个文件夹
*.zip           表示过滤所有.zip文件
/mtk/do.c       表示过滤某个具体文件
 ```

被过滤掉的文件就不会出现在git仓库中（gitlab或github）了，当然本地库中还有，只是push的时候不会上传。
 
需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中，如下：
!*.zip
!/mtk/one.txt
 
唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。为什么要有两种规则呢？
想象一个场景：假如我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理，那么.gitignore规则应写为：：
/mtk/*
!/mtk/one.txt
 
假设我们只有过滤规则，而没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！
注意上面的/mtk/*不能写为/mtk/，否则父目录被前面的规则排除掉了，one.txt文件虽然加了!过滤规则，也不会生效！
 
还有一些规则如下：
fd1/*
说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；
 
/fd1/*
说明：忽略根目录下的 /fd1/ 目录的全部内容；
 
/*
!.gitignore
!/fw/ 
/fw/*
!/fw/bin/
!/fw/sf/
说明：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/ 和 /fw/sf/ 目录；注意要先对bin/的父目录使用!规则，使其不被排除。
