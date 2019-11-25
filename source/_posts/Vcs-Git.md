---
title: Vcs Git
date: 2019-07-09 21:58:27
updated: 2019-07-09 21:58:27
categories: Git
tags: [Vcs,Git]
---

本文总结版本控制工具git在日常开发工作常用到的一些命令，以及一些常用的场景应用，比如分支管理，远程管理，合并冲突处理等。后续持续更新中。

#### 常用命令

下面的图片很清晰的说明来一些命令和各个区域的关系 

![img](https://lairdli.top/images/git-command.png)

##### 常用
```bash
git remote add origin git@github.com:yeszao/dofiler.git   # 配置远程git版本库
git pull origin master                                    # 下载代码及快速合并 
git push origin master                                    # 上传代码及快速合并
git fetch origin                                          # 从远程库获取代码

git branch                                                # 显示所有分支
git checkout master                                       # 切换到master分支
git checkout -b dev                                       # 创建并切换到dev分支
git commit -m "first version"                             # 提交

git status                                                # 查看状态
git log                                                   # 查看提交历史

git config --global core.editor vim                       # 设置默认编辑器为vim（git默认用nano）
git config core.ignorecase false                          # 设置大小写敏感
git config --global user.name "YOUR NAME"                 # 设置用户名
git config --global user.email "YOUR EMAIL ADDRESS"       # 设置邮箱
```
<!--more-->

##### 创建版本库
```bash
git clone <url>                 # 克隆远程版本库
git init                        # 初始化本地版本库
```
##### 修改和提交
```bash
git status                      # 查看状态
git diff                        # 查看变更内容
git add .                       # 跟踪所有改动过的文件
git add <file>                  # 跟踪指定的文件
git mv <old> <new>              # 文件改名
git rm <file>                   # 删除文件
git rm --cached <file>          # 停止跟踪文件但不删除
git commit -m “commit message”  # 提交所有更新过的文件
git commit --amend              # 修改最后一次提交
```
##### 查看提交历史
```bash
git log                         # 查看提交历史
git log -p <file>               # 查看指定文件的提交历史
git blame <file>                # 以列表方式查看指定文件的提交历史
```
##### 撤消
```bash
git reset --hard HEAD           # 撤消工作目录中所有未提交文件的修改内容
git reset --hard <version>      # 撤销到某个特定版本
git checkout HEAD <file>        # 撤消指定的未提交文件的修改内容
git checkout -- <file>          # 同上一个命令
git revert <commit>             # 撤消指定的提交
```
##### 分支与标签
```bash
git branch                      # 显示所有本地分支
git checkout <branch/tag>       # 切换到指定分支或标签
git branch <new-branch>         # 创建新分支
git branch -d <branch>          # 删除本地分支
git tag                         # 列出所有本地标签
git tag <tagname>               # 基于最新提交创建标签
git tag -a "v1.0" -m "一些说明"  # -a指定标签名称，-m指定标签说明
git tag -d <tagname>            # 删除标签

git checkout dev                # 合并特定的commit到dev分支上
git cherry-pick 62ecb3
```
##### 合并与衍合

```bash
git merge <branch>              # 合并指定分支到当前分支
git merge --abort               # 取消当前合并，重建合并前状态
git merge dev -Xtheirs          # 以合并dev分支到当前分支，有冲突则以dev分支为准
git rebase <branch>             # 衍合指定分支到当前分支
```

##### 远程操作

```bash
git remote -v                   # 查看远程版本库信息
git remote show <remote>        # 查看指定远程版本库信息
git remote add <remote> <url>   # 添加远程版本库
git remote remove <remote>      # 删除指定的远程版本库
git fetch <remote>              # 从远程库获取代码
git pull <remote> <branch>      # 下载代码及快速合并
git push <remote> <branch>      # 上传代码及快速合并
git push <remote> :<branch/tag-name> # 删除远程分支或标签
git push --tags                 # 上传所有标签
```

#### Git 分支管理

Git Flow流程管理,参见如下图

![img](https://lairdli.top/images//git-flow.png)

##### 主分支master

##### 开发分支develop

```bash
git checkout -b develop master
# 切换到Master分支
git checkout master
# 对Develop分支进行合并,使用--no-ff参数后，会执行正常合并，
# 在Master分支上生成一个新节点。
# 为了保证版本演进的清晰，我们希望采用这种做法。
git merge --no-ff develop
```

##### 临时分支

* 功能（feature）分支,为了开发某种特定功能，从Develop分支上面分出来的。开发完成后，要再并入Develop。

```bash
# 创建一个功能分支
git checkout -b feature-x develop
# 开发完成后，将功能分支合并到develop分支：
git checkout develop
git merge --no-ff feature-x
删除feature分支
git branch -d feature-x
```

* 预发布（release）分支,发布正式版本之前（即合并到Master分支之前），我们可能需要有一个预发布的版本进行测试。预发布分支是从Develop分支上面分出来的，预发布结束以后，必须合并进Develop和Master分支。它的命名，可以采用release-*的形式。

```bash
# 创建一个预发布分支
git checkout -b release-1.2 develop
# 确认没有问题后，合并到master分支：
git checkout master
git merge --no-ff release-1.2
# 对合并生成的新节点，做一个标签
git tag -a 1.2
# 再合并到develop分支
git checkout develop
git merge --no-ff release-1.2
# 最后，删除预发布分支：
git branch -d release-1.2
```

* 修补bug（fixbug）分支。软件正式发布以后，难免会出现bug。这时就需要创建一个分支，进行bug修补。修补bug分支是从Master分支上面分出来的。修补结束以后，再合并进Master和Develop分支。它的命名，可以采用fixbug-*的形式。
  
```bash
# 创建一个修补bug分支
git checkout -b fixbug-0.1 master
# 修补结束后，合并到master分支：
git checkout master
git merge --no-ff fixbug-0.1
git tag -a 0.1.1
# 再合并到develop分支
git checkout develop
git merge --no-ff fixbug-0.1
# 最后，删除"修补bug分支"：
git branch -d fixbug-0.1
```


#### Git 远程管理

##### Git服务器迁移另外一台GIT服务器

前提条件：

- first.git已存在

- second.git 待同步仓储 第一次需初始化.

  可以在gitlab,github网页初始化，空项目，不要初始化README.md等

  可以以命令行方式初始化

```bash
git init --bare
```

方式一：

```bash
git clone --bare https://first.git First-Server 
cd First-Server 
git add tencent https://second.git
git push tencent --all
```

方式二：

```bash
git clone --mirror https://first.git First-Server 
cd First-Server
git push --mirror https://second.git
```

##### SVN服务器迁移到GIT服务器

svn代码迁移到git服务器，主要用到git-svn命令

```bash
# 创建user.txt 提交记录映射表
svn log --xml | grep author | sort -u | perl -pe 's/.*>(.*?)<.*/$1 = /'
# 拉取svn代码
git svn clone http://svn_address --authors-file=users.txt --no-metadata -s my_project
# 如果提交记录太多，可选取最近提交记录，以下是取最近5000次
git svn clone -r5000:HEAD svn_address --authors-file=users.txt --no-metadata -s my_project
# 清理工作
cp -Rf .git/refs/remotes/origin/tags/* .git/refs/tags/
rm -Rf .git/refs/remotes
# 添加git服务器地址，并上传
git remote add origin git@my-git-server:myrepository.git
git push origin --all
```

##### 绑定多个服务器

方式一：git remote add

```bash
git remote -v
git remote add tecent https://xxx.git
git push origin master:master
git push tecent master:master
```

方式二 git remote set-url

```bash
git remote set-url --add https://xxx.git
cat .git/config
git push origin --all
```

##### 切换已有仓储到另外一个git仓储

```
git remote set-url origin https://xxx.git
git branch --set-upstream-to 远程分支
```

#### 合并冲突处理

```bash
git merge 分支名
//有冲突的话，通过IDE解决冲突,
git status //查看状态然后再执行
git add 
git commit
```

#### 服务器选择

git服务器选择，如果是小团队的话，建议直接服务器安装git后，命令行直接创建，也可以选择gitlab搭建，当然如果不介意公网，想更可视化查看代码，也可以考虑一些云服务器，目前国内的码云，阿里云，腾讯云,以及国外的github等都提供免费的个人代码云仓储。

>- [Git](https://git-scm.com/) 命令行直接搭建 git init —bare
>- 搭建[gitlab](https://about.gitlab.com/)内网环境
>- 选择免费的云服务器代码托管 [github](https://github.com/)，[码云](https://gitee.com/)，[阿里云](https://code.aliyun.com/)，[腾讯云](https://code.aliyun.com/)等。

#### 参考

>- [Git-SCM](https://git-scm.com/)
>- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
>- [Git分支管理策略](http://www.ruanyifeng.com/blog/2012/07/git.html)
>- [Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)
>- [Git 命令图形化训练](https://learngitbranching.js.org/)

#### 推荐阅读

> - [Android 学习书籍推荐](<https://lairdli.top/2018/05/25/Android-Book-Recomendations/>)
> - [Android 常用第三方库整理](<https://lairdli.top/2019/02/25/Android-3rd-Libs/>)
> - [Android 知识点脑图整理](<https://lairdli.top/2019/01/30/Android-Journey/>)
> - [Android 路线图](<https://lairdli.top/2019/05/19/Android-RoadMap/>)
> - [Android NDK知识脑图整理](<https://lairdli.top/2019/06/01/Android-NDK-RoadMap/>)
> - [Andorid C知识脑图整理](<https://lairdli.top/2019/06/09/Android-C-RoadMap/>)
> - [Android Helper 软件开发工具集](<https://lairdli.top/2019/06/18/Android-Helper/>)
