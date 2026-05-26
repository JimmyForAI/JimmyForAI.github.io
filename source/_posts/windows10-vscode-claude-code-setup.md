---
title: Windows 10/11 下 VS Code 部署 Claude Code 完整教程
date: 2026-05-26 14:00:00
tags:
  - Claude Code
  - VS Code
  - Windows
  - 教程
categories: 技术
---

## 前言

Claude Code 是 Anthropic 推出的命令行 AI 编程助手，可以直接在终端中帮你写代码、调试、搜索文件。配合 VS Code 使用体验更佳。

本教程适用于**Windows 10/11 系统**，从零开始一步步完成部署。

---

## 第一步：安装 VS Code

VS Code 是微软推出的免费代码编辑器。

1. 打开浏览器，访问 VS Code 官网：

   **https://code.visualstudio.com/**

2. 点击 **Download for Windows** 按钮，下载安装程序（约 100MB）

3. 双击下载的 `VSCodeSetup-x64-*.exe`，按以下配置安装：

   - 接受许可协议
   - 安装路径用默认即可（`C:\Users\你的用户名\AppData\Local\Programs\Microsoft VS Code`）
   - **勾选以下选项**（重要）：
     - ✅ **将 "Open with Code" 添加到右键菜单**
     - ✅ **将 Code 注册为受支持的文件类型的编辑器**
     - ✅ **添加到 PATH**（这样可以在终端直接用 `code` 命令）

4. 安装完成后打开 VS Code

---

## 第二步：安装 Node.js

Claude Code 依赖 Node.js 运行环境。

1. 打开浏览器，访问 Node.js 官网：

   **https://nodejs.org/**

2. 下载 **LTS 版本**（长期支持版，推荐 20.x 或更高版本）

   - 直接点左侧的 LTS 按钮即可下载 `.msi` 安装包

3. 双击安装包，可以更改自定义安装路径，随后一路默认安装即可。**关键一步**：确保 **"Add to PATH"** 选项已勾选

4. 验证安装是否成功。按 `Win + R`，输入 `cmd` 回车，在命令行中输入：

   ```bash
   node --version
   ```

   如果显示 `v20.x.x` 这样的版本号，说明安装成功。

   ```bash
   npm --version
   ```

   如果显示 `10.x.x` 这样的版本号，说明 npm 也已就绪。

---

## 第三步：安装 Claude Code

npm 是 Node.js 自带的包管理器，用来安装 Claude Code。

1. 打开命令行（`Win + R` → 输入 `cmd` → 回车），输入：

   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

   `-g` 表示全局安装，装完后在任何目录都能使用 `claude` 命令。

2. 安装过程大约需要 1-2 分钟，视网络状况而定。如果下载速度慢，可以切换到国内镜像：

   ```bash
   npm config set registry https://registry.npmmirror.com
   ```

   然后再重新执行安装命令。

3. 安装完成后验证：

   ```bash
   claude --version
   ```

   显示版本号即表示安装成功。

---

## 第四步：配置 API Key

Claude Code 需要 Anthropic API 密钥才能调用 AI 模型。

### 获取 API Key
这里之用**deepseek-v4-pro**模型为例子，创建自己的API key

1. 访问 deepseek网址：

   **https://www.deepseek.com/**

2. 注册或登录账号

3. 进入 **API 开放平台** 页面，点击左侧栏的 **充值**（建议先充值10元试试）

4. 点击左侧栏 **API keys** ，创建API keys，输入名称随意

5. 点击**复制**，离开页面后就无法再看到完整密钥，如果忘记则重新创建API key，步骤同上

### 下载cc-switch:
   **https://github.com/farion1231/cc-switch**

1. 右边栏下拉找到 **release**

2. 点击最新版本的CC-Switch

3. 在弹出页面中下拉到最底的 **Assets** ，寻找符合电脑版本的CC-Switch

4. 如果是 **win10/11**，则下载 **CC-Switch-v3.15.0-Windows.msi**

5. 打开 **cc-switch** 点击右上角 **+** ，在默认的claude供应商中选择 **DeepSeek**，填写刚才的API keys

6. 点击 **添加**

### 验证配置

打开新的命令行窗口，输入：

```bash
claude
```

如果看到 Claude Code 的欢迎界面，说明一切配置成功。

---

## 第五步：在 VS Code 中使用 Claude Code

### 方式一：集成终端（推荐）

1. 在 VS Code 中按 `Ctrl + `` ` 打开内置终端

2. 在终端中直接输入：

   ```bash
   claude
   ```

3. Claude Code 就在 VS Code 底部启动了，可以直接对话

### 方式二：安装 VS Code 扩展

1. 在 VS Code 左侧点击扩展图标（或按 `Ctrl + Shift + X`）

2. 搜索 **Claude Code**，找到官方扩展并安装

3. 安装后侧边栏会出现 Claude Code 图标，点击即可使用

---

## 常用命令速查

| 命令 | 作用 |
|------|------|
| `claude` | 启动 Claude Code 交互模式 |
| `claude "你的问题"` | 直接提问（不进入交互模式） |
| `claude --version` | 查看版本号 |
| `claude update` | 更新到最新版本 |
| `claude --help` | 查看帮助 |

---

## 常见问题

### npm 安装报权限错误

以管理员身份运行命令行，或使用以下命令：

```bash
npm install -g @anthropic-ai/claude-code --unsafe-perm
```

### 安装速度很慢

切换 npm 镜像源：

```bash
npm config set registry https://registry.npmmirror.com
```

### 命令行找不到 `claude` 命令

检查 npm 全局安装路径是否在系统 PATH 中。在命令行中输入：

```bash
npm list -g --depth=0
```

如果能看到 `@anthropic-ai/claude-code`，说明已安装，需要手动将 npm 全局路径加入 PATH：

1. 查看 npm 全局路径：`npm config get prefix`
2. 将该路径添加到系统环境变量 PATH 中

### API Key 验证失败

确保：
- API Key 已充值或有可用额度
- 设置环境变量后**重启了命令行窗口**

---

## 完成

至此，你已经可以在 Windows 的 VS Code 中愉快地使用 Claude Code 了。有任何问题欢迎联系我的邮箱。
