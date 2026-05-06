# Lihuacheng's Blog — 使用报告与完全教程

> 基于 Hexo + GitHub Pages 的个人博客
> 主题：Trae Light（仿 Trae Light 模式设计）

---

## 目录

1. [博客架构概览](#1-博客架构概览)
2. [已修复的错误](#2-已修复的错误)
3. [主题介绍：Trae Light](#3-主题介绍trae-light)
4. [如何本地预览博客](#4-如何本地预览博客)
5. [如何部署到 GitHub Pages（公网访问）](#5-如何部署到-github-pages公网访问)
6. [如何自定义博客内容](#6-如何自定义博客内容)
7. [文件结构说明](#7-文件结构说明)
8. [常见操作速查](#8-常见操作速查)
9. [自定义模板配置](#9-自定义模板配置)
10. [下一步建议](#10-下一步建议)

---

## 1. 博客架构概览

```
技术栈: Hexo (静态网站生成器) + GitHub Pages (托管)
域名: https://lihuacheng524.github.io
主题: trae-light (自定义)
```

### 核心依赖

| 包名 | 用途 |
|------|------|
| hexo | 核心框架 v8.x |
| hexo-deployer-git | Git 部署插件 |
| hexo-generator-index | 首页文章列表生成 |
| hexo-generator-archive | 归档页面生成 |
| hexo-renderer-ejs | EJS 模板引擎 |
| hexo-renderer-marked | Markdown 渲染 |
| hexo-renderer-stylus | Stylus CSS 预处理器 |
| hexo-server | 本地开发服务器 |

---

## 2. 已修复的错误

### 2.1 URL 配置错误

**问题**：`_config.yml` 中的 `url` 被错误地设置为：
```
url: https://github.com/Lihuacheng524/Lihuacheng524.github.io.git
```
这是仓库地址，不是网站地址，导致生成的页面链接全部错误。

**修复**：更正为正确的 GitHub Pages 域名：
```
url: https://lihuacheng524.github.io
```

### 2.2 作者与语言设置

**问题**：author 显示为 `John Doe`，language 为 `en`

**修复**：
```
author: Lihuacheng
language: zh-CN
timezone: 'Asia/Shanghai'
```

### 2.3 "Spawn failed" 部署错误

**原因**：
1. 博客根目录没有初始化 `.git` 仓库
2. 未配置 SSH 密钥到 GitHub 账户
3. 远程仓库可能不存在或权限不足

**修复方法**：见 [第 5 章 部署教程](#5-如何部署到-github-pages公网访问)

---

## 3. 主题介绍：Trae Light

### 3.1 设计理念

参考 Trae IDE 的 Light 模式设计风格，追求 **简洁、清晰、专业** 的视觉体验。

| 特性 | 说明 |
|------|------|
| 🎨 配色 | 纯白背景 `#ffffff` + 蓝色主色调 `#0066ff` + 灰色辅助 `#6b7280` |
| 🔤 字体 | Inter 字体（无衬线），兼顾美观与可读性 |
| 📐 排版 | 清晰的信息层级，充足的行距和留白 |
| 🖼️ 首页 | 个人头像 + 名称 + 简介 + 社交链接 + 技能条 + 项目展示 |
| 📱 响应式 | 完美适配手机、平板、桌面三种尺寸 |
| 🌙 体验 | 平滑过渡动画，毛玻璃导航栏效果 |

### 3.2 页面结构

| 页面 | 路由 | 说明 |
|------|------|------|
| 首页 | `/` | 个人介绍 + 最新文章 + 技能 + 项目 |
| 文章归档 | `/archives/` | 按时间排序的所有文章 |
| 目标 | `/goals/` | 年度目标与完成情况跟踪 |
| 关于我 | `/about/` | 个人详细自我介绍 |
| 文章页 | `/:year/:month/:day/:title/` | 单篇文章阅读页 |

### 3.3 导航栏

```
[Lihuacheng's Blog]    Home | Blog | Goals | About
```

导航栏为粘性定位，滚动时保持可见，带有毛玻璃背景效果。

---

## 4. 如何本地预览博客

### 4.1 一键启动

```bash
# 在博客根目录 d:\Files\blog 下执行

# 清理缓存
node node_modules/hexo/bin/hexo clean

# 生成静态文件
node node_modules/hexo/bin/hexo generate

# 启动本地服务器
node node_modules/hexo/bin/hexo server
```

然后在浏览器打开 **http://localhost:4000** 即可查看。

### 4.2 生成与预览分离

如果只想生成静态文件不启动服务器：

```bash
node node_modules/hexo/bin/hexo generate
```

生成的文件在 `public/` 目录中，可以直接用任何静态服务器托管。

---

## 5. 如何部署到 GitHub Pages（公网访问）

这是让全世界都能访问你博客的关键步骤。

### 5.1 前置条件

- 一个 GitHub 账号
- 仓库 `Lihuacheng524/Lihuacheng524.github.io` 已存在（在 GitHub 上创建）
- Git 已安装（`git --version` 验证）

### 5.2 完整部署流程

#### 第一步：初始化 Git 仓库

```bash
cd d:\Files\blog
git init
git add .
git commit -m "初始化博客"
```

#### 第二步：添加远程仓库

```bash
git remote add origin https://github.com/Lihuacheng524/Lihuacheng524.github.io.git
```

#### 第三步：配置 GitHub Token（推荐，比 SSH 简单）

1. 打开 GitHub → 点击右上角头像 → **Settings**
2. 左侧菜单 → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. 点击 **Generate new token (classic)**
4. 设置名称（如 `hexo-deploy`），勾选 `repo` 权限
5. 点击 **Generate token**
6. **复制并保存生成的 token**（关闭页面后就看不到了）

#### 第四步：修改部署配置

编辑 `_config.yml` 的 deploy 部分：

```yaml
deploy:
  type: 'git'
  repository: https://github.com/Lihuacheng524/Lihuacheng524.github.io.git
  branch: main
```

#### 第五步：部署到 GitHub Pages

```bash
node node_modules/hexo/bin/hexo deploy -g
```

第一次运行会弹出登录窗口：
- 用户名：输入 `Lihuacheng524`
- 密码：**粘贴你刚才生成的 Token**（不是 GitHub 登录密码）

#### 第六步：配置 GitHub Pages

1. 打开浏览器访问：https://github.com/Lihuacheng524/Lihuacheng524.github.io
2. 点击 **Settings** → 左侧 **Pages**
3. 在 **Branch** 下拉选择 `main`，目录选 `/ (root)`
4. 点击 **Save**

等待 1-2 分钟，访问 **https://lihuacheng524.github.io** 就能看到你的博客了！

### 5.3 SSH 方式（备选）

如果不想每次输入 Token，可以配置 SSH：

```bash
# 生成 SSH 密钥
ssh-keygen -t rsa -b 4096 -C "你的邮箱@example.com"
# 一路按 Enter

# 查看公钥
cat ~/.ssh/id_rsa.pub
```

复制输出的内容，打开 GitHub → Settings → SSH and GPG keys → New SSH key，粘贴保存。

然后将部署配置改回 SSH 方式：

```yaml
deploy:
  type: 'git'
  repository: git@github.com:Lihuacheng524/Lihuacheng524.github.io.git
  branch: main
```

### 5.4 部署后更新

以后每次写完新文章，只需两步：

```bash
node node_modules/hexo/bin/hexo generate   # 生成
node node_modules/hexo/bin/hexo deploy      # 部署
```

或者合二为一：

```bash
node node_modules/hexo/bin/hexo deploy -g
```

---

## 6. 如何自定义博客内容

### 6.1 修改个人介绍

编辑 [themes/trae-light/_config.yml](themes/trae-light/_config.yml)：

```yaml
# 头像（图片放到 source/images/ 目录）
avatar: /images/th.jpg

# 问候语
greeting: Hi, I'm

# 个人简介
subtitle: 热衷于技术探索与生活记录

# 社交链接
social:
  GitHub: https://github.com/Lihuacheng524
  # 可以继续添加：
  # Twitter: https://twitter.com/你的账号
  # Bilibili: https://space.bilibili.com/你的UID
```

### 6.2 更换头像

1. 准备一张正方形头像图片（建议 200x200 像素以上）
2. 放入 `source/images/` 目录
3. 修改主题配置中的 `avatar` 路径

### 6.3 修改导航栏

编辑 [themes/trae-light/_config.yml](themes/trae-light/_config.yml)：

```yaml
menu:
  Home: /
  Blog: /archives/
  Goals: /goals/
  About: /about/
```

- `Home` / `Blog` 等是显示的文字
- `/` `/archives/` 等是对应的链接路径
- 要添加新页面，先创建页面（见 6.7），再在这里加链接

### 6.4 写新文章

```bash
node node_modules/hexo/bin/hexo new "文章标题"
```

会在 `source/_posts/` 下生成一个 `.md` 文件，用任何文本编辑器打开编辑。

文章头部格式（Front-matter）：

```markdown
---
title: 文章标题
date: 2026-05-06
tags:
  - 标签1
  - 标签2
categories:
  - 分类名称
description: 文章简介，会显示在首页文章卡片上
---

## 章节标题

这里是文章内容，**支持 Markdown 语法**。

- 列表项
- 列表项

`代码块`

> 引用内容
```

### 6.5 更新目标进度

编辑 [source/goals/index.md](source/goals/index.md)：

```markdown
## 2026 年度目标

### 技术学习
- [x] 已完成的目标
- [ ] 进行中的目标
- [ ] 待开始的目标
```

方括号中的 `x` 表示已完成，空格表示未完成。

### 6.6 修改技能与项目

编辑 [themes/trae-light/_config.yml](themes/trae-light/_config.yml)：

```yaml
skills:
  - name: Web Development
    level: 80      # 1-100 之间的数字，显示为进度条
  - name: Backend
    level: 70

projects:
  - name: 项目名称
    description: 一句话描述你的项目
    url: https://github.com/你的项目地址
```

### 6.7 创建新页面

```bash
node node_modules/hexo/bin/hexo new page 页面名称
```

例如 `node node_modules/hexo/bin/hexo new page photos` 会创建 `source/photos/index.md`。

编辑这个文件后，在主题配置的 `menu` 中添加一行：

```yaml
  Photos: /photos/
```

### 6.8 修改网站标题 / 副标题

编辑根目录 [\_config.yml](_config.yml)：

```yaml
title: Lihuacheng's Blog          # 浏览器标签栏标题
subtitle: 'Ambitious and Liberated'  # 副标题
description: '个人描述，用于 SEO'      # SEO 描述
```

---

## 7. 文件结构说明

```
blog/
│
├── _config.yml                    # 📋 博客主配置文件
├── USAGE.md                       # 📖 本使用文档
├── package.json                   # 📦 Node.js 依赖管理
│
├── scaffolds/                     # 📝 文章模板
│   ├── post.md                    #   文章模板
│   ├── page.md                    #   页面模板
│   └── draft.md                   #   草稿模板
│
├── source/                        # 🗂️ 源文件目录（所有内容放这里）
│   ├── _posts/                    #   文章存放目录
│   │   └── Hello-World.md         #     示例文章
│   ├── about/                     #   关于页面
│   │   └── index.md
│   ├── goals/                     #   目标页面
│   │   └── index.md
│   └── images/                    #   图片资源
│       └── th.jpg                 #     当前头像图片
│
├── themes/                        # 🎨 主题目录
│   └── trae-light/                #   ✅ 当前使用的主题
│       ├── _config.yml            #      主题配置（改这里定制外观）
│       ├── layout/                #      EJS 模板文件
│       │   ├── index.ejs          #      首页
│       │   ├── post.ejs           #      文章页
│       │   ├── page.ejs           #      普通页面
│       │   ├── archive.ejs        #      归档页
│       │   ├── category.ejs       #      分类页
│       │   ├── tag.ejs            #      标签页
│       │   └── _partial/          #      可复用组件
│       │       ├── head.ejs       #        HTML head
│       │       ├── header.ejs     #        导航栏
│       │       ├── footer.ejs     #        页脚
│       │       └── after-footer.ejs #     页脚脚本
│       └── source/
│           └── css/
│               └── style.css      #      🎯 全局样式表
│
├── public/                        # 🌐 生成的静态网站（自动生成，不要手动修改）
│
└── node_modules/                  # 📚 依赖包（自动生成）
```

---

## 8. 常见操作速查

| 操作 | 命令 |
|------|------|
| 清理缓存 | `node node_modules/hexo/bin/hexo clean` |
| 生成网站 | `node node_modules/hexo/bin/hexo generate` |
| 本地预览 | `node node_modules/hexo/bin/hexo server` |
| 部署上线 | `node node_modules/hexo/bin/hexo deploy -g` |
| 新建文章 | `node node_modules/hexo/bin/hexo new "标题"` |
| 新建页面 | `node node_modules/hexo/bin/hexo new page "名称"` |
| 新建草稿 | `node node_modules/hexo/bin/hexo new draft "标题"` |
| 安装依赖 | `npm install` |

---

## 9. 自定义模板配置

### 9.1 主题配置完整说明

编辑 [themes/trae-light/_config.yml](themes/trae-light/_config.yml) 可控制主题的所有行为：

```yaml
# ==== 导航菜单 ====
menu:
  Home: /               # 首页
  Blog: /archives/      # 博客归档
  Goals: /goals/        # 目标
  About: /about/        # 关于

# ==== 个人资料（首页 Hero 区域）====
avatar: /images/th.jpg          # 头像路径
greeting: Hi, I'm               # 问候语
subtitle: 热衷于技术探索与生活记录  # 个人简介

# ==== 社交链接 ====
social:
  GitHub: https://github.com/Lihuacheng524
  # 格式: 名称: 链接

# ==== 技能展示（首页）====
skills:
  - name: Web Development     # 技能名称
    level: 80                  # 熟练度 0-100
  - name: Backend
    level: 70
  - name: DevOps
    level: 60

# ==== 项目展示（首页）====
projects:
  - name: My Blog
    description: 基于Hexo的个人博客
    url: https://github.com/Lihuacheng524/Lihuacheng524.github.io

# ==== 页脚 ====
copyright: © 2026 Lihuacheng. All rights reserved.

# ==== RSS ====
rss: /atom.xml

# ==== 网站图标 ====
favicon: /images/th.jpg
```

### 9.2 样式自定义

直接编辑 [themes/trae-light/source/css/style.css](themes/trae-light/source/css/style.css) 可以修改任何样式。

常用修改：

```css
/* 修改主色调 */
:root {
  --primary: #0066ff;        /* 改成你喜欢的颜色 */
}

/* 修改字体 */
body {
  font-family: 'Inter', ...;  /* 可以改成其他字体 */
}

/* 修改头像大小 */
.hero-avatar {
  width: 120px;
  height: 120px;
}
```

修改后重新生成即可看到效果。

---

## 10. 下一步建议

- [ ] **👤 更换头像** — 将自己的照片放入 `source/images/`，更新配置
- [ ] **✍️ 写第一篇文章** — 使用 `hexo new "标题"` 创建
- [ ] **🎯 完善目标页** — 编辑 `source/goals/index.md`
- [ ] **🔧 调整技能** — 在主题配置中修改 `skills` 列表
- [ ] **🚀 部署上线** — 按照第 5 章教程部署到 GitHub Pages
- [ ] **📝 持续更新** — 保持写作习惯，定期更新博客

---

> **💡 提示**：有任何问题，可以查看 [Hexo 官方文档](https://hexo.io/docs/) 或访问 [GitHub Pages 文档](https://docs.github.com/en/pages)。

---

*最后更新：2026-05-06*
