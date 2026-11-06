---
title: Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚
date: 2026-05-27
slug: obsidian-ai-tools-chain
excerpt: 装了插件不等于能用 AI。这篇文章把模型、入口工具、插件三层关系串成一条完整的线。
cover: ""
tags:
  - Obsidian
  - AI模型
  - Claude Code
  - Codex
  - 自动化
  - 终端命令行
  - Obsidian插件
  - AI Agent
  - Obsidian入门
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理和收集、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过上一篇，可以先看 [Obsidian 入门53：Get 笔记还有另一种同步方式，让 AI 帮你读、帮你整理](/blog/Obsidian%20%E5%85%A5%E9%97%A853%EF%BC%9AGet%20%E7%AC%94%E8%AE%B0%E8%BF%98%E6%9C%89%E5%8F%A6%E4%B8%80%E7%A7%8D%E5%90%8C%E6%AD%A5%E6%96%B9%E5%BC%8F%EF%BC%8C%E8%AE%A9%20AI%20%E5%B8%AE%E4%BD%A0%E8%AF%BB%E3%80%81%E5%B8%AE%E4%BD%A0%E6%95%B4%E7%90%86)。

---

群里有个经典问题，这个问题我遇到过的次数，手指头都不够数：

「我装了 Terminal 插件/Claudian 插件/Agent Client 插件，是不是就可以用 AI 了？」

紧接着的下一个问题：

「装了之后，DeepSeek 怎么接进来？」

这两个问题看起来很简单，但背后其实藏着很多人一直没有真正分清楚的三件事：

- AI 模型是什么
- 入口工具是什么
- Obsidian 插件又是什么。

它们不是同一层的东西，它们之间的关系也不是「装了就能用」这么直接。

这篇文章，我想把它们串成一条完整的线。以后你再遇到任何新的 AI 工具，也能用它判断出：这个工具在这个体系里，属于哪一层。

## 模型是油，入口工具是车

先说第一个容易混的概念：模型和入口工具，不是一回事。

大多数人对 AI 的认知停留在对话框。

你打开一个窗口，打字，它回答，你知道它是谁，它不知道你是谁，更不会碰你的文件。

这类 AI 是云端运行的对话机器，你借它一个脑子，它给你一些答案，仅此而已。

但 Claude Code 和 Codex 这类工具不一样。它们是「能直接操作你本地文件」的 AI：装在你电脑里，能读文件、改文档、跑命令、帮你干活的真实劳动力。

这两个东西放在一起，很像油和车的关系。

模型是油。你烧的油决定了能量从哪里来、品质怎么样。

![Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚 - 配图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A/20260527225620648.webp)

DeepSeek 是 92 号油，价格便宜，够用。Claude 或者chatGPT 是 95 号油，品质更好一点，但成本也高。各个模型厂商把油炼好，你去选加哪种。

入口工具是车。各车厂造出来的车，用什么油是可选的，但车本身是另一家造的。Claude Code 是 Anthropic 造的车。Codex 是 OpenAI 造的车。你可以把国产油的管子接进去，但车还是那辆车。

这就是为什么「装了插件不等于能用 AI」。插件只是插件，它是一条连接工作间的通道。

Obsidian 是工作间，插件是工作间的门。门装了，通道铺好了，还得有车开进来才能干活。而那辆车，是 Claude Code 或 Codex，不是插件。

关于模型和 Claude code 以及 Codex等工具的关系，在[Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)已经有了很形象的介绍。

这一篇主要补的是 Obsidian（工作间） 以及插件（门），与这些模型（油）、 入口工具 Claude code/Codex （车）的关系。

## 国产油怎么加：CC Switch

说到国产油，就不能不提 CC Switch。

国产模型便宜，但有一个现实问题：不是车都能直接加国产油。Claude Code 跑在 Anthropic 的框架里，默认只认自家的油。你想把 DeepSeek 或 GLM 的油加进去，油路不对，因为是接口不兼容。

CC Switch 就是解决这个问题的东西。它把你的 Claude Code 和国产模型之间的协议打通，让车能加到国产油。

![Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚 - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A/20260527225656350.webp)

相当于在中间加了一个转换器，它的具体配置，这篇文章不展开，下一篇可以具体来讲讲（其实之前也在[Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)简单介绍过）。

你只需要知道一点：CC Switch 是让车能加到国产油的那一环。没有它，要么只能用进口油（贵），要么车根本跑不起来（国产模型接不进去）。

## 三款插件，三条进 Obsidian 的路

油有了，车有了，转换器也有了。它们住在哪里？

Claude Code 这类工具，平时住在你电脑的终端里，是一个独立的运行空间。Obsidian 是另一个空间。

你在 Obsidian 里写笔记，突然想让它帮你整理一段话，或者让它根据你的素材生成一篇文章。这个需求发生在 Obsidian 里，但干活的能力在终端里。

怎么把终端里的「劳动力」叫到 Obsidian 里来上班？

> 别看到“终端”这个字眼就被吓到了，其实把它当做一个工具就好。

三个插件，提供了三条不同的路。

![Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚 - 配图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A/20260527225736747.webp)

Terminal 插件。这个最直接，也最硬核。你在 Obsidian 里打开一个 Terminal 窗口，自己把 Claude Code 叫进来，自己输入指令，它帮你干活。你要有基本的命令行基础，知道自己在做什么。自由度最高，但你得自己开那辆车。

Claudian 不一样。你不用开 Terminal，Claudian 像一个穿好西装的管家，帮你把车停好、把门打开。你在 Obsidian 里触发一个指令，管家替你完成调度。基本不需要懂技术，但代价是你得信任这个管家的判断（在 Windows 上，有时候会有些奇怪的问题）。

Agent Client 是第三个选择。它像建了一个通用的调度台，什么牌子的车都能停进来，不只是 Claude Code / Codex，国产模型的车也行，Opencode、Gemini CLI 也行。多工具并行的时候最顺手，代价是配置起来稍微复杂一点。

这三条路的详细介绍和具体配置步骤，分别在入门系列的第 31、32、33 篇里。这里不再展开。

## 把链条串起来

现在把完整的链条串起来，就是这个样子。

你在 Obsidian 里触发一个需求，插件把请求转给 Claude Code 或 Codex，CC Switch 把国产模型的油送进去，AI 操作本地文件，结果返回 Obsidian。

![Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚 - 配图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A/20260527225758872.webp)

这是一个完整的工作流。油、车、转换器、工作间、通道，每一环都缺一不可。

插件不是 AI，插件是通道。车得先进来才能干活。

回到开头那个问题：装了插件是不是就可以用 AI 了？

现在你知道了答案：不能。插件只是把门打开，让车有路进来。车是你要另外准备的东西，没有车，门开着也是空的。

这个框架不只是为了理解这三个插件。是为了以后你遇到任何新的 AI 工具，能用它判断：这个工具在这个体系里，是油，是车，还是那条路。

---

## 进阶阅读

- [Obsidian 入门26：想让 AI 读你的 Obsidian？你需要先认识这几个工具](/blog/Obsidian%20%E5%85%A5%E9%97%A826%EF%BC%9A%E6%83%B3%E8%AE%A9%20AI%20%E8%AF%BB%E4%BD%A0%E7%9A%84%20Obsidian%EF%BC%9F%E4%BD%A0%E9%9C%80%E8%A6%81%E5%85%88%E8%AE%A4%E8%AF%86%E8%BF%99%E5%87%A0%E4%B8%AA%E5%B7%A5%E5%85%B7)
- [Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵”](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D)
- [Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)
- [Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)
- [Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)
- [Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)
