---
title: Vscode工作区管理
author: 濬哲
date: 2024-10-03 10:31:19
tags:
categories:
---

https://juejin.cn/post/7066032710778617892

这句话是在解释 VSCode 的多根工作区（Multi-root Workspace）功能。让我详细解释一下：

1. `.code-workspace` 文件：
   这是一个特殊的配置文件，用于定义 VSCode 的多根工作区。

2. 多根工作区的概念：
   不是将所有项目放在一个物理文件夹中，而是通过配置文件将多个独立的项目或文件夹逻辑地组合在一起。

3. 工作原理：
   - 每个项目保持在其原有的位置
   - `.code-workspace` 文件定义了哪些项目属于这个工作区
   - VSCode 将这些项目作为一个整体来管理

4. 优势：
   - 每个项目保持独立性
   - 可以方便地组合不同位置的项目
   - 避免了单一大文件夹带来的路径解析问题

5. 使用方法：
   创建一个 `.code-workspace` 文件，例如：

```json:frontend.code-workspace
{
  "folders": [
    { "path": "/path/to/项目A" },
    { "path": "/path/to/项目B" },
    { "path": "/path/to/项目C" }
  ]
}
```


然后在 VSCode 中打开这个 `.code-workspace` 文件，就可以同时操作多个项目了。

这种方法可以有效解决您之前提到的路径问题，因为每个项目都被视为独立的根目录。



不是将所有项目放在一个文件夹中，而是创建一个 .code-workspace 文件



最好的方式就是单独给一个文件夹存放所有的工作区文件，这样就把工作区完全虚拟化

文件夹级设置：.vscode文件夹下包含settings.json



在 .vscode 文件夹中，您还可以创建其他配置文件，如：

launch.json：用于调试配置

tasks.json：用于定义任务

extensions.json：用于推荐插件



注意事项：

这些设置只会影响当前项目文件夹。

您可以将 .vscode 文件夹添加到版本控制中，以便团队成员共享相同的设置。

如果某些设置涉及敏感信息或个人偏好，可以将它们添加到 .gitignore 文件中。

通过这种方式，您可以为每个项目创建特定的设置，这些设置会覆盖工作区和全局设置。这对于确保项目的一致性和特定需求非常有用。

## 关于扩展管理
如果是做一些小的东西，是不需要使用工作区的，比如我用vscode打开我的Blogs文件夹，那这个时候我的这个Blogs文件夹就是我的根目录，如果我只是在这个根目录不想打开C/CPP的扩展，我就选择禁用工作区就行，这样也不会产生.vscode文件夹。产生这个文件夹好像只有你**修改工作区设置**的时候才会触发。

![image-20241008120015964](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202410081200078.webp)



建议就是只是管理一些小项目，比如os的lab，oop的lab这些，就把每个文件夹当成工作区，去控制扩展启用情况，然后把文件夹用Project Manager这个插件管理一下就行，不需要去建立工作区了。

什么时候需要多根工作区？当你处理大型项目，比如web，你同时要管前后端而且前后端的插件都很多还很不一样的时候，那用多根吧

多根工作区长这样：

![image-20241008120850627](https://cdn.jsdelivr.net/gh/DreamKongcheng/image-repo/blogs/202410081208755.webp)



这里的扩展开关也不会有.vscode，扩展开关是扩展本身控制的



工作区的扩展设置在.workspace中会有反应，文件夹的扩展设置在.vscode