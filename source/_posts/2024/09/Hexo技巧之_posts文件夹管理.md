---
title: Hexo技巧之_posts文件夹管理
author: JunZhe
date: 2024-09-28 20:04:37
tags:
categories:
---


[如何在Hexo中对文章md文件分类](https://www.githang.com/2018/12/22/hexo-new-post-path/)


经过测试，用日期文件夹来分类只需要如下设置即可：

```yml
permalink: :year/:month/:day/:title/ #这里的title是相对于_posts文件夹的
new_post_name: :year/:month/:title.md
```

这种情况下permalink中的`:title`是对的，但是如果你用了其他名字的文件夹就会出问题

![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409282019287.webp)



![](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202409282020175.webp)



可以看到确实是year/month/day/title
