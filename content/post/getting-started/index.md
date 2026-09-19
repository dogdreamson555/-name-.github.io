---
title: "开始使用你的博客"
date: 2020-01-03T00:00:00+08:00
slug: getting-started
draft: false
description: "修改个人资料、创建第一篇文章，并通过 GitHub Pages 发布。"
categories: ["示例"]
tags: ["入门"]
image: ""
---

这两篇示例文章用于演示写作和排版，准备好自己的内容后可以删除对应的文章目录。

## 修改博客资料

- 部署后的博客名称自动使用 `GitHub用户名 的博客`。需要自定义时，在仓库的 Actions Variables 中设置 `BLOG_TITLE`；本地预览名称由 `config/_default/hugo.toml` 中的 `title` 控制。
- 在 `config/_default/params.toml` 中设置 `sidebar.avatar`。例如把头像放到 `assets/img/avatar.png`，再填写 `img/avatar.png`。
- 评论默认关闭。启用前请在 `config/production/params.toml` 中配置自己的评论服务。

GitHub Pages 工作流会自动设置部署网址。部署到其他平台时，请自行修改 `baseURL`。

浏览器标签页图标（favicon）会在 GitHub Pages 部署时自动使用仓库所有者的 GitHub 头像；组织仓库使用组织头像。更新头像后，重新运行部署即可更新网站图标。本地预览或头像下载失败时使用 `assets/img/favicon.svg` 备用图标。此功能不影响侧栏头像设置。

## 创建第一篇文章

在 `content/post/my-first-post/` 下创建 `index.md`，写入：

```yaml
---
title: "我的第一篇文章"
date: 2020-01-01T12:00:00+08:00
slug: my-first-post
draft: false
description: "这篇文章的简短介绍。"
categories: ["生活"]
tags: ["记录"]
image: ""
---
这里是正文。
```

把日期改为实际发布时间。当前配置不会发布草稿和未来日期的文章。

## 本地预览

安装 `.hugo-version` 指定版本的 Hugo Extended，在仓库根目录执行：

```sh
hugo server -D
```

打开终端显示的本地地址。`-D` 会在预览中包含草稿，正式发布前记得将文章的 `draft` 改为 `false`。

## 发布到 GitHub Pages

1. 从模板创建自己的公开仓库，例如 `你的用户名.github.io`。
2. 保持发布分支为 `main`，在仓库的 **Settings → Pages → Source** 中选择 **GitHub Actions**。
3. 在 **Actions** 中手动运行 **Build and deploy Hugo to Pages**。
4. 此后向 `main` 提交文章修改，工作流会自动构建并部署。

仓库使用其他名称时，网站通常位于 `https://你的用户名.github.io/仓库名/`，现有工作流会自动传入对应地址。

查看另一篇[Markdown 写作示例]({{< relref "/post/reading-preview" >}})，了解代码、公式和图片的写法。
