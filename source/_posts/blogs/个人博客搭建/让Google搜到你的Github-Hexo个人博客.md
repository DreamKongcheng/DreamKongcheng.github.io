---
title: 让Google搜到你的Github-Hexo个人博客
author: JunZhe
date: 2024-10-10 17:58:30
tags:
- 前端 
- 网站建设
- Hexo
comments: true
categories: 个人博客建设
---



## 前言

前段时间自己折腾了一下博客，初步建立起了自己的小站，今天心血来潮在谷歌搜索自己之前写的[从零搭建个人博客](https://dreamkongcheng.github.io/blogs/personal-blog-setup/Github%20Pages%20+%20Hexo%E4%BB%8E%E9%9B%B6%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%88%E4%B8%80%EF%BC%89/)的文章，结果在 Google 上面翻了十页都没有翻到，我一开始还以为是因为发了没多久的缘故，后来一查才知道 GitHub Pages 屏蔽了Google 的爬虫，所以在 Google 里是搜索不到 GitHub Pages 上面的网页的。

这怎么行？！

对于我来说，我写博客主要是为了将自己学习的知识进行一个输出，虽然不是什么高大上的东西，但是我相信一定有和我一样刚刚在计算机领域起步，并且热爱探索、折腾工具的朋友，我的这些经验和感悟或许就能给大家带来一点小小的启发。另外，因为是要写给别人看，所以要更加注重自己语言的逻辑组织。并且要把一件事能够完全的和别人讲清楚，还需要自己更高层次的理解，这反过来也倒逼了我自己去进行更深度的思考，让我更好的理解掌握知识。

话说回来，我不是写只给自己看的日记的，那些我都存放在本地的 obsidian 里面。之后或许有机会写一些我折腾 obsidian 的记录（~~逃~~），我希望我的博客能在网络的海洋里有幸被人看到。

<!--more-->



## 验证自己的博客能否被搜索到

打开Google，输入`site:https://<username>.github.io/`

如果没被索引到，在搜索结果页面就会直接提示你使用[Google Search Console](https://search.google.com/search-console?hl=zh-CN)。



## Google搜索提交

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202410281119393.webp)

在“网址前缀”里输入你的博客网址`https://<username>.github.io>`，然后建议选择HTML文件验证。具体方法为：

下载文件，然后把这个文件**添加到你的Github博客根目录中**，我用的是Hexo博客，以此举例。

将刚刚的文件放入你的source文件夹，然后执行`hexo g`将其添加到public文件夹中，public文件夹就是你博客的内容。

⚠️：你得在**站点配置文件**_config.yml设置不渲染.html文件，否则会出错，具体操作请见我的另一篇文章[Hexo如何不渲染.md与.html文件](https://dreamkongcheng.github.io/blogs/personal-blog-setup/Hexo%E5%A6%82%E4%BD%95%E4%B8%8D%E6%B8%B2%E6%9F%93-md%E4%B8%8E-html%E6%96%87%E4%BB%B6/).

在_config.yml里的`skip_render: `字段下设置：

```yml
skip_render: 
- 'README.md'
- '*.html'
```

然后 `hexo g `&& `hexo d`，过一会点一下验证就行了

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202410281119394.webp)

点击前往资源页面，进行站点地图添加



## 添加站点地图

1. 首先在本地Hexo博客目录下安装扩展

```bash
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

这里索性把百度的也搞了

2. 打开站点配置文件_config.yml，添加

```bash
# 自动生成sitemap
sitemap:
path: sitemap.xml
```

然后`hexo clean && hexo g && hexo d`提交博客。这时能够找到public\sitemap.xml文件。

3. 在资源页面添加站点地图

![image-20241010170844375](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202410281119395.webp)

我因为把sitemap放在博客根目录下，所以在这里直接输入sitemap即可



## 添加robots.txt

> robots.txt（统一小写）是一种存放于网站根目录下的 ASCII 编码的文本文件，它通常告诉网络搜索引擎的漫游器（又称网络蜘蛛），此网站中的哪些内容是不应被搜索引擎的漫游器获取的，哪些是可以被漫游器获取的。

在 `source` 目录下增加 `robots.txt` 文件， 我的文件具体内容如下可供参考，注意将域名改为自己的网站：

```
User-agent: *
Allow: /
Allow: /about/
Allow: /archives/
Allow: /blogs/
Allow: /categories/
Allow: /tags/

Disallow: /js/
Disallow: /css/
Disallow: /lib/

Sitemap: https://www.DreamKongcheng.com/sitemap.xml
Sitemap: https://www.DreamKongcheng.com/baidusitemap.xml

```



## 说明

提交博客之后，需要等待一段时间才能在Google上搜到，因为Google需要时间来处理我们的请求、抓取相应网页并将其编入索引。



---

参考文章：

[让Google搜索到GitHub上的个人博客](https://blog.csdn.net/weixin_44058333/article/details/100165245)

[Hexo博客提交链接到搜索引擎来收录](https://www.xiemingzhao.com/posts/HexoblogSE.html)
