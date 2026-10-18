# LimbMove Blog — Hugo + GitHub + Cloudflare Pages

这是一个无需下载主题、无需 Node.js 的轻量 Hugo 个人博客源码，目标域名是 `https://blog.limbmove.com/`。

## 日常维护：用自然语言管理

本地项目已连接 `haixinhello/limbmove-blog`，生产分支为 `main`。初次建站步骤保留在下方，日常维护无需重复建仓或配置域名。

你可以直接要求开发助手：

- “把下面的内容发布为一篇博客，标题是……”。助手负责 Markdown、摘要、代码块、图片链接、构建与 Git 提交。
- “先把这篇保存为草稿”。草稿不会进入生产构建。
- “修改某篇文章的措辞，保留原链接”。保留原文件名，不随意更改 slug 或 URL。
- “调整博客排版，先给我预览”。本地验证后展示效果，确认后提交推送。

长期约定见 [AGENTS.md](AGENTS.md)。当前改版需先确认预览效果，再提交并推送。源码、文章和部署产物均为标准 Hugo 静态文件；不依赖数据库、外部字体、前端框架或 Cloudflare 专用运行时。

## 构建与验证

项目验证版本为 **Hugo 0.158.0**，Cloudflare Pages 的生产和预览环境应使用相同版本。无需安装 Node.js。

```sh
hugo version
hugo --minify --panicOnWarning
hugo server --bind 127.0.0.1
```

修改后检查首页、文章列表、正文、关于页、`/tags/`、`/categories/`、`/404.html`、RSS 和 sitemap；布局变更至少检查 320px、390px、768px 和桌面宽度。确认原有 `/posts/hello-world/` 与 `/posts/markdown-notes/` 继续可访问。

新增文章可由助手直接生成，也可使用 `hugo new content posts/my-project.md`；模板默认 `draft: true`。发布前填写摘要，核对日期（Asia/Shanghai）并改为 `draft: false`。正文中两处及以上的二、三级标题会生成可折叠目录。

## 模板与视觉结构

- `layouts/baseof.html`：公共页面结构。
- `layouts/partials/`：头部元信息、导航、页脚、文章列表行。
- `layouts/home.html`、`section.html`、`page.html`：首页、文章列表、正文。
- `layouts/taxonomy.html`、`term.html`：分类/标签索引及主题文章。
- `layouts/404.html`：错误页；Cloudflare Pages 和 Nginx 可使用生成的 `404.html`。
- `static/css/style.css`：按功能分组的样式、响应式与打印规则；样式链接包含内容摘要，更新后会更换缓存地址。

## 未来迁移到 VPS

在同一份源码上执行 `hugo --minify`，把生成的 `public/` 发布到 Nginx 网站目录即可。保留域名、目录结构、尾部斜杠和 HTTPS，文章链接不需要变更。Nginx 示例：

```nginx
server {
    listen 80;
    server_name blog.limbmove.com;
    root /var/www/limbmove-blog/public;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
    error_page 404 /404.html;
    location = /404.html { internal; }
}
```

此片段仅展示静态文件路由；正式迁移另行配置 HTTPS。当前维护不改动主站及任何 DNS 配置。

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
