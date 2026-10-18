# LimbMove Blog — Hugo + GitHub + Cloudflare Pages

这是一个无需下载主题、无需 Node.js 的轻量 Hugo 个人博客源码，目标域名是 `https://blog.limbmove.com/`。

## 上传到 GitHub（推荐第一次使用网页操作）

1. 访问 https://github.com/new 新建名为 `limbmove-blog` 的仓库。建议选 **Public**，不要勾选 `Add a README file`（压缩包已经包含）。
2. **解压本 ZIP**，进入 `limbmove-blog-hugo` 文件夹，上传文件夹**里面的所有文件和文件夹**到 GitHub 仓库根目录（不是上传 ZIP 原文件，也不要额外包一层文件夹）。
3. 上传成功后，GitHub 仓库首页应该能直接看到 `hugo.toml`、`layouts`、`content`、`static` 和 `README.md`。

## Cloudflare Pages 部署

1. 登录 Cloudflare > Workers & Pages > Create application > Pages > Connect to Git。
2. 授权 GitHub，选择 `limbmove-blog` 仓库，生产分支 `main`。
3. Build command: `hugo --minify`。
4. Build output directory: `public`。
5. 环境变量 `HUGO_VERSION` 设为 `0.158.0`（生产和预览环境推荐一致）。
6. 点击 Save and Deploy；成功后先测试 `你的项目名.pages.dev`。
7. Pages 项目 > Custom domains > Set up a domain > 输入 `blog.limbmove.com`。
8. 如果 DNS 不在 Cloudflare 管理，在当前 DNS 服务商创建 CNAME：`blog` → `你的项目名.pages.dev`。先绑定域名再按提示加 DNS 记录。不要更改主域名的 A/AAAA/MX 记录或 NS，避免影响已有网站和邮件。

官方部署文档：https://developers.cloudflare.com/pages/framework-guides/deploy-a-hugo-site/
官方域名文档：https://developers.cloudflare.com/pages/configuration/custom-domains/

## 以后怎么写文章？

进入 `content/posts/`，在 GitHub 网页点 Add file > Create new file，创建 `new-post.md`，例如：

```md
---
title: "我的第一篇新文章"
date: 2026-10-18
draft: false
---

这是正文，可以使用 Markdown。
```

提交后 Cloudflare Pages 会自动重新构建博客。

## 如何修改网站？

- 网站标题、说明和域名：`hugo.toml`。
- 首页布局：`layouts/home.html`。
- 文章列表布局：`layouts/section.html`。
- 文章详情：`layouts/page.html`。
- 字体、颜色、排版：`static/css/style.css`。
- 关于页面：`content/about.md`。
- 更换 Logo 图标：`static/favicon.svg`。

## 本地运行（可选）

安装 Hugo 0.158.0 或更新版本，然后在项目根目录运行：

```sh
hugo server
```

打开 http://localhost:1313/ 预览。`hugo --minify` 将生成可供 Nginx 托管的 `public` 文件夹，未来迁移自己的服务器时直接复用即可。
