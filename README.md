# Hugo 博客模板

基于 [Hugo](https://gohugo.io/) 和 [Stack](https://github.com/CaiJimmy/hugo-theme-stack) 的中文博客模板。通过 GitHub Pages 自动部署，支持文章分类、标签、归档、搜索、目录、数学公式和 Mermaid 流程图。

主题源码已包含在仓库中，无需初始化 Git 子模块。只通过 GitHub 网页编辑内容也可以完成发布，无需在电脑上安装 Hugo。

## 创建并部署自己的博客

1. 在模板仓库首页点击 **Use this template → Create a new repository**，创建自己的公开仓库。
2. 填写仓库名称：
   - `你的用户名.github.io`：网站地址为 `https://你的用户名.github.io/`。
   - 其他名称，例如 `blog`：网站地址为 `https://你的用户名.github.io/blog/`。
3. 在新仓库的 **Settings → Pages → Build and deployment → Source** 中选择 **GitHub Actions**。仓库已包含工作流，无需再创建一个。
4. 打开 **Actions → Build and deploy Hugo to Pages → Run workflow**，选择 `main` 并运行。
5. 等待 `build` 和 `deploy` 成功，从部署记录或 **Settings → Pages** 打开网站。

以后向 `main` 提交修改，网站就会自动更新。当前工作流监听 `main`；如果更换发布分支，请同步修改 [.github/workflows/pages.yml](.github/workflows/pages.yml) 的触发分支。

部署时会自动读取 GitHub Pages 的实际地址，无需手动替换工作流中的用户名或仓库名。创建仓库后仍需完成一次上述 Pages 设置。

## 修改博客资料

| 内容 | 修改位置 |
| --- | --- |
| 本地预览名称、菜单、时区 | [config/_default/hugo.toml](config/_default/hugo.toml) |
| 侧栏头像、目录、阅读时间、日期格式 | [config/_default/params.toml](config/_default/params.toml) |
| 正式部署的评论配置 | [config/production/params.toml](config/production/params.toml) |
| 自定义样式 | [assets/scss/custom.scss](assets/scss/custom.scss) |
| 示例文章 | [content/post/](content/post/) |

GitHub Pages 部署时，博客名称自动设为 `GitHub用户名 的博客`（组织仓库使用组织账号名），同步用于首页标题、侧栏、页脚和站点元数据。文章页仍使用文章自己的标题。

需要自定义线上名称时，在仓库 **Settings → Secrets and variables → Actions → Variables** 中添加仓库变量 `BLOG_TITLE`。本地预览名称由 `hugo.toml` 中的 `title` 控制。

侧栏头像配置留空时，自动使用部署下载的 GitHub 头像。自定义头像优先：可以将头像放在 `assets/img/avatar.png`，然后修改已有的 `[sidebar]` 配置：

```toml
[sidebar]
  avatar = "img/avatar.png"
```

### 网站图标

GitHub Pages 部署时会下载**仓库所有者的 GitHub 头像**，生成透明背景的圆形 SVG favicon；组织仓库使用组织头像。头像嵌入 SVG 并作为本地资源随网站发布，访客无需向 GitHub 请求图片。

修改 GitHub 头像后，重新运行部署即可更新 favicon 和默认侧栏头像，两者共用一次下载。下载失败时和本地预览时，favicon 使用 [assets/img/favicon.svg](assets/img/favicon.svg) 备用图标，侧栏仅在配置了自定义头像时显示头像。

### 评论

评论默认关闭。需要评论时，在 `config/production/params.toml` 中填写自己的评论服务配置，再将 `[comments]` 的 `enabled` 改为 `true`。例如使用 Giscus 时，需要配置自己的仓库、仓库 ID 和讨论分类 ID，不能只打开开关。

## 写第一篇文章

在 `content/post/my-first-post/` 下创建 `index.md`：

```markdown
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

将日期替换为实际发布时间。正式构建不会发布 `draft: true` 或未来日期的文章。`slug` 决定文章地址，例如 `/p/my-first-post/`，发布后建议保持不变。

配图放在同一目录中，用 `![图片说明](photo.png)` 引用；将头部的 `image` 设置为 `photo.png` 即可用作封面。

模板提供两篇可直接编辑的示例：

- [开始使用你的博客](content/post/getting-started/index.md)
- [Markdown 写作示例](content/post/reading-preview/index.md)：含代码、表格、公式、图片和 Mermaid 流程图。

两篇示例互不依赖，可以独立删除任意示例目录，再添加自己的文章。保留 `content/page/` 中的归档、搜索和分类页面。

## 本地预览（可选）

安装 [.hugo-version](.hugo-version) 指定版本的 **Hugo Extended**，当前为 `0.165.0`。克隆自己的仓库后，在仓库根目录运行：

```sh
hugo server -D
```

打开终端显示的本地网址。`-D` 会包含草稿；如果还需要预览未来日期文章，可以使用 `hugo server -D -F`。

生成正式构建：

```sh
hugo --environment production --minify --baseURL https://YOUR_USERNAME.github.io/
```

把示例网址替换为自己的实际网址；项目站点需包含仓库路径，例如 `https://YOUR_USERNAME.github.io/blog/`。生成结果位于 `public/`，无需提交。GitHub Actions 会自行构建和上传网站。

## 常见问题

**首次部署失败**：确认已将 Pages 的 Source 设置为 GitHub Actions，然后重新运行工作流，在 Actions 中查看失败步骤的日志。

**文章没有出现**：检查 `draft`、发布日期以及是否提交到了 `main`，再确认最新部署是否成功。

**本地构建提示找不到文章**：检查自己添加的 `relref` 链接是否指向已删除或改名的文章。

**更换 Hugo 版本**：需同步更新 `.hugo-version` 和工作流中的 `HUGO_SHA256`。后者对应官方 Hugo Extended Linux amd64 发布包的 SHA-256 校验值。

## 许可与来源

原创模板代码及示例内容采用 [GPL-3.0-only](LICENSE)。第三方组件保留各自的版权与许可，来源和署名见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
