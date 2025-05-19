---
title: Github Pages + Hexo从零搭建个人博客（一）：基础建设
author: 濬哲
tags:
  - 前端
  - 网站建设
  - Hexo
comments: true
categories: 个人博客建设
abbrlink: blog-setup-1-basics
date: 2024-09-27 21:17:27
---



## 前言

今年我刚刚步入大三，已经进行了两年的计算机科学与技术专业的学习。这两年感觉有些摸鱼，学了一些知识，但是好像也就是为了应付考试，在考试结束以后这些知识慢慢的被遗忘了，这是我不愿意看到的。感觉如果想把自己所学的东西更好的消化吸收，光靠学是不够的，更重要的是把自己学的东西进行分享。只有当你能把一个知识点逻辑清晰的用自己的话讲述给别人时，才能说明自己真的是掌握了这个知识点。

我也见过学校里一些学长学姐的个人网站，他们分享自己的课程笔记，~~为我的期末补天提供了宝贵的资源~~。我自己也是一个比较喜欢折腾的人，感觉在这些地方折腾就像是精心布置自己的房间一样，会让自己非常的有归属感与成就感。于是，我也看了网上不少的教程，希望能够从零开始一步步搭建属于我自己的个人网站。

第一篇博客就来讲一下我是怎么搭建个人网站的吧！

<!-- more -->

## 概念简介——Github Pages、Hexo都是什么？

### Github Pages

