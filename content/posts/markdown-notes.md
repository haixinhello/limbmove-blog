---
title: "如何使用 Markdown 写博客"
date: 2026-10-17
draft: false
description: "用最少的标记，写出结构清晰的文章。"
---

Hugo 支持 Markdown，所以写文章时不需要每次都修改 HTML。

## 常见的写作格式

下面是最常用的 Markdown 语法：

```md
# 一级标题
## 二级标题
**粗体文字**
*斜体文字*

- 第一项
- 第二项

[这是一个链接](https://example.com)
```

## 下一篇文章怎么添加？

在仓库的 `content/posts/` 文件夹里创建一个新的 `.md` 文件，例如 `my-project.md`，写入：

```yaml
---
title: "我的新文章"
date: 2026-10-18
draft: false
---

这里开始写文章正文。
```

提交到 GitHub 后，Cloudflare Pages 就会自动重新部署网站。
