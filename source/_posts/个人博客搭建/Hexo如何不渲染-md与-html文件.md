---
title: Hexo如何不渲染.md与.html文件
author: JunZhe
tags:
  - 前端
  - 网站建设
  - Hexo
categories: 个人博客建设
abbrlink: hexo-skip-render
date: 2024-10-10 16:58:37
---

## 前言
众所周知，Hexo会自动将 source 文件夹下的所有 .md 与 .html 文件渲染。但有的时候，这会造成很大的问题。比如我写了个 README.md 文件，或者我想在根目录下添加一个 html 文件（比如谷歌用于验证网站的 html 文件），他们都会在 `hexo g` 时候被渲染。如果我们把这些文件直接放在 public 文件夹下，那么他们就不会被渲染，但是当我们执行了 `hexo clean` 之后，这些文件就会被删除。我们希望能够把这些文件放在我们的 source 文件夹下，每次 `hexo g` 的时候被**拷贝**到 public文件夹下而不被**渲染**。

<!--more-->
## 操作方法
找到**站点配置文件** `_config.yml`，在其中添加以下配置：

```yml
skip_render:
  - 'README.md'
  - '*.html'
```
这样符合规则的文件就不会被渲染了，他们会原封不动地进入到 pubilc 文件夹，存放在博客的根目录。完美！

方法参考：
[Hexo不渲染.md或者.html](https://blog.csdn.net/ganzhilin520/article/details/79057774)