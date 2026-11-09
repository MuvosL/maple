# Maple's Notes

> 一个基于 Quartz v4 的个人数字花园，用于记录学习、实践与复盘。

在线访问：[muvosl.github.io/maple](https://muvosl.github.io/maple)

## 技术栈

- **Quartz v4**：静态站点生成，提供双链、反向链接、图谱、搜索与标签等数字花园能力。
- **Markdown / Obsidian**：笔记以 Obsidian 风格的 Markdown 编写，支持 `[[wikilinks]]` 与 callout。
- **GitHub Actions + GitHub Pages**：推送到 `main` 后自动构建并部署。

## 本地运行

要求：Node.js 22+ 与 npm 10.9+。

```bash
npm install
npx quartz build --serve
```

启动本地预览服务后即可访问；笔记位于 [`content/`](content/)，站点配置位于 [`quartz.config.ts`](quartz.config.ts)，布局配置位于 [`quartz.layout.ts`](quartz.layout.ts)。

## 目录结构

```text
content/          笔记内容
quartz/           主题、组件与插件
quartz.config.ts  站点配置
quartz.layout.ts  页面布局
public/           构建输出（自动生成）
```

## 写作

在 `content/` 下新建 Markdown 文件即可。一篇笔记的最小 frontmatter：

```yaml
---
title: "标题"
date: 2026-01-01
tags: [标签]
---
```

## 致谢

本项目使用 [Quartz](https://github.com/jackyzha0/quartz) 构建。感谢 jackyzha0 与 Quartz 社区提供轻量、开放的数字花园发布能力。
