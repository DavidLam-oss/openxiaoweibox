---
title: 在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖
date: "2026-01-11"
slug: gemini-cli-skills-free
excerpt: Claude Code 要付费，Gemini CLI 免费。我用软链接把 Skills 打通了——一次配置，永久同步。
tags:
  - AI模型
  - 效率工具
  - Obsidian
  - 编程开发
  - Obsidian入门
---

**Claude Code 的 Skills 要付费，Gemini CLI 的 Skills 免费。** 这个差距够我写一篇教程了。

上次分享过怎么在 Obsidian 里装 Gemini CLI，直接在编辑器里跟它对话，修文章、创建文件都行。

[保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian](/blog/%E4%BF%9D%E5%A7%86%E7%BA%A7%E6%95%99%E7%A8%8B%EF%BC%9A%E5%B0%86%20Gemini%20CLI%E5%92%8CClaude%20code%E9%9B%86%E6%88%90%E5%88%B0%20Obsidian)

最近 Gemini CLI 更新了 Preview 版本，支持 Skills 功能了。我就想：能不能把 Claude Code 的 Skills 拿过来直接用？

毕竟 Claude Code 里面，不管用 Claude 模型还是国产模型，都要付费。但 Gemini CLI 不一样，**免费用户每分钟 60 次请求，每天 1000 次**，足够日常折腾了。

说干就干。

## 安装 Gemini CLI 预览版

首先，安装最新的 Gemini CLI 预览版。

这一步需要准备 Node.js 环境。不懂也没关系，让 AI 帮你。打开你常用的 AI，发这段话给它：

```bash
我需要在我的电脑（Windows 或 Mac）上安装 Gemini CLI，请你教我一步一步怎么操作
```

AI 会一步一步教你。

如果环境已经准备好了，直接运行这条命令：

```bash
npm install -g @google/gemini-cli@preview
```

装过正式版的话，这条命令会自动更新到预览版。

装完之后，查一下版本：

```bash
gemini --version
```

看到 0.24 Preview 版本就对了。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 1](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111110916509.webp)

## 手动开启 Skills

在终端输入 `gemini` 启动。但 Skills 默认是关着的，需要手动打开。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 2](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111111244193.webp)

输入 `/settings`，搜索 `agent skills`，看到它是 `false`。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 3](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111111441852.webp)

选中它，按 Enter，变成 `true`。

按 ESC 退出设置。

输入 `skills` 确认一下，看到列表就说明生效了。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 4](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111111614676.webp)

## 把 Claude Code 的 Skills 搬过来

我在 Claude Code 里装了三个 Obsidian 相关的 Skills：

- json-canvas
- obsidian-bases
- obsidian-markdown

现在要把它们搬到 Gemini CLI 里。

两边的 Skills 存放路径：

- **Claude Code**：`~/.claude/skills/` 或项目目录下的 `.claude/skills/`
- **Gemini CLI**：`~/.gemini/skills/` 或项目目录下的 `.gemini/skills/`

最简单的方式是直接复制，但有个问题：以后 Skills 更新了，两边都要改，麻烦。

所以我想用软链接。一次链接，永久同步。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 5](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111112034644.webp)

我问 Gemini 能不能用软链接，它说可以，然后直接帮我创建了。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 6](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111112127706.webp)

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 7](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111112156619.webp)

你也可以直接把这段话发给 Gemini：

```bash
帮我查看当前的项目目录下是否存在 Claude Code Skills，如果有的话，通过软链接的方式放到 Gemini Skills 里面。
```

## 效果展示

三个 Skills 都通过软链接指向 Claude Code 了。

我让 Gemini 用 json-canvas 这个 Skill，把这篇文章生成一个画板。

![在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 白嫖 - 配图 8](/images/posts/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96/20260111112729821.webp)

**AI 就是遇强则强**。把 Skills 装上，它能做的事情就更多了。

你用 Gemini CLI 还做过什么有趣的事？欢迎留言分享。
