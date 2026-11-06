---
title: Obsidian 入门53：Get 笔记还有另一种同步方式，让 AI 帮你读、帮你整理
date: 2026-05-25
slug: getnote-ai-read
excerpt: 插件负责同步，AI 负责整理。Get 笔记的另一条路，让 AI 帮你读、帮你整理。
cover: Wechat/published/img/cover-combined.jpg
tags:
  - Web剪藏
  - Obsidian
  - 知识管理
  - MCP
  - 提示词工程
  - AI模型
  - 效率工具
status: published
---

[入门52](/blog/Obsidian%20%E5%85%A5%E9%97%A852%EF%BC%9A%E7%94%A8%20Get%20%E7%AC%94%E8%AE%B0%E3%80%8C%E5%8F%AA%E7%AE%A1%E8%AE%B0%E5%BD%95%E3%80%8D%EF%BC%8C%E7%84%B6%E5%90%8E%E7%94%A8%20Obsidian%20%E7%9C%9F%E6%AD%A3%E7%94%A8%E8%B5%B7%E6%9D%A5)写了 get-to-obsidian 插件之后，有群友说了一句话让我重新思考这件事。

他说"让 AI 直接去读你的 Get笔记，整理完放到 Obsidian 不就好了？"

我认真想了一下，发现它代表了一种完全不同的思路。插件是让工具替你做苦力活；AI 路线是让工具替你做思考。**这两件事，其实你都需要。**

当然，前提是你得先有 AI 能力。这个能力从哪来，Obsidian AI 插件（[入门31](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D)/[入门32](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)/[入门33](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)介绍过），或者本地 AI 工具（Claude Code 等）。

有哪个用哪个，这条路才走得通。

这篇不重复插件怎么装，只讲怎么用这些 AI 能力去读 Get笔记。

---

## 两条路的本质区别

先说清楚一件事：这两条路解决的是不同问题。

**插件路线**是备份思维。你在 Get笔记里存了什么，Obsidian 里就有什么。原文同步，不丢东西，偶尔翻看很方便。但说到底，你还是在「另一个地方存了一份」，并没有解决「从来没看」这个问题。

**AI 路线**是加工思维。你告诉 AI：「去读一下我最近存的那些关于产品思维的笔记，帮我整理成条目，写到 Obsidian 里去。」AI 读原文、理解内容、提炼重点、写成你想要的格式，最后落到 Obsidian 的某个文件夹下。

核心差异就一句话：**插件是同步，AI 是整理。**

![Project_Get笔记AI同步Obsidian-illustration-01.jpg](/images/posts/Obsidian%20%E5%85%A5%E9%97%A853%EF%BC%9AGet%20%E7%AC%94%E8%AE%B0%E8%BF%98%E6%9C%89%E5%8F%A6%E4%B8%80%E7%A7%8D%E5%90%8C%E6%AD%A5%E6%96%B9%E5%BC%8F%EF%BC%8C%E8%AE%A9%20AI%20%E5%B8%AE%E4%BD%A0%E8%AF%BB%E3%80%81%E5%B8%AE%E4%BD%A0%E6%95%B4%E7%90%86/Project_Get%25E7%25AC%2594%25E8%25AE%25B0AI%25E5%2590%258C%25E6%25AD%25A5Obsidian-illustration-01.webp)

这两件事，你可能都需要。

当然，两者可以并存。你用插件做备份，用 AI 做整理，让两种方式互相补充。

---

## 前提：你得有 AI 能力

这条路的入口是：你得先有调用 AI 的能力。方向有两个，

**Obsidian AI 插件**（[入门31](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D)/[入门32](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)/[入门33](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)介绍过）适合不想折腾的用户，装上插件，Obsidian 就能直接跑 AI。

**本地 AI 工具**（Claude Code、Cursor 等）适合习惯用终端或者 IDE的人。

有哪个用哪个。

---

## Get笔记的 Skill / MCP / CLI 生态

在说怎么用 AI 读 Get笔记之前，先了解一下目前能找到的三套工具：

**Skill**（/iswalle/getnote）

这是最面向普通用户的入口。装上之后，直接用自然语言指令控制 Get笔记，比如「保存这条笔记」「搜索某内容」「列出我的知识库」。指令体系清晰，Save/Search/List/KB/Tag/Config 六条路由覆盖主要操作。装上就能用，不需要懂 API。

安装方式，将下面的命令发给你的 AI agent（Claude code或者 Codex）：

```
帮我安装这个 get 笔记 skill，项目地址是：https://github.com/iswalle/getnote-openclaw。安装好后，教我怎么使用，最好按照由浅入深的步骤。
```

**MCP Server**（getnote-mcp，GitHub: iswalle/getnote-mcp，⭐64）

MCP 是 Model Context Protocol 的缩写，简单说就是让 AI 模型能直接调用工具的标准接口。这个 MCP Server 暴露了 30 多个工具，覆盖 Get笔记的几乎所有功能。如果你在用一个支持 MCP 的 AI 客户端（Claude Code、Cursor 等），接上这个就能让 AI 真正「操控」你的 Get笔记。

**CLI**（getnote-cli，GitHub: iswalle/getnote-cli，⭐82）

本地终端工具，包含 5 个子 Skill：认证、知识库、笔记操作、搜索、标签。适合喜欢在终端操作、或者想把 Get笔记能力整合到自己脚本里的用户。

