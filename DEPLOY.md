# 部署到 520maodizhang.github.io/blog/ 指南

本仓库已从 [Yuimi-chaya/Yuimi-chaya.github.io](https://github.com/Yuimi-chaya/Yuimi-chaya.github.io) 克隆,
配置为部署到你的 GitHub 项目页 **`https://520maodizhang.github.io/blog/`**。

> 你原有的 `520maodizhang.github.io` 用户主页仓库**不会被影响**,两个站点并存。

## 已完成的配置

`astro.config.mjs` 里已设置:

```js
site: "https://520maodizhang.github.io",
base: "/blog/",
```

- `site`:你的 GitHub Pages 根域名
- `base: "/blog/"`:项目页路径前缀(项目页必须配置,否则资源 404)

## 部署步骤

### 1. 在 GitHub 新建仓库

- 仓库名:**`blog`**(小写)
- 可见性:**Public**
- **不要**勾选 "Initialize with README"(本地已有内容)

### 2. 启用 GitHub Pages(Actions 部署)

进入新仓库 → **Settings** → **Pages**:
- **Source** 选 `GitHub Actions`(不是 Deploy from a branch)

> 这一步必须先做,否则推送后 Actions 没有写入 Pages 的权限会失败。

### 3. 推送代码

```bash
cd /workspace/Yuimi-chaya.github.io

# 关联你的远程仓库
git remote add origin https://github.com/520maodizhang/blog.git

# 提交配置修改
git add -A
git commit -m "chore: configure for project page at /blog/"

# 推送
git branch -M main
git push -u origin main
```

### 4. 等待部署完成

推送后,仓库的 **Actions** 标签页会出现 "Deploy Astro site to GitHub Pages" 工作流。
等它跑完(绿色 ✓,约 3–6 分钟),访问:

**https://520maodizhang.github.io/blog/**

就能看到博客了。

---

## 本地预览

开发服务器已在后台运行,地址:

**http://localhost:4321/blog/**

主要页面:

| 路径 | 内容 |
|------|------|
| `/blog/` | Kisara 主题首页 |
| `/blog/blog/` | 文章列表 |
| `/blog/games/` | 游戏页 |
| `/blog/about/` | 个人页 |
| `/blog/themes/fuyukawa-kagari/` | Fuyukawa Kagari 手账风主题 |
| `/blog/themes/blank/` | 极简主题 |

> 构建需要 Node.js 24(已在本环境装好 v24.21.0)。GitHub Actions 也会自动用 Node 24。

---

## 想改成自己的内容?

- **站点名称 / 作者 / 导航文案**:`src/lib/site.ts`
- **文章**:`src/content/blog/` 下新建 `.md` / `.mdx`
- **主题**:三套可选,Kisara(默认)、Fuyukawa Kagari(手账风,更适合改造)、Blank(极简)

## 素材授权提醒

代码是 MIT,文章文字 CC BY-NC-SA 4.0,但**图片/音视频等媒体不自动授权**。
公开部署前建议替换未获许可的角色素材(详见 `THIRD_PARTY_ASSETS.md`)。

## 常见问题

**Q: 推送后 Actions 报错 "You can only deploy to a Pages site that you own"**
A: 没做第 2 步。去 Settings → Pages 把 Source 改成 `GitHub Actions`。

**Q: 站点打开是 404 或样式错乱**
A: 确认 `astro.config.mjs` 里有 `base: "/blog/"`(已配好),且 Actions 部署成功。
   访问地址是 `https://520maodizhang.github.io/blog/`(带 `/blog/` 后缀,不是根路径)。
