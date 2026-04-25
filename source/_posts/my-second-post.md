---
title: 我的第二篇文章
date: 2026-04-25 17:10:00
updated: 2026-04-25 17:10:00
categories:
  - 技术
tags:
  - Hexo
  - 博客
cover: 
description: 这篇文章记录了我如何修复 GitHub Pages 部署问题，让博客成功上线。
keywords: 
abbrlink: 
password: 
top: 
mathjax: false
katex: false
comments: true
aside: true
---

## 前言

昨天在部署 Hexo 博客到 GitHub Pages 时，遇到了一个奇怪的问题：本地预览完全正常，但 GitHub Pages 上却一直显示旧内容。

## 问题排查

经过排查，发现问题出在 GitHub Pages 的构建源设置上。GitHub Pages 默认会尝试用 Jekyll 构建源码，但我们的 Hexo 博客根本不是用 Jekyll 构建的。

解决方案是让 GitHub Pages 直接从 `gh-pages` 分支读取静态文件，而不是从 `main` 分支构建。

## 关键步骤

1. 在 GitHub 仓库设置中，将 Pages 的 Source 改为 **Deploy from a branch**
2. 选择 `gh-pages` 分支作为部署源
3. 目录选择 `/ (root)`

这样 GitHub Pages 就会直接服务 Hexo 生成的静态文件，不再尝试用 Jekyll 构建。

## 总结

遇到 GitHub Pages 部署问题时，首先确认 CI 是否成功构建并推送到了 `gh-pages` 分支，然后再检查 GitHub Pages 的源设置是否正确。

希望这篇文章对你有帮助！
