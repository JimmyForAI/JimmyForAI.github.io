# Personal Blog Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a personal blog with Hexo + Butterfly theme, deployed to GitHub Pages via GitHub Actions.

**Architecture:** Hexo generates static HTML from Markdown source files. Butterfly theme provides the UI (dark/light mode, responsive, search). GitHub Actions auto-deploys on push to main.

**Tech Stack:** Hexo (Node.js), Butterfly theme, GitHub Pages, GitHub Actions

---

### Task 1: Initialize Hexo project

**Files:**
- Create: `package.json`, `_config.yml`, `source/`, `scaffolds/`, `.gitignore`

- [ ] **Step 1: Run hexo init**

Hexo init requires an empty directory. Temporarily move existing files out, init, then restore.

```bash
cd E:/vscode_test
mkdir ../vscode_test_tmp
mv calculator.py test.py ../vscode_test_tmp/
npx hexo init .
mv ../vscode_test_tmp/calculator.py ../vscode_test_tmp/test.py .
rmdir ../vscode_test_tmp
```

Expected: Hexo scaffolds created (package.json, _config.yml, source/, scaffolds/, node_modules/, .gitignore).

- [ ] **Step 2: Verify project structure**

```bash
ls -la E:/vscode_test/_config.yml E:/vscode_test/package.json E:/vscode_test/source/
```

Expected: All three paths exist.

- [ ] **Step 3: Run hexo generate to verify it works**

```bash
cd E:/vscode_test && npx hexo generate
```

Expected: `public/` directory created with HTML files, no errors.

- [ ] **Step 4: Commit**

```bash
cd E:/vscode_test
git add package.json package-lock.json _config.yml .gitignore scaffolds/ source/ node_modules/ public/
git commit -m "feat: initialize Hexo project"
```

---

### Task 2: Install Butterfly theme

**Files:**
- Modify: `package.json`
- Create: `themes/butterfly/`, `_config.butterfly.yml`

- [ ] **Step 1: Install butterfly via npm**

```bash
cd E:/vscode_test && npm install hexo-theme-butterfly --save
```

Expected: `hexo-theme-butterfly` added to package.json, theme files in `node_modules/hexo-theme-butterfly/`.

- [ ] **Step 2: Copy theme config to project root**

```bash
cd E:/vscode_test && cp node_modules/hexo-theme-butterfly/_config.yml _config.butterfly.yml
```

- [ ] **Step 3: Commit**

```bash
cd E:/vscode_test
git add package.json package-lock.json _config.butterfly.yml
git commit -m "feat: add Butterfly theme"
```

---

### Task 3: Configure site metadata

**Files:**
- Modify: `_config.yml`

- [ ] **Step 1: Update _config.yml with site metadata**

Read `E:/vscode_test/_config.yml` and update these fields:

```yaml
title: My Blog
subtitle: ''
description: 'Personal blog about tech and life'
author: Your Name
language: zh-CN
timezone: 'Asia/Shanghai'

url: https://<username>.github.io
root: /

theme: butterfly

new_post_name: :title.md
default_layout: post
```

- [ ] **Step 2: Verify hexo generate still works**

```bash
cd E:/vscode_test && npx hexo generate
```

Expected: No errors, output in `public/`.

- [ ] **Step 3: Commit**

```bash
cd E:/vscode_test
git add _config.yml
git commit -m "feat: configure site metadata"
```

---

### Task 4: Configure Butterfly theme

**Files:**
- Modify: `_config.butterfly.yml`

- [ ] **Step 1: Set up Butterfly theme config**

Read `E:/vscode_test/_config.butterfly.yml` and update these sections:

```yaml
# Navigation menu
menu:
  Home: / || fas fa-home
  About: /about/ || fas fa-heart
  Projects: /projects/ || fas fa-folder

# Enable search
local_search:
  enable: true

# Post settings
post_meta:
  page:
    date_type: created
    categories: true
    tags: true

# Sidebar
sidebar:
  display_position: right
```

- [ ] **Step 2: Commit**

```bash
cd E:/vscode_test
git add _config.butterfly.yml
git commit -m "feat: configure Butterfly theme"
```

---

### Task 5: Create About page

**Files:**
- Create: `source/about/index.md`

- [ ] **Step 1: Create about page**

Write to `E:/vscode_test/source/about/index.md`:

