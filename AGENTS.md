# 博客维护约定

- 本仓库只管理 `https://blog.limbmove.com/`，部署分支为 `main`。不修改 limbmove.com 主站、DNS 或 Cloudflare 域名设置。
- 保留现有文章和功能。未经用户明确要求，不删除文章，不改已有文章的文件名、slug、url、aliases 或站点 baseURL。
- 保持 Hugo 纯静态架构、系统字体和最少依赖；不引入必须依靠 Cloudflare 才能运行的功能。构建产物 public/ 可直接由 VPS 的 Nginx 托管。
- 自然语言发布：将用户提供的内容整理为 content/posts/ 下的 Markdown，处理 front matter、标题、摘要、代码语言、图片与链接。不得编造作者经历、项目结果或来源。
- 新文件使用稳定的英文 kebab-case 文件名；日期使用 Asia/Shanghai 的用户当地时间。草稿 draft: true，发布前核对 draft: false 和发布时间。
- 技术基线：Hugo 0.158.0。运行 hugo --minify，检查警告、原有 URL、RSS、sitemap 和本次变动涉及的页面；布局修改需检查桌面及窄屏效果。
- 文章内容属于用户，不主动改写现有文章。可复用的页面片段置于 layouts/partials/，CSS 置于 static/css/style.css，避免额外客户端 JavaScript。
- 当前视觉改版：先交付本地预览，收到用户对效果的确认后才提交并推送。后续发布按当次用户授权范围操作，不重复索取已有授权。
- 提交时仅包含本任务源码及文档，排除构建产物、临时截图、工具、凭据。推送后检查对应提交的 Cloudflare Pages 部署及线上页面；不能仅以 git push 成功代替部署成功。
