---
title: "我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？"
date: "2026-06-16"
slug: "reasonix-cache-hit-rate"
excerpt: "从 ChatGPT 试到 DeepSeek，从 CC Switch 套壳用到 Reasonix 原生。缓存命中率 95%+，成本控制是真的省。"
tags:
  - 自动化
  - AI模型
  - AI Agent
  - 内容创作
  - 开源
status: published
---
如果你一直在关注我们这个 [David 写作天团](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0)的工作流，应该记得我们试过不少模型。

ChatGPT、MiniMax，都有拿来配合写作 Skill 跑过。
- ChatGPT 总是有些车轱辘话在来回说，而且很爱说稳稳地接住你。
- Minimax 对指令遵循度不太好。跟他说了不要破折号，还总是会用破折号。

后来换到 DeepSeek，效果好很多。中文理解到位，指令跟得紧，配合我们那套写作 Skill 用起来很舒服。

那会儿是用 Claude Code 加 CC Switch，把 DeepSeek 的模型配置进去用的。

后来发现了 **Reasonix**。

![我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？ - 截图 1](/images/posts/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F/CleanShot%25202026-06-17%2520at%252008.26.30.webp)

一个 DeepSeek 原生的 AI coding agent，GitHub 上 22.7k stars。不用套壳，直接原生跑 DeepSeek，缓存优化也是专门围绕 DeepSeek 的前缀缓存做的。因为这个 Agent 只支持 DeepSeek 模型。

用了挺长一段时间，整体感觉很务实+很省钱。

## 先说说最让我意外的一点：省钱

DeepSeek 的 API 价格本身就很便宜了，但用 AI agent 的人都知道，真正的成本不在单次调用，在长会话。一聊就是几十上百轮，token 累积起来，再便宜的模型也能跑到让你肉疼。

Reasonix 解决这个问题的方式很直接。它围绕 DeepSeek 的前缀缓存做了极致优化。

GitHub 上的介绍写的是「围绕 DeepSeek 的前缀缓存调优，长会话也能把 token 成本压低」。我实际用下来的感受是，大部分会话的缓存命中率都在 95% 以上，有时候甚至能到 100%。这意味着什么？意味着你聊了半天，大部分 token 其实不计费。

这不是理论上的「设计上支持缓存」，而是实打实地省了钱。

## 后来我试了另一个很火的

我直接开始用 Reasonix 的，用了挺长一段时间。

后来刷 GitHub 的时候注意到另一个项目，Star 数量比 Reasonix 高不少，当时还叫 DeepSeek TUI，后来改名叫 CodeWhale。很多人推荐，社交媒体上讨论度也很高。

![我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？ - 配图 2](/images/posts/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F/20260617083057793.webp)


我就下载了它的终端版试了一下。

怎么说呢。功能确实不少，界面也确实好看，花里胡哨的好看。但实际用起来，总觉得差了点意思。不是功能不够，而是整个体验有一种「为了做而做」的感觉。可能是我个人偏好，我更喜欢 Reasonix 那种「工具就是工具」的务实感。

说到底，工具是拿来干活的，不是拿来好看的。试了一圈，还是回到了 Reasonix。

## 几个真正打动我的点

Reasonix 有几个点是我觉得真正打动我的。

第一个是**缓存优化不是噱头**。前面说了，95%+ 的命中率是实打实的。我现在主要是用它来写文章，一聊就是大半天，月底看 API 账单，比预期的低很多。

第二个是**自动模式**。Reasonix 会根据任务的难易程度自动切换模型，大部分任务走 V4 Flash，只有在遇到需要更多推理能力的复杂任务时，才自动切到 V4 Pro。你自己不用纠结「这次该用哪个模型」，它帮你选了。DeepSeek V4 Flash 本身就很便宜了，再加上缓存命中率高，成本控制得极其好。

第三个是它**现在不只是终端了**。macOS 和 Windows 都有了桌面客户端，GUI 界面，操作比终端直观很多。不是每个人都能习惯在黑框里打字跟 AI 对话的，有了桌面端，门槛低了不少。

![我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？ - 截图 3](/images/posts/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F/CleanShot%25202026-06-17%2520at%252008.32.21.webp)


第四个是该有的东西基本都有了，**MCP 支持**、**Skill 支持**（可以复用工作流，跟我们在 Obsidian 里用的 Skill 是同一个概念）。

**IM 控制**（可以通过微信、QQ、飞书来控制 agent，出门在外手机也能操作）。当然前提是一样的，电脑要保持开机。

这一点跟之前聊过的 Hermes agent 和 OpenClaw 一样，不是短板，是这类工具的共性。

## 适合谁，不适合谁

如果你已经在用 DeepSeek，或者正在找一个适合长会话的 AI agent 客户端，Reasonix 值得试一试。

安装很简单，一行命令：

```bash
npm i -g reasonix
```

或者 macOS 用户。

```bash
brew install esengine/reasonix/reasonix
```

把 API Key 填进去就能用了。GitHub 上 22.7k stars，社区活跃，文档齐全。

如果你不想使用终端，想像我一样使用客户端，可以通过下方的地址去 Github release 页面下载适合你的系统的版本(当前最新版本是1.8.1）。

项目地址：
https://github.com/esengine/DeepSeek-Reasonix/releases/tag/desktop-v1.8.1

![我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？ - 截图 4](/images/posts/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F/CleanShot%25202026-06-17%2520at%252008.45.37.webp)

当然，它也不是适合所有人。如果你完全不想碰配置文件、不想了解什么是 MCP 和 Skill，那可能 Claude 或 ChatGPT 的官方客户端更适合你。

Reasonix 的灵活性和可配置性，恰好也是它的门槛。

但如果你愿意花十分钟配置一下，换来的是长期的 token 成本节省和工作流自定义的自由。我觉得这十分钟花得很值。
