---
title: Github Pages + Hexo从零搭建个人博客（二）：Git双分支管理网页与源文件
author: JunZhe
date: 2024-09-28 18:46:45
tags:
- 前端 
- 网站建设
comments: true
categories: 个人博客建设
---



## 双分支管理

参考文章：[使用 GitHub 分支保存 Hexo 环境和博文](https://blog.csdn.net/gatieme/article/details/82317704)

### 为什么要双分支管理？

`hexo d`命令实际上是用了hexo-deploy-git工具，将public中的内容加入到.deploy_git文件夹中，然后把这个文件夹的内容同步到远程仓库(YourgithubName.github.io)中你[前面设置](#具体操作)的分支中。我这里设置的是main。

注意！你的source文件夹等是不会到public里面去的，所以不会被同步！

那么问题来了。如果我需要在不同地方撰写我的博客，或者我需要使用github来进行备份，该怎么办呢？

这时候就需要我们用两个分支，第一个main分支保存public的html内容，也就是我们的网站，另一个source分支来保存我们的配置文件、md源文件等。

<!--more-->

### 具体操作

（如果完全安装我前面的步骤，你应该还没有进行`git init`，也没有同步远程仓库）

1. 初始化 Hexo 项目为 Git 仓库

```bash
cd Blogs  # 返回到 Hexo 项目的根目录
git init  # 初始化 Git 仓库
```

2. 切换到一个新的分支来保存源文件：

```bash
git checkout -b source
```

3. 将当前的 Hexo 源文件（如 `_config.yml`、`themes` 目录、`source` 目录等）提交到这个 `source` 分支：

```bash
git add .
git commit -m "Initial commit of Hexo source files"
```

4. 关联远程仓库

```bash
git remote add origin git@github.com:<YourName>/<YourName>.github.io
```

这一步需要你配置好ssh key，具体方法请自行google

通过`git remote -v`来检查是否关联成功，若成功，有如下消息：

```
origin  git@github.com:<YourName>/<YourName>.github.io (fetch)
origin  git@github.com:<YourName>/<YourName>.github.io (push)
```

5. 推送

```bash
git push -u origin source
```

这样就成功把源文件保存到`<YourName>.github.io`仓库的source分支了

接下来，你已经能够对你的整个Hexo博客环境进行git版本控制了，接下来尽情Diy你的个人博客吧！:smiley:





