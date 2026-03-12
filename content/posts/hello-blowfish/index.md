---
title: "第一篇文章：Hugo + Blowfish 已就绪"
date: 2026-03-12T17:30:00+08:00
draft: false
description: "这个站点已经基于 Hugo 搭建完成，并启用了 Blowfish 主题。"
tags: ["Hugo", "Blowfish", "博客"]
categories: ["建站"]
---

博客已经搭好了。

你现在可以直接使用下面这些命令继续写内容：

```bash
hugo server -D
hugo new content posts/my-next-post/index.md
hugo
```

如果你想继续个性化这个博客，通常会从下面几处开始：

1. 修改站点标题和作者信息：`config/_default/languages.zh-cn.toml`
2. 调整 Blowfish 外观与首页布局：`config/_default/params.toml`
3. 增减导航菜单：`config/_default/menus.zh-cn.toml`

接下来，写下你的第一篇真正的文章就可以了。
