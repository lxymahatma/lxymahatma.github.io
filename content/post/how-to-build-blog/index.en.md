---
title: "How to Quickly Build a Blog"
description: A simple tutorial for building a blog from scratch with GitHub Pages + Hugo
slug: "how-to-build-blog"
date: 2024-06-15
lastmod: 2026-05-05
categories:
    - Tutorial
tags:
    - Hugo
    - Blog
---

I was bored recently and had nothing to do (definitely not because I had too little homework), so I figured I'd build a personal blog to write some stuff. At least it makes me look kinda cool that way (jk), and that's how this blog came to be.

After getting the basic blog up, I started wondering what to actually post. Thinking it over, I figured why not just write a tutorial about the process of building this blog itself — it's both a recap of what I did over the past few days and could potentially help others. What a wonderful thing.jpg

Without further ado, let's get started:

## Prerequisites

* A [GitHub](https://github.com) account
* A computer (because I personally recommend running the demo locally rather than editing online)
* Ability to read English (or knowing how to use translation software)
* Basic computer knowledge (can use the command line, basic GitHub operations)

## Getting Started

First, if you're not a frontend developer, or you don't want to reinvent the wheel, you can find a theme you like on Hugo's official website.

Hugo's site has many good-looking and usable [blog themes](https://themes.gohugo.io/tags/blog/). I personally think the following four are pretty solid (sorted by Star count, most to least):

* [PaperMod](https://themes.gohugo.io/themes/hugo-papermod)
* [Stack](https://themes.gohugo.io/themes/hugo-theme-stack)
* [Paper](https://themes.gohugo.io/themes/hugo-paper)
* [TailWind](https://themes.gohugo.io/themes/hugo-theme-tailwind)

This blog is built with the Stack theme, so the following content mainly walks through the project file structure of the Stack theme.

## Creating the Repository

Since we'll use GitHub Pages to deploy the blog, we need to create a GitHub repository first.

Generally, you'd create a repository named `GitHubUsername.github.io` as your personal blog's address. Example: `lxymahatma.github.io`

Many Hugo themes (like Stack) provide a [repository template](https://github.com/CaiJimmy/hugo-theme-stack-starter) specifically for creating new repositories. Two scenarios to discuss here:

### Traditional way (no "Use this template" button)

* Create a new repository directly through the GitHub web UI
* Clone both your created repository and the template repository to local (use `git clone` from the command line, or just use GitHub Desktop)
* Copy what you need from the template repository into your repository, generally these:
  * .github
  * assets
  * config
  * content
  * static
  * .gitignore
  * go.mod
  * go.sum

### Simple version (recommended for beginners!)

* Open the template repository's page and follow the ReadMe.
* If you want to build the website locally, you're done after the first step.
* If you want to use GitHub Codespace (web editing, recommended for beginners! Because environment setup is kinda annoying) you can continue with the ReadMe and skip the [Local environment setup](#local-environment-setup-and-local-website) section.
* If you want to deploy locally, clone the created repository to your machine (use `git clone` from the command line, or just GitHub Desktop)

> [!TIP]
> After entering the repository's settings page, click `Pages` to see your blog's webpage address. Worth copying it down for later.

## Local Environment Setup and Local Website

> [!IMPORTANT]
> This article is written for Windows, so path separators are `\`. If you're on macOS or Linux, replace path separators with `/`.
>
> The local setup section requires somewhat higher computer fundamentals, so the following content assumes you can read Hugo's English documentation and have some understanding of installing language environments / configuring environment variables, etc.

* Configure according to [Hugo's official docs](https://gohugo.io/installation)
* Download and install Git, Go, Dart Sass, and Hugo Extended
* Use the command line to enter your cloned repository folder, run `hugo server`, and you should see Hugo's prompt
`Web Server is available at <http://localhost:1313/> (bind address 127.0.0.1)`
* Hold Ctrl and click the link to open the page in your default browser
* The webpage will hot-reload based on local file changes, so it's super useful — strongly recommend local deployment for easier editing and previewing!

## Modifying Configuration

> [!IMPORTANT]
> Note: All configuration files here use the Stack theme template's toml files. If you're not familiar with toml syntax, you can learn from [the toml official site](https://toml.io/cn/v1.0.0). yaml or json work too.

### Basic Configuration

#### `config.toml`

* `baseurl`: Blog webpage address
* `locale`: Hugo uses this to populate the language element in the built-in RSS template. Generally, write it the same as the webpage language.
* `[pagination] pagerSize`: How many articles can show per page on the blog homepage
* `title`: Blog title
* `defaultContentLanguage`: Default webpage language (`zh`)
* `hasCJKLanguage`: If you use Chinese (which obviously you do) set it to `true`
* `disqusShortname`: Comment system setting, only those using disqus as the comment system need to set this

#### `menu.toml`

This file is used to configure your left sidebar, but per [Stack's documentation recommendation](https://stack.jimmycai.com/config/menu), it's best not to configure through this file, but rather through [this method](#left-sidebar-setup).
So this section only describes how to set the icons on the sidebar.

* `[[social]]` represents a `social` array; refer to the original template for modifications
* `identifier`: Internal identifier, must be unique
* `name`: The text shown when users hover over the button
* `url`: The link users navigate to when clicking the button
* `params.icon`: Button icon

> [!NOTE]
> If the icon you want isn't built-in, Hugo will remind you to add the corresponding image.
> Refer to [Stack documentation](https://stack.jimmycai.com/config/menu#add-custom-icon), just add the image to `assets\icons`.

#### `params.toml`

There's really too much to set in here. Some content will be mentioned later, so I'll only cover the more important parts:

* `mainSections`: Articles placed under this folder will be published to the website
* `footer.since`: Footer, the year this website started
* `widgets`: The right side content of the homepage on desktop. Refer to [Stack documentation](https://stack.jimmycai.com/config/widgets) for specific settings.

### Multilingual Configuration

First you need to decide whether your personal blog needs multilingual support. If not, skip directly to the next section.

Hugo has built-in multilingual configuration, and the Stack theme also provides [methods](https://stack.jimmycai.com/config/i18n). This tutorial teaches based on Hugo's official built-in configuration template.

Hugo officially provides two configuration methods:

1. Set `contentDir` via `languages.toml` to set different folders for storing articles for each language
2. Add the corresponding language code as a suffix to the article filename, place them in the same folder, and let Hugo handle them automatically.

#### General Settings

* Enter the `config\_default` folder, find and rename `_languages.toml` to `languages.toml`, open the file
* Then, configure according to [Hugo's official documentation](https://gohugo.io/content-management/multilingual)
  * Since the file name is already `languages.toml`, you don't need to write `[languages.en]` form, just write `[en]` like the existing one
  * You can refer to [my configuration](languages-example.toml) for modifications

Here's a brief explanation of what each item in my configuration represents:

* `label`: The language name displayed in the language switcher dropdown
* `direction`: Language reading direction (left-to-right)
* `title`: Blog title
* `weight`: Sorting weight in the dropdown — higher values go to the bottom

And `[params]` are configurations from `params.toml`

* `sidebar.subtitle`: Blog subtitle
* `article.license.default`: License at the bottom of articles

I deleted these two configurations from `params.toml` and set them per-language. If you don't need this you can leave them alone.

#### Setting contentDir (slightly more complex version)

* In `languages.toml`, add `contentDir = "xxx"` under each language config (generally `content/en`, `content/zh`, etc.)
* `contentDir` sets the folder where blog article content is placed. Just put the corresponding articles in the corresponding language folder, and you can publish different language content.

#### Modify Filename (simple version)

* Before changing to multilingual, each article folder has an `index.md` Markdown file. Add the language code you use to the filename (e.g., for English it's `en`, for Simplified Chinese it's `zh`)
* The modified filenames should be `index.en.md` and `index.zh.md`
* In this case, Hugo will automatically handle the relationship between Chinese and English articles, so it's relatively simple

## Image Modifications

* Avatar modification is at `assets\img\avatar.png`. Just replace this image with the avatar you want.
  * If your image type is not `.png` or you don't want to name it `avatar.png`, find this in `params.toml`:

    ```toml
    [sidebar]
        avatar = "img/avatar.png"
    ```

    Modify avatar to your image path (path is relative to `assets`).

* Website favicon modification is at `assets\img\favicon.png`. Just replace this image with the favicon you want.
  * If your image type is not `.png` or you don't want to name it `favicon.png`, find this in `params.toml`:

    ```toml
    favicon = "img/favicon.png"
    ```

    Modify favicon to your image path (path is relative to `assets`).

* For any other images, if used in the `icon` attribute, just put the image into `assets\icons`.

> [!TIP]
> The Stack theme has built-in svg files for some icons that can be accessed directly via filename, like `brand-github`, `user`, etc.
> See [here](https://github.com/CaiJimmy/hugo-theme-stack/tree/master/assets/icons) for details.

## Left Sidebar Setup

> [!IMPORTANT]
> In this section, if you've set the `contentDir` folder variable, then `content` folder refers to your set corresponding `contentDir` folder.

If you've successfully cloned the repository, then there are already a few examples under your `content` folder. So I'll just briefly explain the existing examples and elaborate on how to create more sections.

### Example explanation

There's a file named `_index.md` under the `content` folder:

> [!NOTE]
> Example:
>
> ```yaml
> ---
> menu:
>     main:
>         name: Home
>         weight: 1
>         params:
>             icon: home
> ---
> ```

Here, setting `weight` to 1 puts this button at the top of the left sidebar, and setting `icon` to `home` uses the default home icon.

Under the `content\page` folder, there are `archives` and `search` folders, each containing an `index.md`. The only difference from the homepage's `_index.md` is the addition of a `layout` setting. Different `layout` names have default implementations.

### Creating new sections

Create a new folder under `content\page`, naming it whatever button name you want.

> [!WARNING]
> Don't rename the `page` folder!
>
> If the folder name is not `page`, some features may not work (search)

Add an `index.md` file in the new folder, modifying based on the home template.

## Categories and Tags Setup

> [!IMPORTANT]
> In this section, if you've set the `contentDir` folder variable, then `content` folder refers to your set corresponding `contentDir` folder.

### Categories

* Create a folder named `categories` under the `content` folder. Inside it, create a new folder with your desired category name.
* Create a Markdown file named `_index.md` in the new folder, modify based on the following template:

> [!NOTE]
> Example:
>
> ```yaml
> ---
> title: Example Category
> description: A description of this category
> image:
>
> style:
>     background: "#2a9d8f"
>     color: "#fff"
> ---
> ```

Parameter meanings:

* `title`: Category name. Clicking the article's category badge on the homepage takes you to the specific category page.
* `description`: Category description, shown on the specific category page
* `image`: Cover image of the category, shown on the specific category page
* `style`: Sets the color of the category badge when articles are displayed on the homepage.
  * `background`: Background color
  * `color`: Text color.

### Tags

* Create a folder named `tags` under the `content` folder. Inside it, create a new folder with your desired tag name.
* Create a Markdown file named `_index.md` in the new folder, modify based on the following template:

> [!NOTE]
> Example:
>
> ```yaml
> ---
> title: Example Category
> description: A description of this category
> image:
> ---
> ```

> [!NOTE]
> The only difference between tags and categories is that you can't customize the badge color.
>
> But at the same time, the right sidebar set via `widgets` doesn't display the category's custom color either.

## Creating Post Archetypes

According to [Hugo's official documentation](https://gohugo.io/content-management/archetypes), there are two ways to create archetypes:

1. Single Markdown file form
2. Folder form

Both methods require creating a new folder named `archetypes` under the root directory.

### Single Markdown file form (not recommended)

* Create a Markdown file named `default.md` under the `archetypes` folder. Refer to the following template (official) for the content:

> [!NOTE]
> Example:
>
> ```yaml
> ---
> date: '{{ .Date }}'
> draft: true
> title: '{{ replace .File.ContentBaseName `-` ` ` | title }}'
> ---
> ```

* `date`: Article creation date
* `draft`: Whether the article is a draft. If it's a draft, it won't be published to the website.
* `title`: This bit replaces `-` in the filename with spaces and assigns the result to `title`

After setting this up, you can use `hugo new content post/my-first-post.md` to create a new file under the post folder. But because of the previous setting, only articles inside folders are loaded correctly, so you need to wrap it in another folder for it to work properly.

### Folder form (recommended)

* Create a folder named `post` under the `archetypes` folder, and add a Markdown file named `index.md` inside it.
Below is my template:

> [!NOTE]
> Example:
>
> ```yaml
> ---
> title: "{{ replace .File.ContentBaseName "-" " " | humanize | title }}"
> description:
> slug: "{{ .Name }}"
> date: {{ .Date | time.Format "2006-01-02"}}
> categories:
>     - Category
> tags:
>     - Tag1
>     - Tag2
>     - Tag3
> ---
>
> ```

* `title`: Used the humanize function to make the title more readable
* `description`: Article content overview
* `slug`: Article identifier
* `date`: Article creation date, only includes year, month, day
* `categories`: Article categories
* `tags`: Article tags

After setting this up, you can use `hugo new content post/my-first-post` to create a new folder under the post folder. Just write the article content you want into `index.md`.

## Small Details (Pitfalls)

* In `config.toml`, you can add an entry `timeZone = "Asia/Shanghai"`. The purpose of this setting is to let Hugo determine whether to publish a corresponding article based on the set time zone when building your website.

By default, Hugo uses the computer's time zone at build time to determine the current time, but in some cases it also uses UTC +0 for judgment. So if you push your website content to GitHub for building, when your local time is already the next day, the time Hugo gets might still be the previous day, so the pushed article won't be published.

## Adding a Comment System

The last step is adding a comment system to the blog. This blog chose [giscus](https://lxymahatma.github.io/).
We won't go into the basic setup of giscus, just talk about how to set it up in your personal blog:

* Copy the script from giscus's `Enable giscus` section
* Delete `disqusShortname = "hugo-theme-stack"` from `config.toml`
* In `params.toml`, you can see:

    ```toml
    ## Comments
    [comments]
    enabled = true
    provider = "disqus"
    ```

    Set `provider` to `"giscus"`

* Scrolling down further you can see:

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

    Now fill in the information from the copied script. For `lightTheme` and `darkTheme`, if you're lazy you can just fill in `light` and `dark`.

## Final Push and Setup

When all the above settings are done, you can push all the changes back to the GitHub repository. If you used a template or copied the `.github` folder during the repository creation step, GitHub Action should now try to deploy the website.

But! There's still one most important step left:
The default GitHub workflow's last step is pushing all the generated stuff to the `gh-pages` branch, so we need one more step.

* Enter the repository's settings page and select `Pages`
* Under `Build and deployment`, set `Source` to `Deploy from a branch`, choose `gh-pages` as the Branch, and `/(root)` as the path
* Click `Save`

**And that's it! Mission accomplished! Wait a bit and then go to your webpage — you should see your blog has been successfully deployed on GitHub Pages!**

## Acknowledgments

* [CaiJimmy](https://github.com/CaiJimmy) for making the Hugo Stack theme
* [十月的寒流](https://github.com/BYJRK)'s personal blog repository provided a lot of template help when I was trying to make my own blog

**Thanks for reading this far! If you have any questions about this article, leave a comment below. But since I'm not exactly an expert in this stuff and this article is just sharing experience, I can only answer questions within my abilities.**

~~Remember to drop an emoji or comment after reading (jk)~~
