---
title: Hexo 博客修改后如何测试与上线
date: 2026-05-26 16:00:00
tags:
  - Hexo
  - GitHub Pages
  - 教程
categories: 技术
---

## 前言

每次修改博客内容后，建议先本地预览确认无误，再推送到 GitHub 自动部署。本教程适用于本站（Hexo + Butterfly + GitHub Actions 自动部署）。

---

## 工作流程总览

```mermaid
flowchart LR
    A[修改内容] --> B[本地预览]
    B --> C{满意?}
    C -->|否| A
    C -->|是| D[提交并推送]
    D --> E[GitHub Actions 自动部署]
    E --> F[线上生效]
```

---

## 一、本地预览测试

### 启动本地服务器

在 VS Code 终端或命令行中，进入博客项目目录，运行：

```bash
npm run server
```

这个命令会：
1. 生成静态文件
2. 启动本地 Web 服务器
3. 自动监听文件变化（修改保存后自动刷新）

### 打开浏览器预览

启动后终端会显示：

```
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```

在浏览器打开 **http://localhost:4000/** 即可预览。

### 预览时的注意事项

- **热更新**：修改 Markdown 文件保存后，刷新浏览器即可看到变化
- **配置文件修改**：如果改了 `_config.yml` 或 `_config.butterfly.yml`，需要**重启**服务器（`Ctrl+C` 停止，再 `npm run server`）
- **清除缓存**：如果页面显示异常，先清理再启动：

  ```bash
  npm run clean
  npm run server
  ```

### 停止服务器

按 `Ctrl + C` 停止本地服务器。

---

## 二、推送到 GitHub（上线）

### 步骤 1：查看修改内容

```bash
git status
```

这会列出所有修改过的文件，确认无误后再提交。

### 步骤 2：添加到暂存区

```bash
git add source/_posts/你的新文章.md
```

> **注意**：只添加博客内容相关的文件，**不要**添加 `.claude/`、`.vscode/`、`node_modules/` 等本地配置文件。

### 步骤 3：提交

```bash
git commit -m "feat: 添加新文章 xxx"
```

### 步骤 4：推送到 GitHub

```bash
git push origin main
```

推送成功后，GitHub Actions 会**自动触发部署**（约 1-2 分钟完成）。

---

## 三、验证线上效果

### 查看部署状态

1. 打开 **https://github.com/JimmyForAI/JimmyForAI.github.io/actions**
2. 查看最新的 workflow run：
   - 黄色旋转图标 🟡 → 正在部署
   - 绿色对勾 ✅ → 部署成功
   - 红色叉号 ❌ → 部署失败，点击查看日志

### 检查线上网站

部署成功后，访问 **https://jimmyforai.github.io** 验证。

> **提示**：如果看到的是旧内容，按 `Ctrl + F5` 强制刷新清除浏览器缓存。

---

## 四、快速操作参考

```bash
# 本地预览
npm run server                # http://localhost:4000

# 缓存清理
npm run clean

# 提交上线
git add <文件>
git commit -m "描述你的修改"
git push origin main

# 查看部署进度
# 浏览器打开: https://github.com/JimmyForAI/JimmyForAI.github.io/actions
```

---

## 五、网络问题的处理

如果 `git push` 失败，提示无法连接 GitHub：

1. 确认代理/VPN 已开启
2. 设置 Git 代理：
   ```bash
   git config --global http.proxy http://127.0.0.1:你的端口号
   ```
3. 重试推送：
   ```bash
   git push origin main
   ```

---

## 总结

改内容 → `npm run server` 本地看 → 确认没问题 → `git add` → `git commit` → `git push` → 等一分钟刷新线上页面。就这三步，每次改完走一遍就行。