三者的关系：**Skill 依赖 MCP，MCP 调用官方 API，CLI 是独立出口。** 对普通用户来说，从 Skill 开始就够了。

普通用户，从 Skill 开始就够了。

别想太多，先跑起来。

---

## 实战演示：让 AI 整理你的 Get笔记

说了这么多，来点实际的。以下是完整操作步骤，以 MCP 为例（Skill 的操作逻辑类似，只是封装层次不同）。

**第一步：配置 MCP，连接 Get笔记 API**

你需要两个东西：API Key 和 Client ID，来源是 Get笔记开放平台（biji.com/openapi）。

在支持 MCP 的 AI 客户端里，配置文件大概长这样（当然你不用手动配置，把项目地址发给 AI，让你的 AI 帮你配置就好）：

```json
{
  "mcpServers": {
    "getnote": {
      "command": "npx",
      "args": ["-y", "@getnote/mcp"],
      "env": {
        "GETNOTE_API_KEY": "你的API Key",
        "GETNOTE_CLIENT_ID": "你的Client ID"
      }
    }
  }
}
```

配置完，AI 就有了「读你 Get笔记」的能力。

我第一次配的时候，用的是 Claude Code，接上 MCP 之后第一件事就是让 AI 搜了一下我存了哪些内容。结果吓了一跳。半年前存的一些零碎想法还在，都快忘了。

**第二步：告诉 AI 去读什么**

比如你有一堆录音转写的笔记，主题散乱，从来没整理过。你可以这样问 AI：

> 「去搜一下我最近存的关于'产品方法论'的笔记，列出标题和摘要。」

![让 AI 读一遍](/images/posts/Obsidian%20%E5%85%A5%E9%97%A853%EF%BC%9AGet%20%E7%AC%94%E8%AE%B0%E8%BF%98%E6%9C%89%E5%8F%A6%E4%B8%80%E7%A7%8D%E5%90%8C%E6%AD%A5%E6%96%B9%E5%BC%8F%EF%BC%8C%E8%AE%A9%20AI%20%E5%B8%AE%E4%BD%A0%E8%AF%BB%E3%80%81%E5%B8%AE%E4%BD%A0%E6%95%B4%E7%90%86/Project_Get%25E7%25AC%2594%25E8%25AE%25B0AI%25E5%2590%258C%25E6%25AD%25A5Obsidian_illustration-02_73873f3d_20260525.webp)

AI 调用 Get笔记的搜索工具，返回结果。你从中挑出想整理的那几篇。

我一开始搜"产品"，出来40多条，根本没法看。后来学会加限定词，用"产品 方法论 最近一周"，一下就精准了。

**第三步：AI 读内容，整理成结构化条目**

继续：

> 「读一下这几篇笔记，帮我提炼核心观点，写成 Obsidian 格式的条目，包括：来源、日期、核心观点、我的批注。输出 Markdown。」

AI 调用笔记读取工具，逐篇读内容，按你要求的格式整理输出。

**第四步：写入 Obsidian**

得到整理好的 Markdown 后，你可以手动粘到 Obsidian 对应的文件夹，也可以让 AI 直接写文件。写完之后，Obsidian 里就是结构化的知识条目，而不是一堆散乱的原文链接。

我让 AI 整理完会自己过一遍，是因为 AI 偶尔会有漏字，或者某个词翻译得不准确。检查一遍比直接用放心。

整个过程，从「搜什么」到「读什么」到「整理成什么格式」，都是由你驱动 AI 完成。你在控制读哪篇、怎么整理，AI 在做苦力活。

---

## 插件和 AI 路线，怎么选？

**插件适合：** 只想原文备份，不追求深度整理；使用场景偏「偶尔翻翻」，不需要 AI 参与；手动整理习惯了，AI 整理反而不习惯。

**AI 路线适合：** 想让笔记真正变成可检索、可关联的知识；存量大，想系统梳理但一直没时间；愿意花一次时间搭好工具链，之后省力。

![Project_Get笔记AI同步Obsidian-illustration-03.jpg](/images/posts/Obsidian%20%E5%85%A5%E9%97%A853%EF%BC%9AGet%20%E7%AC%94%E8%AE%B0%E8%BF%98%E6%9C%89%E5%8F%A6%E4%B8%80%E7%A7%8D%E5%90%8C%E6%AD%A5%E6%96%B9%E5%BC%8F%EF%BC%8C%E8%AE%A9%20AI%20%E5%B8%AE%E4%BD%A0%E8%AF%BB%E3%80%81%E5%B8%AE%E4%BD%A0%E6%95%B4%E7%90%86/Project_Get%25E7%25AC%2594%25E8%25AE%25B0AI%25E5%2590%258C%25E6%25AD%25A5Obsidian-illustration-03.webp)

如果你选了 AI 路线，Get笔记 + Skill/MCP + Obsidian，这条链子搭好之后，「让 AI 读一遍我最近存了什么」这件事，大概两三分钟就能跑完。

也可以两条路同时用，没人规定只能选一个。

---

## 工具链完整了

回顾一下整个系列：入门50讲微信读书笔记怎么进 Obsidian，入门52讲 Get笔记怎么通过插件同步，这篇讲怎么用 AI 去读、去整理。

**存（Get笔记）→ 同步（插件）→ 读+整理（AI）**

工具本身不是答案。

定时去理，才是。
