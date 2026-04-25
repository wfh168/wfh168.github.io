# Hexo 博客操作指南

> 博客地址：https://wfh168.github.io  
> 主题：hexo-theme-redefine v2.9.0  
> 部署方式：GitHub Pages (hexo-deployer-git)

---

## 目录

1. [目录结构](#1-目录结构)
2. [基础命令](#2-基础命令)
3. [写作文章](#3-写作文章)
4. [音乐播放器](#4-音乐播放器)
5. [主题配置](#5-主题配置)
6. [部署上线](#6-部署上线)
7. [常见问题](#7-常见问题)

---

## 1. 目录结构

```
d:\codeproject\
├── _config.yml              # Hexo 主配置文件
├── _config.redefine.yml     # 主题配置文件
├── package.json             # 依赖配置
├── source/                  # 网站内容（写在这里的都会生成到网站）
│   ├── _posts/              # 文章存放目录
│   ├── music/               # 音乐文件目录
│   ├── images/              # 图片目录
│   └── _data/               # 数据文件目录
├── scripts/                 # Hexo 脚本目录（会自动加载为插件）
├── themes/                  # 主题目录
│   └── redefine/            # Redefine 主题
└── public/                  # 生成的静态网站文件（部署用）
```

---

## 2. 基础命令

在 `d:\codeproject\` 目录下执行：

### 开发预览

```bash
# 清理缓存并启动本地服务器
npx hexo clean && npx hexo server

# 简写方式（每次改配置后建议先 clean）
npx hexo clean
npx hexo server
```

- 本地预览地址：`http://localhost:4000/`
- 修改配置或文章后，刷新页面即可看到更新

### 生成网站

```bash
# 生成静态文件到 public/ 目录
npx hexo generate

# 简写
npx hexo g
```

### 部署上线

```bash
# 推送到 GitHub Pages
npx hexo deploy

# 简写
npx hexo d
```

> 部署配置已在 `_config.yml` 中设置好，会自动推送到 `https://github.com/wfh168/wfh168.github.io` 的 `gh-pages` 分支。

---

## 3. 写作文章

### 创建新文章

```bash
npx hexo new "文章标题"
```

执行后会在 `source/_posts/` 目录下生成一个 Markdown 文件，文件名根据标题自动生成。

### 文章 Front-matter 格式

文件顶部以 `---` 包裹的部分称为 Front-matter，用于设置文章属性：

```yaml
---
title: 我的第一篇文章
date: 2026-01-01 10:00:00
tags:
  - 标签1
  - 标签2
categories: 分类名称
cover: /images/cover.jpg    # 文章封面图（可选）
description: 文章描述（SEO用）
---
正文内容...
```

### 文章内引用资源

在 Markdown 中引用图片：

```markdown
<!-- 引用 source/images/ 目录下的图片 -->
![图片描述](/images/example.jpg)

<!-- 引用文章同目录下的图片 -->
![图片描述](./example.jpg)
```

引用音乐（见第四章）。

### 开启草稿模式

草稿文件放在 `source/_drafts/` 目录下，不会发布到网站：

```bash
npx hexo new draft "草稿标题"
```

预览草稿时使用：

```bash
npx hexo server --draft
```

---

## 4. 音乐播放器

本博客使用 APlayer 作为全局音乐播放器。

### 音乐文件存放位置

将 mp3 文件放入 `source/music/` 目录。

### 配置文件

编辑 `_config.redefine.yml` 中的 `plugins.aplayer.audios` 部分：

```yaml
plugins:
  aplayer:
    enable: true                    # 开启播放器
    type: fixed                     # fixed=固定底部 / mini=迷你模式
    audios:
      - name: 歌曲名                 # 必填
        artist: 歌手名               # 必填
        url: /music/文件名.mp3       # 必填，路径相对于 source/
        cover: /music/封面.jpg       # 封面图（可选）
        lrc:                         # 歌词文件（可选，留空即可）
      - name: 另一首歌
        artist: 歌手
        url: /music/另一首.mp3
        cover: /music/封面.jpg
        lrc:
```

### 注意事项

- 文件名中不要包含空格或特殊字符，建议格式：`歌手 - 歌名.mp3`
- 封面图放在 `source/music/` 目录，文件名随意
- 每次添加歌曲后需要执行 `npx hexo clean` 清除缓存

---

## 5. 主题配置

主题的所有配置集中在 `_config.redefine.yml` 文件中，各部分说明：

| 配置项 | 说明 | 文档链接 |
|--------|------|----------|
| `info` | 站点基本信息（标题、作者、URL） | [文档](https://redefine-docs.ohevan.com/basic/info) |
| `defaults` | avicon、Logo、头像 | [文档](https://redefine-docs.ohevan.com/basic/defaults) |
| `colors` | 主题颜色配置 | [文档](https://redefine-docs.ohevan.com/basic/colors) |
| `home_banner` | 首页大图横幅 | [文档](https://redefine-docs.ohevan.com/home/home_banner) |
| `navbar` | 导航栏配置 | [文档](https://redefine-docs.ohevan.com/home/navbar) |
| `home` | 首页文章列表设置 | [文档](https://redefine-docs.ohevan.com/home/home) |
| `articles` | 文章页样式 | [文档](https://redefine-docs.ohevan.com/posts/articles) |
| `comment` | 评论系统（Waline/Gitalk等） | [文档](https://redefine-docs.ohevan.com/posts/comment) |
| `footer` | 页脚信息 | [文档](https://redefine-docs.ohevan.com/footer) |
| `plugins` | 插件配置（音乐/Mermaid等） | [文档](https://redefine-docs.ohevan.com/plugins) |

### 修改主题后生效

每次修改 `_config.redefine.yml` 后都需要执行：

```bash
npx hexo clean && npx hexo server
```

---

## 6. 部署上线

### 完整部署流程

```bash
# 1. 清理旧文件
npx hexo clean

# 2. 生成静态网站
npx hexo generate

# 3. 部署到 GitHub Pages
npx hexo deploy
```

### 查看部署配置

在 `_config.yml` 中已配置：

```yaml
deploy:
  type: git
  repo: https://github.com/wfh168/wfh168.github.io.git
  branch: gh-pages
  message: "Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}"
```

### 部署后访问

网站会自动在 `https://wfh168.github.io` 上线，通常需要等待 1-2 分钟。

---

## 7. 常见问题

### Q1: 启动时报 `Script load failed`

Hexo 会自动加载 `scripts/` 目录下的 `.js`、`.json` 等文件作为插件。如果该目录存在非插件文件（如 `.ps1`、`.py`），会导致报错。

**解决方法**：把非插件脚本移到 `scripts/` 目录外，比如 `tools/` 目录。

### Q2: 修改配置后页面没变化

Hexo 会缓存配置，需要执行：

```bash
npx hexo clean
npx hexo server
```

### Q3: 文章不显示

检查 Front-matter 中的 `date` 字段是否为未来时间，Hexo 默认不显示未来发布的文章。

### Q4: 图片不显示

- 图片必须放在 `source/` 目录或其子目录下
- 引用路径相对于 `source/` 目录
- 例如：图片 `source/images/cover.jpg` 的引用路径是 `/images/cover.jpg`

### Q5: 部署失败

检查网络连接和 GitHub 认证是否有效：

```bash
# 测试 GitHub 连接
git ls-remote https://github.com/wfh168/wfh168.github.io.git
```

### Q6: 音乐无法播放

- 确认 mp3 文件放在 `source/music/` 目录下
- 检查 `_config.redefine.yml` 中的 `url` 路径是否正确
- 文件名不要包含中文或空格，或确保 URL 编码正确

---

## 附录：常用工具

| 工具 | 用途 | 安装命令 |
|------|------|----------|
| hexo-generator-searchdb | 本地搜索功能 | 已安装 |
| hexo-wordcount | 文章字数统计 | 需另行安装 |
| hexo-deployer-git | Git 部署插件 | 已安装 |

---

*文档更新时间：2026-04-25*
