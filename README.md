# ZEKOGAMES LIMITED 利用規約 — Cloudflare Pages 部署

本目录是一个**纯静态站点**，仅包含 `index.html`（完整日文利用規約）与可选的 `wrangler.toml` 配置文件，可直接部署到 Cloudflare Pages，**无需任何构建步骤**。

> 配套存档文档：`/workspace/ZEKOGAMES利用規約.docx`（Word 版，供内部存档）。

## 目录结构

```
cloudflare-site/
├── index.html      # 利用規約网页（自包含，含样式与目录导航）
├── wrangler.toml   # （可选）Wrangler CLI 部署配置
└── README.md       # 本说明
```

## 部署方式一：Git 仓库连接（推荐，自动 CI/CD）

1. 将 `cloudflare-site/` 整个目录作为仓库根目录推送到 GitHub / GitLab。
   ```bash
   git init
   git add .
   git commit -m "add ZEKOGAMES terms of service"
   git branch -M main
   git remote add origin <你的仓库地址>
   git push -u origin main
   ```
2. 登录 Cloudflare Dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**。
3. 选择对应仓库，构建设置填写：
   - **Framework preset**：`None`
   - **Build command**：留空
   - **Build output directory**：`.`（点号，即根目录）
4. 点击 **Save and Deploy**。完成后会获得 `*.pages.dev` 域名，可在 **Custom domains** 绑定自有域名（如 `terms.zekogames.com`）。
5. 之后每次 `git push` 即自动重新部署。

## 部署方式二：Wrangler CLI 直接上传（无需 Git）

1. 安装 Node.js 后安装 Wrangler：
   ```bash
   npm install -g wrangler
   wrangler login        # 浏览器授权，仅首次需要
   ```
2. 在本目录执行部署：
   ```bash
   wrangler pages deploy . --project-name zekogames-terms
   ```
3. 终端会返回预览 URL 与生产 URL。设置自定义域名：
   ```bash
   wrangler pages project add-domain zekogames-terms terms.zekogames.com
   ```

## 部署方式三：Dashboard 直接拖拽上传

1. 将本目录压缩为 ZIP（确保 `index.html` 在压缩包根层）。
2. Cloudflare Dashboard → **Workers & Pages** → **Create** → **Pages** → **Upload assets**。
3. 拖入 ZIP，Project name 填 `zekogames-terms`，点击 **Deploy**。

## 本地预览

```bash
# 在本目录启动静态服务器
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

## 注意事项

- 站点为静态、无外部依赖，符合 Cloudflare Pages 免费额度。
- 如需启用 HTTPS 强制跳转与缓存策略，可在本目录新增 `_headers` 文件（可选）。
- 利用規約正文中的 `2026年○月○日` 为占位日期，正式发布前请替换为实际施行日。
- 除 Hong Kong 注册地址外，本文适用日本法、东京地方裁判所管辖，属跨境服务场景，正式上线前建议由当地律师复核。
