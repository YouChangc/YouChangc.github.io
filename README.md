# Hugo 博客使用说明

这个项目是一个基于 [Hugo](https://gohugo.io/) 搭建的静态博客，主题使用的是 [Blowfish](https://themes.gohugo.io/themes/blowfish/)。

如果你不熟悉 Hugo，可以先把它理解成：

- `content/` 里放文章和页面
- `config/_default/` 里放博客配置
- `themes/blowfish-theme/` 是主题代码
- `public/` 是 Hugo 生成出来的静态网站文件

你平时最常做的事，其实只有 3 个：

1. 写文章
2. 改配置
3. 本地预览后发布

## 目录结构

当前项目里最重要的目录和文件如下：

```text
Blog/
├── archetypes/
│   └── default.md                  # 新建文章时使用的默认模板
├── config/
│   └── _default/
│       ├── hugo.toml               # Hugo 基础配置
│       ├── params.toml             # Blowfish 主题配置
│       ├── languages.zh-cn.toml    # 中文站点标题、作者、描述
│       ├── menus.zh-cn.toml        # 顶部和底部菜单
│       └── markup.toml             # Markdown 渲染配置
├── content/
│   ├── _index.md                   # 首页内容
│   ├── about/
│   │   └── index.md                # 关于页
│   └── posts/
│       ├── _index.md               # 文章列表页
│       └── hello-blowfish/
│           └── index.md            # 示例文章
├── static/                         # 原样拷贝到网站根目录的静态资源
├── themes/
│   └── blowfish-theme/             # Blowfish 主题
└── public/                         # Hugo 生成后的静态文件
```

## 先学会这几个命令

在项目根目录 `/Users/youc/Desktop/Blog` 下运行：

```bash
hugo server -D
```

作用：

- 启动本地预览服务
- 默认地址是 `http://localhost:1313`
- 改完文件后会自动刷新
- `-D` 表示连草稿文章也一起显示

生成正式网站：

```bash
hugo
```

生成后的文件会放到 `public/` 目录。

## 怎么新增一篇博客

最简单的方法是用 Hugo 命令创建：

```bash
hugo new content posts/my-first-post/index.md
```

执行后会生成一个新文件：

[`content/posts/my-first-post/index.md`](/Users/youc/Desktop/Blog/content/posts/my-first-post/index.md)

你可以把它改成这样：

```md
---
title: "我的第一篇文章"
date: 2026-03-12T18:00:00+08:00
draft: false
description: "这是一篇测试文章。"
tags: ["随笔", "Hugo"]
categories: ["博客"]
---

这里开始写正文。
```

几个最重要的字段：

- `title`: 文章标题
- `date`: 发布时间
- `draft`: 是否为草稿，`true` 不会出现在正式构建里
- `description`: 文章摘要
- `tags`: 标签
- `categories`: 分类

## 怎么修改一篇博客

直接编辑对应文件就可以。

例如现在这篇示例文章在这里：
[content/posts/hello-blowfish/index.md](/Users/youc/Desktop/Blog/content/posts/hello-blowfish/index.md)

你可以修改：

- 标题
- 日期
- 正文内容
- 标签和分类
- `draft` 状态

改完后，如果本地正在运行 `hugo server -D`，浏览器会自动刷新。

## 怎么删除一篇博客

Hugo 没有特殊删除命令，直接删文章目录即可。

例如删除示例文章：

```bash
rm -rf content/posts/hello-blowfish
```

为什么是删整个目录而不是只删 `index.md`？

- Hugo 很常见的写法是“文章一个文件夹”
- 这样以后你可以把文章配图也放进同一个目录

如果你不想真的删掉，也可以先把文章改成草稿：

```md
draft: true
```

这样本地预览还能看到，但正式执行 `hugo` 时不会发布。

## 怎么更新博客内容

“更新博客”通常有 3 种情况：

### 1. 更新文章正文

直接改 `content/` 下面的文章文件。

例如：
[content/posts/hello-blowfish/index.md](/Users/youc/Desktop/Blog/content/posts/hello-blowfish/index.md)

### 2. 更新首页或关于页

对应文件分别是：

- 首页：[content/_index.md](/Users/youc/Desktop/Blog/content/_index.md)
- 关于页：[content/about/index.md](/Users/youc/Desktop/Blog/content/about/index.md)

### 3. 更新网站信息

常见修改位置：

- 网站标题、作者、描述：
  [config/_default/languages.zh-cn.toml](/Users/youc/Desktop/Blog/config/_default/languages.zh-cn.toml)
- 主题外观、首页布局、文章显示方式：
  [config/_default/params.toml](/Users/youc/Desktop/Blog/config/_default/params.toml)
- 顶部/底部菜单：
  [config/_default/menus.zh-cn.toml](/Users/youc/Desktop/Blog/config/_default/menus.zh-cn.toml)

## 最常改的几个配置

### 改博客标题和作者

编辑：
[config/_default/languages.zh-cn.toml](/Users/youc/Desktop/Blog/config/_default/languages.zh-cn.toml)

重点看这几个字段：

```toml
title = "Youc 的博客"

[params.author]
  name = "youc"
  headline = "记录技术、写作与日常思考。"
  bio = "欢迎来到我的博客，这里会持续更新开发笔记、项目实践和一些值得保存下来的想法。"
```

### 改首页布局和主题风格

编辑：
[config/_default/params.toml](/Users/youc/Desktop/Blog/config/_default/params.toml)

例如：

```toml
colorScheme = "blowfish"
defaultAppearance = "light"

[homepage]
  layout = "profile"
  showRecent = true
```

### 改导航菜单

编辑：
[config/_default/menus.zh-cn.toml](/Users/youc/Desktop/Blog/config/_default/menus.zh-cn.toml)

例如新增一个“友链”菜单：

```toml
[[main]]
  name = "友链"
  pageRef = "links"
  weight = 40
```

如果你新增了这个菜单，记得还要创建对应页面，比如：

[`content/links/index.md`](/Users/youc/Desktop/Blog/content/links/index.md)

## 图片应该放哪里

推荐两种放法。

### 1. 文章专属图片

放在文章目录里，和 `index.md` 同级：

```text
content/posts/my-first-post/
├── index.md
└── cover.jpg
```

正文里这样写：

```md
![封面](cover.jpg)
```

### 2. 全站通用图片

放到 `static/` 目录：

```text
static/images/avatar.png
```

页面里引用时写：

```md
![头像](/images/avatar.png)
```

## 一篇文章的标准工作流

建议你以后都按这个顺序来：

1. 新建文章

```bash
hugo new content posts/文章名/index.md
```

2. 启动预览

```bash
hugo server -D
```

3. 编辑文章内容，把 `draft` 改成 `false`

4. 确认页面显示正常

5. 生成正式文件

```bash
hugo
```

## 什么时候会看不到文章

最常见的原因有这些：

- `draft: true`
- 文章放错目录，没有放在 `content/posts/` 下
- Front Matter 格式写错
- 本地没开 `hugo server -D`

如果是正式构建后看不到，优先检查是不是还保留了：

```md
draft: true
```

## 主题怎么更新

当前主题目录是：
[themes/blowfish-theme](/Users/youc/Desktop/Blog/themes/blowfish-theme)

它本质上是一个单独的 Git 仓库。以后如果你想更新 Blowfish，可以在主题目录里执行：

```bash
git -C themes/blowfish-theme pull
```

更新后建议重新构建检查：

```bash
hugo
```

如果主题更新后样式或配置有变化，优先检查：

- [config/_default/params.toml](/Users/youc/Desktop/Blog/config/_default/params.toml)
- [config/_default/hugo.toml](/Users/youc/Desktop/Blog/config/_default/hugo.toml)

## 这个博客现在已经有哪些页面

目前已经有这些内容：

- 首页：[content/_index.md](/Users/youc/Desktop/Blog/content/_index.md)
- 关于页：[content/about/index.md](/Users/youc/Desktop/Blog/content/about/index.md)
- 文章列表页：[content/posts/_index.md](/Users/youc/Desktop/Blog/content/posts/_index.md)
- 示例文章：[content/posts/hello-blowfish/index.md](/Users/youc/Desktop/Blog/content/posts/hello-blowfish/index.md)

## 你现在最需要记住的事

如果只记 4 条，就记这 4 条：

1. 文章都写在 `content/posts/`
2. 网站配置都在 `config/_default/`
3. 本地预览用 `hugo server -D`
4. 正式生成用 `hugo`

## 常用命令速查

```bash
# 本地预览
hugo server -D

# 新建文章
hugo new content posts/my-post/index.md

# 生成正式站点
hugo

# 更新主题
git -C themes/blowfish-theme pull
```

## 发布到 GitHub Pages

项目已经内置自动部署工作流：
[`/.github/workflows/hugo.yml`](/Users/youc/Desktop/Blog/.github/workflows/hugo.yml)

你只需要做一次初始化发布：

1. 在 GitHub 新建一个仓库（建议公开仓库，方便所有人访问）。
2. 在本地项目根目录执行（把 `YOUR_NAME` 和 `YOUR_REPO` 改成你的）：

```bash
git branch -M main
git remote add origin https://github.com/YOUR_NAME/YOUR_REPO.git
git add .
git commit -m "init: hugo blog with blowfish"
git push -u origin main
```

3. 打开 GitHub 仓库页面：
`Settings` -> `Pages` -> `Build and deployment` -> `Source` 选择 `GitHub Actions`。
4. 推送完成后，等待 Actions 跑完，网站就会自动发布。

发布地址通常是：

- 用户主页仓库（仓库名是 `YOUR_NAME.github.io`）：
  `https://YOUR_NAME.github.io/`
- 普通仓库：
  `https://YOUR_NAME.github.io/YOUR_REPO/`

说明：

- 这个工作流会自动使用 GitHub Pages 的 `baseURL`，所以不需要你手动改 `config/_default/hugo.toml` 里的 `baseURL`。
- 以后每次 `git push` 到 `main`，都会自动重新发布。
