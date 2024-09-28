---
title: Github Pages + Hexo从零搭建个人博客（三）：Next主题美化
author: JunZhe
date: 2024-09-28 18:46:45
tags:
- 前端 
- 网站建设
comments: true
categories: 个人博客建设
---

参考文章：[Hexo+Github Page｜基础教程(二)：NexT 主题基本美化｜全网最细致全面的教程](https://sspai.com/post/85116)

首先来讲一下**站点配置文件**和**主题配置文件**

- 站点配置文件
  - 位于博客根目录下的`_config.yml`
- 主题配置文件
  - 位于themes/next中的`_config.yml`

## 站点配置



## 主题配置

### 更换内置主题

在`Schemes`下可以看到这些主题，去掉想要的主题前面的 # 即可

```yml
# Schemes
#scheme: Muse
scheme: Mist
#scheme: Pisces
#scheme: Gemini
```

这里我选择了Mist主题，我很喜欢他的顶部导航栏

![image-20240928212948404](assets/Github Pages + Hexo从零搭建个人博客（三）/image-20240928212948404.png)

### 设置菜单

1. 把你想要展示的东西都取消注释掉

```yml
# ---------------------------------------------------------------
# Menu Settings
# ---------------------------------------------------------------

# Usage: `Key: /link/ || icon`
# Key is the name of menu item. If the translation for this item is available, the translated text will be loaded, otherwise the Key name will be used. Key is case-senstive.
# Value before `||` delimiter is the target link, value after `||` delimiter is the name of Font Awesome icon.
# When running the site in a subdirectory (e.g. yoursite.com/blog), remove the leading slash from link value (/archives -> archives).
# External url should start with http:// or https://
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

这时候在本地预览里可以看到这些入口已经出现了，但是点进去会报错`Cannot GET /tags/`

这是因为你还没有在_post里面新建**页面（page）**。



如果需要更改图标，可以进入[Font Awesome](https://sspai.com/link?target=https%3A%2F%2Ffontawesome.dashgame.com%2F)获取新图标，只需将||后的内容改为“fa + 复制的图标”即可

2. 进入终端，输入命令（以创建tags为例）

```bash
cd Blogs
hexo new page "tags"
```

完成以后在Blogs/source目录中会出现tags文件夹，其中含有index.md文件，文件内容如下：

```
---
title: tags
date: 2024-09-28 10:56:39
---
```

3. 接下来添加字段： `type: tags`（必须要添加，不然网页里是不会显示内容的）

```
---
title: tags
date: 2024-09-28 10:56:39
type: tags
---
```

![image-20240928214810057](assets/Github Pages + Hexo从零搭建个人博客（三）/image-20240928214810057.png)

这样就对了



> 其实这个的原理就是在hexo g的时候会在public文件夹下生成tags文件夹，里面是由刚刚的index.md生成的index.html，它包含了tags这个页面的全部内容



其他的几个都同理



4. （可选）为菜单栏的图标添加内容数量统计，效果如下：

![image-20240928215331479](assets/Github Pages + Hexo从零搭建个人博客（三）/image-20240928215331479.png)



### 设置侧边栏

```yml
# ---------------------------------------------------------------
# Sidebar Settings
# See: https://theme-next.org/docs/theme-settings/sidebar
# ---------------------------------------------------------------

sidebar:
  # Sidebar Position.
  position: left
  #position: right

  # Manual define the sidebar width. If commented, will be default for:
  # Muse | Mist: 320
  # Pisces | Gemini: 240
  width: 250

  # Sidebar Display (only for Muse | Mist), available values:
  #  - post    expand on posts automatically. Default.
  #  - always  expand for all pages automatically.
  #  - hide    expand only when click on the sidebar toggle icon.
  #  - remove  totally remove sidebar including sidebar toggle.
  display: post

  # Sidebar padding in pixels.
  padding: 30
  # Sidebar offset from top menubar in pixels (only for Pisces | Gemini).
  offset: 12
  # Enable sidebar on narrow view (only for Muse | Mist).
  onmobile: false
```

- position：sidebar是在左边还是右边展示
- width：sidebar的宽度
- display：默认的显示模式，是默认为展开还是默认为关闭，看个人喜好吧，我默认关闭

- padding：和顶部的距离，数字越大你的名字、头像这些东西和上面离得越开，默认的18太顶天了，我改成30了

- onmobile：当你把网页侧边距变小（把窗口拉窄）时，sidebar会继续待着还是自动收起来，建议选择false，即会自动收起来，不然很丑



```yml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/head.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: true
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```

- 这一部分是设置头像的
- url：头像的图片保存在themes/next/source/images文件夹中
- rounded：头像变成圆框，推荐
- rotated：鼠标放上去会旋转，~~有点沙雕~~



```yml
# Posts / Categories / Tags in sidebar.
site_state: true
```

- 是否展示这三个图标，方便你在sidebar里快速导航

![image-20240928220954102](assets/Github Pages + Hexo从零搭建个人博客（三）/image-20240928220954102.png)



```yml
# Social Links
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimiter is the target permalink, value after `||` delimiter is the name of Font Awesome icon.
social:
  GitHub: https://github.com/yourname || fab fa-github
  E-Mail: mailto:yzy20040303@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  #FB Page: https://www.facebook.com/yourname || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  #Instagram: https://instagram.com/yourname || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype
```

- 社交链接：自行设置即可，||后面依然是图标



有点写不动了，感觉注释很详细，可以跟着注释去做



### 设置右上角Github图标

```yml
# `Follow me on GitHub` banner in the top-right corner.
github_banner:
  enable: true
  permalink: https://github.com/DreamKongcheng
  title: Follow me on GitHub

```

