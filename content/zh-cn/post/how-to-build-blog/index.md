---
title: "如何快速创建一个博客"
description: 从零开始的 GitHub Page + Hugo 简易博客打造教程
slug: "how-to-build-blog"
draft: true
date: 2024-06-15
categories:
    - Tutorial
tags:
    - Hugo
    - Blog
---

最近心血来潮有点没事干（不是作业太少）所以寻思着要么弄个个人博客写写东西，这样好歹看起来还挺牛的样子（不是），也就因此有了这个博客。

弄完基础的博客内容之后又开始想说发啥好呢，想来想去感觉诶不如直接把我弄这个个人博客的过程写一个教程，又是总结一下自己这几天干了啥又可以造福别人这何尝不是一件美事呢.jpg

话不多说以下开始正题：

## 如何使用 GitHub Page + Hugo 来快速创建一个博客

### 前提条件

* 一个 [GitHub](https://github.com) 账户
* 一台电脑 （因为我个人比较推荐本地跑一下网站 Demo 而不是在线编辑）
* 能阅读英文（或者会使用翻译软件）
* 电脑基础知识（会使用命令行，了解基础 GitHub 操作）

### 开始

首先，如果你不是一个前端开发人员，或者你不想重新造轮子，你可以在 Hugo 的官方网站上寻找你满意的主题。

Hugo 的网站上有许多好看可用的[博客主题](https://themes.gohugo.io/tags/blog/)，我个人觉得比较可以的是以下四个（以 Star 数从多到少）：

* [PaperMod](https://themes.gohugo.io/themes/hugo-papermod)
* [Stack](https://themes.gohugo.io/themes/hugo-theme-stack)
* [Paper](https://themes.gohugo.io/themes/hugo-paper)
* [TailWind](https://themes.gohugo.io/themes/hugo-theme-tailwind)

此博客使用 Stack 主题构建，因此以下主要以 Stack 主题的项目文件结构来进行讲解

### 创建仓库

因为需要使用 GitHub Page 来部署博客，所以我们需要先创建一个 GitHub 仓库。

一般来说会选择创建一个 `GitHub用户名.github.io` 名称的仓库作为个人博客的地址。例: `lxymahatma.github.io`

许多 Hugo 主题（比如 Stack）提供了一个[仓库模板](https://github.com/CaiJimmy/hugo-theme-stack-starter)专门用来创建新的仓库，这里分成两种情况进行讨论

#### 传统方式（无 generated from template 显示）

* 直接通过 GitHub 网页端创建一个新的仓库
* 把创建好的仓库以及仓库模板克隆到本地（可以使用命令行 `git clone` 或者直接使用 GitHub Desktop）
* 把你需要的内容从仓库模板里复制到你的仓库里，一般来说为以下几个：
  * .github
  * assets
  * config
  * content
  * static
  * .gitignore
  * go.mod
  * go.sum

#### 简单版本（新手推荐！）

* 打开仓库模板的页面，可以根据 ReadMe 的内容进行操作。
* 把创建好的仓库克隆到本地（可以使用命令行 `git clone` 或者直接使用 GitHub Desktop）

### 本地环境配置

**注意：此篇文章针对 Windows 环境编写，因此路径分隔符均为 `\`， 如果使用 macOS 或者 Linux 需要将路径分隔符替换为 "/"**

### 修改配置

**注意：此处配置文件都使用 Stack 主题模板的 toml 文件，如果你不熟悉 toml 语法，可以通过 [toml 官方网站](https://toml.io/cn/v1.0.0) 学习，也可以使用 yaml 或者 json**

#### 多语言配置

首先你需要决定你的个人博客是否需要多语言支持，如果不需要，你可以直接跳到下一小节。

Hugo 有内置的多语言配置，而 Stack 主题也提供了[方法](https://stack.jimmycai.com/config/i18n)，此教程根据 Hugo 官方内置配置模板进行教学。

* 进入 `config\_default` 文件夹，找到并重命名 `_languages.toml` 为 `languages.toml`，打开文件
* 接着，根据 [Hugo 官方文档](https://gohugo.io/content-management/multilingual) 进行配置
  * 因为文件名已经为 `languages.toml`，因此并不需要写成 `[languages.en]` 的形式，只要和已有的一样写成 `[en]`就行
  * 可以参考 [我的配置](https://github.com/lxymahatma/lxymahatma.github.io/blob/main/config/_default/languages.toml) 进行修改

下面简单讲解一下我的配置中各项代表了什么

* `languageName`: 切换语言的下拉框中的语言名字显示
* `languageDirection`: 语言阅读方向（从左往右）
* `contentDir`: 博客内容的文件夹（可以对于不同语言设置发布内容不同）
* `title`: 博客的标题
* `weight`: 下拉框中的排序权重，越高越在底下

而 `[params]` 是在 `params.toml` 中的配置

* `sidebar.subtitle`: 博客的副标题
* `article.license.default`: 文章底部的协议

我把 `parames.toml` 里的这两个配置给删除并且设置了多语言，如果不需要的话也可以不修改

#### 基础配置

#### 图片修改

* 头像的修改是在 `assets\img\avatar.png`，把这个图片替换成你想要的头像就行
  * 如果你的图片类型不是 `.png` 或者你不想起名叫 `avatar.png`，找到 `params.toml` 中的

    ```toml
    [sidebar.avatar]
    enabled = true
    local = true
    src = "img/avatar.png"
    ```

    将 src 修改为你的图片路径即可

#### 分类与标签设置

#### 创建文章模板

#### 小细节（踩坑）

* 在 `config.toml` 中, 可以添加一项 `timeZone = "Asia/Shanghai"`。这个设置的目的是让 Hugo 在构建你的网站的时候，会根据设定的时区来确定是否发布对应的文章。

在默认情况下，Hugo 会使用构建时候的电脑时区来判断当前时间，但是有些情况下也会使用 UTC +0 的时区来进行判断。因此，如果你把你的网站内容推送到 Github 进行构建，当你已经是下一天的时候，可能 Hugo 获取的时间还是前一天，所以推送的文章并不会被发表。

### 添加评论系统

最后一步就是给博客添加评论系统，此博客选择的是 [giscus](https://lxymahatma.github.io/)。
对于 giscus 的基础设置就不再过多赘述，讲一下如何设置到个人博客里：

* 把 giscus 的 `启用 giscus` 中的 script 给复制下来
* 删除 `config.toml` 中的 `disqusShortname = "hugo-theme-stack"`
* 在 `params.toml` 中，可以看到有

    ```toml
    ## Comments
    [comments]
    enabled = true
    provider = "disqus"
    ```

    将 `provider` 设置为 `"giscus"`

* 再往下滑能看到

    ```toml
    [comments.giscus]
    repo = ""
    repoID = ""
    category = ""
    categoryID = ""
    mapping = ""
    lightTheme = ""
    darkTheme = ""
    reactionsEnabled = 1
    emitMetadata = 0
    ```

    这时就需要把复制的 script 中的信息分别填写进去。`lightTheme` 和 `darkTheme` 如果比较懒的话可以直接填写 `light` 和 `dark`

### 最后的推送与设置

**如果有任何关于文章的问题可以在底下评论区留言，但是因为本人并不精通这些，这篇文章只是分享经验，所以只能回答一些力所能及的问题**
