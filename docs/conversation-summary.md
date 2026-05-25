# 个人博客搭建 — 对话总结

> 日期：2026-05-25
> 项目：基于 Hexo + Butterfly 的个人博客

---

## 1. 需求澄清

| 问题 | 回答 |
|------|------|
| 博客目的 | 综合性个人主页（博客 + 关于我 + 项目展示） |
| 技术栈偏好 | 静态站点生成器（Hugo/Hexo） |
| 部署平台 | GitHub Pages |
| 生成器选择 | Hexo（推荐，Node.js 生态，中文社区大） |
| 网站板块 | 博客 + 关于我 + 项目展示 |

---

## 2. 设计方案

### 技术栈

- **Hexo** — Node.js 静态站点生成器
- **Butterfly** — Hexo 主题（支持深色/浅色模式、响应式、搜索）
- **Markdown** — 内容编写
- **GitHub Pages** — 托管
- **GitHub Actions** — 自动构建部署

### 网站结构

- **首页** (`/`) — 博客文章列表，分页
- **关于我** (`/about/`) — 个人介绍
- **项目展示** (`/projects/`) — 作品展示

### 项目架构

```
├── source/
│   ├── _posts/              # Markdown 博客文章
│   ├── about/index.md       # 关于我页面
│   ├── projects/index.md    # 项目展示页面
│   └── images/              # 图片资源
├── themes/butterfly/        # Butterfly 主题
├── _config.yml              # Hexo 配置
├── _config.butterfly.yml    # 主题配置
└── .github/workflows/       # GitHub Actions 部署
```

### 发布流程

```
新建 .md 文章 → hexo g 生成静态文件 → git push → GitHub Actions 自动部署
```

本地预览：`hexo s` 启动开发服务器 `http://localhost:4000`

---

## 3. 实施计划（9 个任务）

| 任务 | 内容 |
|------|------|
| Task 1 | 初始化 Hexo 项目 |
| Task 2 | 安装 Butterfly 主题 |
| Task 3 | 配置站点元数据（标题、语言、URL、主题） |
| Task 4 | 配置 Butterfly 主题（导航、搜索、侧边栏） |
| Task 5 | 创建「关于我」页面 |
| Task 6 | 创建「项目展示」页面 |
| Task 7 | 创建示例博客文章 |
| Task 8 | 设置 GitHub Actions 自动部署 |
| Task 9 | 本地验证 |

---

## 4. 实施结果

### 提交记录

| Commit | 内容 |
|--------|------|
| `27018cf` | 初始化 Hexo 项目 |
| `4915e16` | 添加 Butterfly 主题 |
| `66ad0c8` | 配置站点元数据 |
| `b8fd012` | 配置 Butterfly 主题 |
| `d3c51f6` | 添加关于我页面 |
| `9b3ab89` | 添加项目展示页面 |
| `bfb8f61` | 添加 Hello World 博客文章 |
| `537083e` | 添加 GitHub Actions 部署工作流 |
| `a2d2854` | 修复：安装 hexo-generator-searchdb 搜索插件 |

### 本地验证

- `hexo clean && hexo generate` — 22 个文件生成，0 错误
- 首页 `public/index.html` — 14KB
- 关于我 `public/about/index.html` — 14KB
- 项目展示 `public/projects/index.html` — 14KB
- 博客文章 `public/2026/05/25/hello-world/index.html` — 16KB
- 本地搜索 `search.json` — 生成正常

---

## 5. 部署到 GitHub Pages

### 步骤

1. 在 GitHub 上创建新仓库（不要勾选 README/.gitignore）
2. 重命名分支并推送：

```bash
git branch -m master main
git remote add origin https://github.com/<用户名>/<仓库名>.git
git push -u origin main
```

3. 启用 GitHub Pages：
   - Settings → Pages → Source: `Deploy from a branch`
   - Branch: `gh-pages`，目录: `/ (root)`

### 上线前需要修改的配置

在 `_config.yml` 中：
- `url` — 替换为 `https://<你的用户名>.github.io`
- `author` — 替换为真实名字

在 `_config.butterfly.yml` 中：
- 侧边栏 GitHub 链接 — 替换为真实链接

在页面内容中：
- `source/about/index.md` — 替换 `[你的名字]` 和联系方式
- `source/projects/index.md` — 替换项目链接

---

## 6. 文件清单

### 项目文件

| 文件 | 说明 |
|------|------|
| `_config.yml` | Hexo 主配置 |
| `_config.butterfly.yml` | Butterfly 主题配置 |
| `package.json` | npm 依赖（hexo, hexo-theme-butterfly, hexo-generator-searchdb） |
| `source/_posts/hello-world.md` | 示例博客文章 |
| `source/about/index.md` | 关于我页面 |
| `source/projects/index.md` | 项目展示页面 |
| `.github/workflows/deploy.yml` | GitHub Actions 自动部署 |
| `scaffolds/` | Hexo 文章模板（draft, page, post） |

### 设计文档

| 文件 | 说明 |
|------|------|
| `docs/superpowers/specs/2026-05-25-personal-blog-design.md` | 设计规格 |
| `docs/superpowers/plans/2026-05-25-personal-blog-plan.md` | 实施计划 |
