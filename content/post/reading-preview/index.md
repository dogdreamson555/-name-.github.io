---
title: "Markdown 写作示例"
date: 2020-01-02T00:00:00+08:00
slug: reading-preview
draft: false
description: "标题、代码、表格、公式和文章配图的简明示例。"
categories: ["示例"]
tags: ["Markdown", "写作"]
image: "cover.png"
---

这是一篇可以替换的示例文章。编辑此目录的 `index.md`，即可修改正文。

## 正文与列表

用 **加粗** 标记重点，用 *斜体* 补充说明，用 `行内代码` 表示命令或文件名。

- 用二级标题划分章节。
- 用三级标题补充细节。
- 发布后保持 `slug` 不变，避免已有链接失效。

> 先写清楚要表达的内容，再调整排版。

## 代码

在代码围栏后指定语言，可以启用语法高亮。

```python
def greet(name):
    return f"你好，{name}！"

print(greet("读者"))
```

## 表格与公式

| 字段 | 用途 |
| --- | --- |
| title | 文章标题 |
| description | 列表中的摘要 |
| categories | 文章分类 |
| tags | 文章标签 |

当前配置启用了数学公式，例如 $a^2 + b^2 = c^2$。

## 文章配图

将图片放在 `index.md` 所在目录，用相对路径引用：

![模板作者原创的示例封面](cover.png)

```markdown
![图片说明](cover.png)
```

使用自己的封面时，将图片放在同一目录，并把文章头部的 `image` 改为对应文件名。

文章封面最后会被裁切为 16:5 的图片比例

## Mermaid 流程图

使用标记为 `mermaid` 的代码块即可绘制流程图，无需另存图片。主题会自动加载 Mermaid。

```mermaid
flowchart LR
    A[编写 Markdown] --> B[本地预览] --> C[检查内容] --> D[发布文章]
```

[返回首页]({{< relref "/" >}})
