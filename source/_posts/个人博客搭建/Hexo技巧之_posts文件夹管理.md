---
title: Hexo技巧之_posts文件夹管理
author: JunZhe
tags:
  - 前端
  - 网站建设
  - Hexo
categories: 个人博客建设
abbrlink: hexo-posts-folder-manage
date: 2024-09-28 20:04:37
---

## 前言
在搭建起我的Hexo框架并且进行了一些的博客写作之后，我发现我习惯是有一点灵感就把他记录下来，然后想着后面有更多输入之后再来填这个坑。但是这样我就会有大量的文档堆在_posts文件夹下面，非常混乱。虽然Hexo也提供了_drafts文件夹来存放草稿，但是就算这样，等我想要发布的时候还是会有很多的文件在_posts文件夹下面。网上很多人都是用年/月/日来建立文件夹进行分类，但是这不能从根本上解决**本地**分类混乱的问题（线上的分类可以用文章的front-matter来解决）。所以我就想着能不能用文件夹来分类，就像我自己在obsidian里面搭建的个人知识体系一样，下面给出我的一些解决方法.

<!--more-->

## 解决方法
参考文章：[Hexo - 使文章依文章分类为资料夹名称置放](https://mouson.im/Notes/Hexo/make-hexo-post-category-by-folder/)

_config.yml文件中的设置：
```yml
permalink: :title/
new_post_name: :title.md
```
⚠️说明：
permalink中的`:title`是相对于_posts文件夹的，而new_post_name中的`:title`是你在`hexo new`命令中输入的文件名（会稍稍处理一下，把空格什么的变成-号），然后在后面加上.md作为你在文件列表里看到的文件名。（**不是文章的标题！**）


所以我这样设置之后，我就按自己的需要再_posts文件夹下面建立分类文件夹，比如“个人博客搭建”来存放我所有关于博客搭建的文章，以及这篇文章。而在“计算机网络”文件夹下面存放所有关于计算机网络的笔记。在`hexo new <title>`的时候，文章一开始被放在_posts下面，然后你根据需要把他丢进具体的分类文件夹里，是不是很方便！然后在`hexo g`的时候，public文件夹里的目录就是和你的_posts文件夹一样的结构，看起来也很清爽。
另外，你还可以在front-matter里面加上categories来进行线上的分类，可以和本地统一也可以采用不同的分类方法。

## 进阶设置
其实本地的_post文件夹的结构和线上没有关系，在本地可以用中文目录进行分类，然后在`_config.yml`进行如下设置：
```yml
permalink: posts/:abbrlink.html
```

然后在每一篇文章的front-matter里面加上`abbrlink`，比如：
```
---
title: Github Pages + Hexo从零搭建个人博客（一）：基础建设
abbrlink: blog-setup-1-basics
---
```

这样线上的链接就会是`https://<YourName>.github.io/posts/<abbrlink>.html`，而本地的文件夹结构可以是中文的，比如“个人博客搭建”，这样即不会有url编码的问题，也能在本地清晰的进行分类，而且还利于SEO优化。


## 总结
1. 和你在本地存放笔记那样，用文件类别作为区分，会比用日期区分更加清晰。
2. 如你习惯以`hexo new draft`作草稿编辑，那在进行`hexo publish {title}`后，文章会进入_posts中，还需要手动再把它塞进你想让他去的文件夹。
3. 如果你的文件夹是中文，那你文章最终的链接会存在一些url编码，看起来有些丑，不过你完全可以在本地使用英文文件夹，然后在front-matter里面加上中文的categories，这样就可以解决这个问题了。

希望这篇文章对你有所帮助！