```markdown
---
title: 关于我
date: 2026-05-25 12:00:00
type: about
---

## 关于我

你好！我是 [你的名字]。

这里是一个热爱技术、喜欢分享的开发者。

### 技能

- 编程语言：Python, JavaScript
- 前端：HTML, CSS, React
- 工具：Git, VS Code

### 联系方式

- GitHub: [@username](https://github.com/username)
- Email: your-email@example.com
```

- [ ] **Step 2: Verify about page renders**

```bash
cd E:/vscode_test && npx hexo generate
```

Expected: `public/about/index.html` exists.

- [ ] **Step 3: Commit**

```bash
cd E:/vscode_test
git add source/about/index.md
git commit -m "feat: add About page"
```

---

### Task 6: Create Projects page

**Files:**
- Create: `source/projects/index.md`

- [ ] **Step 1: Create projects page**

Write to `E:/vscode_test/source/projects/index.md`:

```markdown
---
title: 项目
date: 2026-05-25 12:00:00
type: projects
---

## 项目展示

### 计算器应用
一个基于 Python Tkinter 的桌面计算器，支持基本运算和深色主题。
- **技术栈：** Python, Tkinter
- **GitHub：** [链接](https://github.com/username/calculator)

### 个人博客
基于 Hexo 和 Butterfly 主题的静态博客。
- **技术栈：** Hexo, Node.js, Markdown
- **GitHub：** [链接](https://github.com/username/blog)
```

- [ ] **Step 2: Verify projects page renders**

```bash
cd E:/vscode_test && npx hexo generate
```

Expected: `public/projects/index.html` exists.

- [ ] **Step 3: Commit**

```bash
cd E:/vscode_test
git add source/projects/index.md
git commit -m "feat: add Projects page"
```

---

### Task 7: Create sample blog post

**Files:**
- Create: `source/_posts/hello-world.md`

- [ ] **Step 1: Write first blog post**

Write to `E:/vscode_test/source/_posts/hello-world.md`:

```markdown
---
title: Hello World
date: 2026-05-25 12:00:00
tags:
  - 博客
  - 入门
categories: 随笔
---

## 欢迎来到我的博客

这是我的第一篇博客文章。

这个博客使用 **Hexo** 构建，使用 **Butterfly** 主题，部署在 **GitHub Pages** 上。

### 功能

- 支持 Markdown 写作
- 代码语法高亮
- 深色/浅色模式
- 标签和分类系统
- 全文搜索

以后会在这里分享技术文章和生活随笔。
```

- [ ] **Step 2: Verify blog post renders**

```bash
cd E:/vscode_test && npx hexo generate && ls public/2026/05/25/hello-world/
```

Expected: `index.html` in the hello-world directory.

- [ ] **Step 3: Commit**

```bash
cd E:/vscode_test
git add source/_posts/hello-world.md
git commit -m "feat: add hello world blog post"
```

---

### Task 8: Set up GitHub Actions deployment

**Files:**
- Create: `.github/workflows/deploy.yml`

- [ ] **Step 1: Create GitHub Actions workflow**

Write to `E:/vscode_test/.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install dependencies
        run: npm ci

      - name: Generate static files
        run: npx hexo generate

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages
```

- [ ] **Step 2: Commit**

```bash
cd E:/vscode_test
git add .github/workflows/deploy.yml
git commit -m "feat: add GitHub Actions deploy workflow"
```

---

### Task 9: Local verification

**Files:**
- (none, verification only)

- [ ] **Step 1: Clean generate**

```bash
cd E:/vscode_test && npx hexo clean && npx hexo generate
```

Expected: Clean build, no errors.

- [ ] **Step 2: Verify all pages exist in public/**

```bash
ls E:/vscode_test/public/index.html
ls E:/vscode_test/public/about/index.html
ls E:/vscode_test/public/projects/index.html
```

Expected: All three files exist.

- [ ] **Step 3: Verify site structure matches spec**

- Blog homepage: `public/index.html`
- About page: `public/about/index.html`
- Projects page: `public/projects/index.html`
- Blog post: `public/2026/05/25/hello-world/index.html`

- [ ] **Step 4: Run dev server for manual check**

```bash
cd E:/vscode_test && npx hexo server
```

Expected: Server starts at `http://localhost:4000`. Open in browser to verify all three pages render correctly.

- [ ] **Step 5: Commit any final changes**

```bash
cd E:/vscode_test
git status
git add -A
git commit -m "chore: final verification and cleanup"
```