来看一下[官方文档](https://docs.github.com/zh/pages/getting-started-with-github-pages/about-github-pages)的解释

> GitHub Pages 是一项静态站点托管服务，它直接从 GitHub 上的仓库获取 HTML、CSS 和 JavaScript 文件，（可选）通过构建过程运行文件，然后发布网站。 
>
> 你可以在 GitHub 的 `github.io` 域或自己的自定义域上托管站点。

总结一下，就是：

- Github Pages 是 Github 提供的**网页寄存服务**，用于存放**静态网页**，也就是我们的博客。
- 我们可以通过博客框架（e.g.Hexo）来把md文档转换为静态网页

- 最终可以通过自己的`github.io`**子域名**来访问到生成的静态网页



> 静态网页是指内容固定、没有动态交互的网页，通常由HTML、CSS和JavaScript构成。每次用户请求时，服务器直接返回存储在硬盘上的文件，不会根据用户的输入或行为进行变化。



而且重点是**不花钱，不花钱，不花钱**！！！

### Hexo

[Hexo官网地址](https://hexo.io/zh-cn/)	

[Hexo官方文档](https://hexo.io/zh-cn/docs/)

- Hexo 是一个快速、简洁且高效的**静态博客框架**。 

- Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
- 我们写博客的工作流就是，在本地使用Markdown编辑器写博客，然后使用本地的Hexo框架进行解析，然后一键上传

- Hexo包含丰富的**主题**，你可以选择一款自己喜欢的主题来美化自己的博客，我选择的是[Next主题](https://github.com/theme-next/hexo-theme-next)



## 从零开始搭建

默认你已经注册了Github账号并且安装了Git工具和Vscode代码编辑器



### Step1：Github Pages配置

新建仓库， 名称为`<username>.github.io` ，并保持仓库为**public**

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251954.webp)

### Step2：安装Hexo（Mac环境）

#### 要求

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

在Mac中，我们可以使用[Homebrew](https://brew.sh/zh-cn/)进行这两者的安装。Homebrew是Mac的一款包管理工具

```bash
brew install git
brew install node
```

#### 安装Hexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```
$ npm install -g hexo-cli
```



#### 初始化

在电脑上创建一个文件夹用来存放自己的博客，我在文稿中新建了一个Blogs文件夹，在vscode中打开Blogs文件夹，新建一个终端，输入命令：

```bash
cd Blogs
hexo init
```

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251955.webp)

已经成功初始化

其实这一步首先是克隆了一个Github仓库，然后执行了`npm install`命令来安装package.json中的依赖包，依赖安装完成后就会多出node_modules与package-lock.json两个文件夹。

简单介绍下hexo的文件结构：

- node_modules ：插件以及hexo所需node.js模块
- _config.yml 站点配置文件，设定一些公开信息等
- package.json 应用程序信息，配置hexo运行所需js包
- scaffolds 模板文件夹，新建文章，会默认包含对应模板内容
- themes 存放主题文件，hexo根据主题生成静态网页
- source 用于存放用户资源



我们的日常写作都是在source/_posts文件夹下



#### 启动Hexo服务

输入命令：

```bash
hexo s  //或者hexo server
```

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251956.webp)

点击链接 [http://localhost:4000](http://localhost:4000/)（图中黄色下划线位置）进行本地预览，默认是hexo内置的landscape 主题

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251957.webp)



### Step3：配置Hexo的主题

我选择的是[Next主题](https://github.com/theme-next/hexo-theme-next)

在Blogs这个主目录中，将Next主题从Github上克隆到themes文件夹中

```bash
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

可以看到themes文件夹下面多了存放Next主题的文件

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251958.webp)

接下来，我们进入到_config.yml中修改主题配置

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape
```

将其修改为Next，然后启动hexo服务

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251959.webp)

我们已经成功使用了Next主题，是不是非常的方便快捷？


### Step4：开始我们的第一篇博客文章写作！

具体内容请参考[Hexo官方文档](https://hexo.io/zh-cn/docs/writing)和[一个Hexo文章写作流程示例](https://fuguigui.github.io/hexo2/)，下面我就简单讲一点比较常用的操作



你可以执行下列命令来创建一篇新文章或者新的页面。

```bash
$ hexo new [layout] <title>
```

`post`是默认的`布局`，但你也可以提供自己的布局。 您可以通过编辑 `_config.yml` 中的 `default_layout` 设置来更改默认布局。



Hexo 有三种默认布局：`post`、`page` 和 `draft`。 Files created by each of them is saved to a different path. Newly created posts are saved to the `source/_posts` folder.

| 布局    | 路径             |
| ------- | :--------------- |
| `post`  | `source/_posts`  |
| `page`  | `source`         |
| `draft` | `source/_drafts` |



一般来说，我们就直接执行命令：

```bash
hexo new "Github Pages + Hexo从零搭建个人博客"
```

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409272251960.webp)

可以看到我们已经成功创建了一篇新的文章（文件名会把一些非法符号替换为-）

我们就按照正常的Markdown写作流程进行写作就行了





### Step5：将生成的静态页面部署到 github 上

具体内容请参考[Hexo官方文档](https://hexo.io/zh-cn/docs/writing)和[一次Hexo文章写作流程示例](https://fuguigui.github.io/hexo2/)

- 通过上面4步的操作，我们已经可以在本地通过 `localhost:4000` 查看博客页面了。
- 因此，这里我们要将 Hexo 框架生成的内容部署到 github 上，让其他家人也能看到 。



#### 常用命令介绍

先列举一些常用的命令

- Clean: `hexo clean`。该命令会删除整个`***.github.io/public/`文件夹

- Generate: `hexo generate`或者简写为`hexo g`。该命令会生成静态文件夹`public/`，也就是从markdown到网页文件html等的转换操作

- Server: 启动服务器常用的是`hexo server`或者简写为`hexo s`。

  该命令会把生成好的静态文件部署到本地的指定端口，之后即可在本地浏览器输入`localhost:4000`即可预览。

- deploy：`hexo deploy`或者简写为`hexo d`。该命令将网站部署到服务器上。实际操作是：更新你在github上的仓库`***.github.io`的指定分支（如果你采用Hexo系列第一节说到的两分支方式的话）。这是你最终发表的博客页面，你可以在浏览器上访问`https://***.github.io`来查看更新后的博客啦。

接着，给出一些命令使用的常见套路

- `hexo clean`这个命令其实很少用。使用情况常见于：更新了`_config.yml`文件夹，删除了一些已有博文等。原因就是速度慢，耗费不必要的时间。毕竟它会将整个`public/`文件夹删除，再重新生成。推荐偶尔清理使用即可。
- **通常更新一次博客的套路是先本地预览，再远程部署**。即先执行`hexo g; hexo s`，再执行`hexo d`或者`hexo g; hexo d`
- hexo有个特别便利的地方！
  - 在本地预览时，你仍可以更改markdown文件中一般的文字内容，然后直接在浏览器端刷新页面，就能看到实时更改的效果，而不需要再执行一次`hexo g;hexo s`，节省很多时间。常用于预览过程中进行微调操作。

#### 具体操作

修改站点配置文件`_config.yml`的最后部分

```yml
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: main
```

在执行之前，记得安装自动部署 (--save 加不加的区别在于是否写入到依赖文件package.json中)

```bash
npm install hexo-deployer-git --save
```

然后

```bash
hexo clean #清除之前生成的东西
hexo generate  #生成静态文章，缩写hexo g
hexo deploy  #部署文章，缩写hexo d
```

过一会儿就可以在`http://yourname.github.io`这个网站看到你的博客了！

（ps：其实部署就是把public内的所有内容推送到仓库中。.gitignore中的内容是给版本控制用的）

