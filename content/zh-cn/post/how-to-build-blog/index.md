---
title: "如何快速创建一个博客"
description: 从零开始的 GitHub Page + Hugo 简易博客打造教程
slug: "how-to-build-blog"
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

## 前提条件

* 一个 [GitHub](https://github.com) 账户
* 一台电脑 （因为我个人比较推荐本地跑一下网站 Demo 而不是在线编辑）
* 能阅读英文（或者会使用翻译软件）
* 电脑基础知识（会使用命令行，了解基础 GitHub 操作）

## 开始

首先，如果你不是一个前端开发人员，或者你不想重新造轮子，你可以在 Hugo 的官方网站上寻找你满意的主题。

Hugo 的网站上有许多好看可用的 [博客主题](https://themes.gohugo.io/tags/blog/)，我个人觉得比较可以的是以下四个（以 Star 数从多到少）：

* [PaperMod](https://themes.gohugo.io/themes/hugo-papermod)
* [Stack](https://themes.gohugo.io/themes/hugo-theme-stack)
* [Paper](https://themes.gohugo.io/themes/hugo-paper)
* [TailWind](https://themes.gohugo.io/themes/hugo-theme-tailwind)

此博客使用 Stack 主题构建，因此以下主要以 Stack 主题的项目文件结构来进行讲解

## 创建仓库

因为需要使用 GitHub Page 来部署博客，所以我们需要先创建一个 GitHub 仓库。

一般来说会选择创建一个 `GitHub用户名.github.io` 名称的仓库作为个人博客的地址。例: `lxymahatma.github.io`

许多 Hugo 主题（比如 Stack）提供了一个 [仓库模板](https://github.com/CaiJimmy/hugo-theme-stack-starter) 专门用来创建新的仓库，这里分成两种情况进行讨论

### 传统方式（无 generated from template 显示）

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

### 简单版本（新手推荐！）

* 打开仓库模板的页面，可以根据 ReadMe 的内容进行操作。
* 如果想要本地构建网站，执行完第一步之后就可以了
* 把创建好的仓库克隆到本地（可以使用命令行 `git clone` 或者直接使用 GitHub Desktop）

{{<notice tip>}}
进入仓库的设置页面后点击 `Pages` 即可看到你的博客网页地址，可以复制记下来以便之后需要用到
{{</notice>}}

## 本地环境配置以及本地网站

{{<notice info>}}
此篇文章针对 Windows 环境编写，因此路径分隔符均为 `\`， 如果使用 macOS 或者 Linux 需要将路径分隔符替换为 `/`
{{</notice>}}

* 根据 [Hugo 官方文档](https://gohugo.io/installation) 进行配置
* 下载安装 Git, Go, Dart Sass 以及 Hugo Extended
* 使用命令行进入到你克隆下来的仓库文件夹下，运行 `hugo server`，即可看到 Hugo 提示
`Web Server is available at <http://localhost:1313/> (bind address 127.0.0.1)`
* 按住 Ctrl 点击链接即可在默认浏览器里打开网页
* 网页会根据本地文件修改自动热重载，因此非常好用，强烈建议本地部署方便修改预览！

## 修改配置

{{<notice info>}}
注意：此处配置文件都使用 Stack 主题模板的 toml 文件，如果你不熟悉 toml 语法，可以通过 [toml 官方网站](https://toml.io/cn/v1.0.0) 学习, 也可以使用 yaml 或者 json
{{</notice>}}

### 基础配置

#### `config.toml`

* `baseurl`: 博客网页地址
* `languageCode`: Hugo 用来填充内置 RSS 模板中的语言元素，一般来说写成和网页语言一致即可
* `paginate`: 博客主页每一页可以显示多少篇文章
* `title`: 博客的标题
* `defaultContentLanguage`: 默认网页语言（`zh-cn`）
* `hasCJKLanguage`: 如果有使用中文（那肯定啊）就设置为 `true`
* `disqusShortname`: 评论系统的设置，只有用 disqus 作为评论系统的需要设置

#### `menu.toml`

这个文件是用来设置你的左侧侧边栏的，但是根据 [Stack 文档的建议](https://stack.jimmycai.com/config/menu)，最好不要通过这个文件来设置，而是通过 [此方法](#左侧边栏设置) 来进行设置。
因此此项里只讲述如何设置侧边栏上的图标

* `[[social]]` 代表了一个 `social` 数组，参考原模板进行修改即可
* `identifer`: 内部识别使用的标识符，需要唯一
* `name`: 用户把鼠标悬浮在按钮上后显示出的字
* `url`: 用户点击按钮后跳转的链接
* `params.icon`: 按钮图标

{{<notice note>}}
如果你想要的图标并没有内置，Hugo 会提醒你需要添加对应图片。
可参考 [Stack 文档](https://stack.jimmycai.com/config/menu#add-custom-icon)，将图片添加到 `assets\icons` 下即可。
{{</notice>}}

#### `params.toml`

因为里面可以设置的东西实在太多，有些内容会在之后提到，因此只讲一些比较重要的内容：

* `mainSections`: 放在此文件夹底下的文章会被发布到网站上
* `footer.since`: 页脚，这个网站是从哪一年开始的
* `widgets`: 电脑端的主页右侧部分内容，具体设置可以参考 [Stack 文档](https://stack.jimmycai.com/config/widgets)

### 多语言配置

首先你需要决定你的个人博客是否需要多语言支持，如果不需要，你可以直接跳到下一小节。

Hugo 有内置的多语言配置，而 Stack 主题也提供了 [方法](https://stack.jimmycai.com/config/i18n)，此教程根据 Hugo 官方内置配置模板进行教学。

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

我把 `params.toml` 里的这两个配置给删除并且设置了多语言，如果不需要的话也可以不修改

## 图片修改

* 头像的修改是在 `assets\img\avatar.png`，把这个图片替换成你想要的头像就行
  * 如果你的图片类型不是 `.png` 或者你不想起名叫 `avatar.png`，找到 `params.toml` 中的

    ```toml
    [sidebar.avatar]
    enabled = true
    local = true
    src = "img/avatar.png"
    ```

    将 src 修改为你的图片路径即可

* 网站图标的修改是在 `static\favicon.png`，把这个图片替换成你想要的网站图标
  * 如果你的图片类型不是 `.png` 或者你不想起名叫 `favicon.png`，找到 `params.toml` 中的

    ```toml
    favicon = "/favicon.png"
    ```

    将 favicon 修改为你的图片路径即可

* 其他任意图片，如果是使用在 `icon` 属性里，那么都是将图片放入到 `assets\icons` 里即可

## 左侧边栏设置

{{<notice info>}}
此小节内，`content` 文件夹代指你设置的对应 `contentDir` 文件夹（如果没有设置多语言那么就是 `content` 文件夹）
{{</notice>}}

如果你已经成功克隆了仓库，那么你的 `content` 文件夹底下已经有几个例子了，因此只是简单解释一下已有的例子并且赘述一下如何创建更多的栏目

### 例子解释

在 `content` 文件夹下有名为 `_index.md` 的文件：

{{<notice example>}}

```yaml
---
menu:
    main:
        name: 主页
        weight: 1
        params:
            icon: home
---
```

{{</notice>}}

其中，`weight` 设置为 1 表示将这个按钮放到左侧边栏最上方，`icon` 设置为 `home` 就可以使用默认的主页图标

在 `content\page` 文件夹下有 `archives` 和 `search` 的文件夹，里面分别带有 `index.md`，
和主页的 `_index.md` 的唯一区别就是多了一项 `layout` 设置，里面不同名称的 `layout` 是默认实现的功能

### 创建新栏目

在 `content\page` 文件夹下创建一个新的文件夹，起名为你想要的按钮名字

{{<notice warning>}}
不要重命名 `page` 文件夹！

如果文件夹名字不为 `page`，可能会造成有些功能无法使用（搜索）
{{</notice>}}

在新的文件夹内添加 `index.md` 文件，根据 home 的模板修改即可

## 分类与标签设置

{{<notice info>}}
此小节内，`content` 文件夹代指你设置的对应 `contentDir` 文件夹（如果没有设置多语言那么就是 `content` 文件夹）
{{</notice>}}

### 分类

* 在 `content` 文件夹下创建一个名为 `categories` 的文件夹，在里面创建一个新的文件夹，起名为你想要的分类名
* 在新文件夹里创建一个名为 `_index.md` 的 Markdown 文件，根据以下模板进行修改即可

{{<notice example>}}

```yaml
---
title: Example Category
description: A description of this category
image:

style:
    background: "#2a9d8f"
    color: "#fff"
---
```

{{</notice>}}

参数含义：

* `title`: 分类的名称，在主页中通过点击文章的分类标签会进入到具体的分类页面
* `description`: 分类的描述，在具体分类页面显示
* `image`: 分类的封面图片，在具体分类页面显示
* `style`: 设置文章在主页里显示的时候，分类勋章的颜色。
  * `background`: 背景色
  * `color`: 文字颜色。

### 标签

* 在 `content` 文件夹下创建一个名为 `tags` 的文件夹，在里面创建一个新的文件夹，起名为你想要的标签名
* 在新文件夹里创建一个名为 `_index.md` 的 Markdown 文件，根据以下模板进行修改即可

{{<notice example>}}

```yaml
---
title: Example Category
description: A description of this category
image:
---
```

{{</notice>}}

{{<notice note>}}
标签和分类唯一的区别就是不能自定义勋章的颜色。

但同时，通过 `widgets` 设置的右侧栏目并不会显示分类的自定义颜色
{{</notice>}}

## 创建文章模板

根据 [Hugo 官方文档](https://gohugo.io/content-management/archetypes)，有两种模板创建方式：

1. 单 Markdown 文件形式
2. 文件夹形式

两种方法都需要在根目录底下创建一个名为 `archetypes` 的新文件夹

### 单 Markdown 文件形式（不推荐）

* 在 `archetypes` 文件夹底下创建一个名为 `default.md` 的 Markdown 文件，里面的内容参考以下模板（官方）：

{{<notice example>}}

```yaml
---
date: '{{ .Date }}'
draft: true
title: '{{ replace .File.ContentBaseName `-` ` ` | title }}'
---
```

{{</notice>}}

* `date`: 文章创建日期
* `draft`: 文章是否是草稿，如果是草稿则不会发布到网站上
* `title`: 这一串东西是把文件名中的 `-` 给替换成空格，赋值给 `title`

设置完之后，就可以通过 `hugo new content post/my-first-post.md` 在 post 文件夹下创建一个新的文件。但是因为前面设置，只有在文件夹里的文章会被正确加载，还需要再套一层文件夹才能正常使用。

### 文件夹形式 （推荐）

* 在 `archetypes` 文件夹底下创建一个名为 `post` 的文件夹，里面添加一个名为 `index.md` 的 Markdown 文件。
下面是我的模板：

{{<notice example>}}

```yaml
---
title: "{{ replace .File.ContentBaseName "-" " " | humanize | title }}"
description: 
slug: "{{ .Name }}"
date: {{ .Date | time.Format "2006-01-02"}}
categories:
    - Category
tags:
    - Tag1
    - Tag2
    - Tag3
---

```

{{</notice>}}

* `title`: 使用了 humanize 函数让标题更加可读
* `description`: 文章内容概述
* `slug`: 文章的辨识符
* `date`: 文章创建日期，但是只包含年月日
* `categories`: 文章的分类
* `tags`: 文章的标签

设置完之后，就可以通过 `hugo new content post/my-first-post` 在 post 文件夹下创建一个新的文件夹，将你想要的文章内容写入 `index.md` 即可。

## 小细节（踩坑）

* 在 `config.toml` 中, 可以添加一项 `timeZone = "Asia/Shanghai"`。这个设置的目的是让 Hugo 在构建你的网站的时候，会根据设定的时区来确定是否发布对应的文章。

在默认情况下，Hugo 会使用构建时候的电脑时区来判断当前时间，但是有些情况下也会使用 UTC +0 的时区来进行判断。因此，如果你把你的网站内容推送到 Github 进行构建，当你的时间已经是下一天的时候，Hugo 获取的时间可能还是前一天，所以推送的文章并不会被发表。

## 添加评论系统

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

## 最后的推送与设置

当以上设置都结束之后，可以将所有修改内容都重新推送到 GitHub 仓库里。如果在创建仓库的步骤里使用了模板或者复制了 `.github` 文件夹的话，此时 GitHub Action 应该会尝试部署网站。

但是！还有最重要的一步没有做：
默认的 GitHub workflow 的最后一个 step 是把所有生成出来的东西重新给推送到 `gh-pages` 这个分支上，因此我们需要多做一步。

* 进入仓库的设置页面，选择 `Pages`
* 在 `Build and deployment` 中，`Source` 选择 `Deploy from a branch`，Branch 选择 `gh-pages`，路径选择 `/(root)`
* 点击 `Save`

**以上，大功告成了！稍微等待一会再进入你的网页应该就能看到你的博客已经成功部署在 GitHub Pages 上了！**

## 感谢名单

* [CaiJimmy](https://github.com/CaiJimmy) 制作了 Hugo 的 Stack 主题
* [十月的寒流](https://github.com/BYJRK) 的个人博客仓库在我尝试做自己的博客的时候提供了很多模板帮助

**感谢你看到这里，如果有任何关于文章的问题可以在底下评论区留言，但是因为本人并不精通这些，这篇文章只是分享经验，所以只能回答一些力所能及的问题**

~~记得看完发个表情或者发个评论（不是）~~
