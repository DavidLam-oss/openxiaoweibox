---
title: "Obsidian 入门72：在 Obsidian 里用 DeepSeek 的四种姿势"
date: "2026-07-15"
slug: "obsidian-72-deepseek-four-postures"
excerpt: "关于 DeepSeek，在 Obsidian 里到底怎么接进去？四种姿势，选一个适合你的。"
tags:
  - AI模型
  - Obsidian
  - 自动化
  - 效率工具
  - Obsidian入门
  - 终端命令行
  - Obsidian插件
  - AI Agent
status: published
---
> 本文是「Obsidian x AI」系列第 72 篇。入门 54 写了 DeepSeek 接入的概览，入门 55 写了 CC Switch 配置，入门 31/32/33 把三个侧栏插件拆清楚了。如果你都看过，这篇正好把它们串起来。

关于 DeepSeek，我问过不少人，自己也试过好几条路。发现大部分人用 Obsidian 的人，在困惑的是在 Obsidian 里到底**怎么接进去**。

![在 Obsidian 里用 DeepSeek 的四种姿势示意图](/images/posts/20260715223601925.webp)


这个坑我在[入门 54](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A) 里拆过一次。把「油、车、转换器」的比喻讲清楚，模型是油，工具是车，中间可能需要一个转换器才能对上号。

但入门 54 之后，后台一直有人在问同一个问题：**你说了这么多工具，我到底用哪个？**

这个问题我回答过好几次。但每次回答的版本都不太一样。因为我自己也在换。

---

## 先说我现在怎么用

我的日常用下来，其实就两套东西。

在电脑前面的时候，我现在几乎全部走 **Reasonix + DeepSeek**。公众号的 WeChat Writer Skill、调一个 Skill、处理素材：全是用这个组合。

Reasonix 针对 DeepSeek 做了缓存优化，大部分时候缓存命中率在 95% 以上，有时候能到 100%。这意味着同样的提问，第二次几乎不花钱。

但在手机上面，这是另一套玩法。临时有事的时候，我会直接用 **Hermes Agent + Minimax M3**。原因很简单：手机上我不太可能用终端去敲命令，Hermes 有个聊天界面，发条消息就行。

我自己的路径是一路走过来的：**CC Switch → Reasonix CLI → Reasonix GUI**，再加上手机一个独立场景。

下面把这四种方式摊开来说。你可以对照着看一下，自己现在在哪个位置。

---

## 姿势一：CC Switch + 你顺手的工具

这是最通用的路子。

[CC Switch](/blog/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5) 是一个转换器，它能把各种模型接到各种工具上。你装上它，配好 DeepSeek 的 API Key，然后在你习惯的工具（Claude Code、Codex、Gemini CLI 等等）里面拉 CC Switch 的模型就行。

![CC Switch 转换器配置界面](/images/posts/CleanShot%202026-07-15%20at%2022.26.30%402x.webp)


这条路的好处是**灵活**。CC Switch 支持 6 个工具 + 50 多个模型供应商，你换工具不换配置，换模型不换工具。

坏处是**绕一道**。你是通过转换器去调模型的，多了一层。如果你只是想要 DeepSeek 的极致缓存优化，CC Switch 帮不了你。缓存是 Reasonix 那边的能力。

**适合谁**：已经用着某个工具、只想把模型换成 DeepSeek 的人。[入门 31](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D) 到 [33](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98) 讲的那三个插件，都能这样接。

---

## 姿势二/三：OB 侧栏的三个插件，选一个

之前的 [入门 54](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A) 用「车」来比喻工具。如果继续这个比喻，那这三个侧栏插件就像是**不同款的鞋**。都能跑步，但脚感完全不同。

![Obsidian 侧栏三插件 Terminal Claudian Agent Client](/images/posts/20260715223639558.webp)


**Terminal 插件**（[入门 31](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D)）像硬核跑鞋。自由度最高，你得自己贴路径进去。我现在就是用这个，因为对我来说贴个路径不是问题，而且它就在 OB 侧栏里，不离开 Obsidian 界面。

**Claudian 插件**（[入门 32](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)）像懒人跑鞋。界面优雅，开箱即用。它会自动从你的库根目录读取上下文，你当前在看哪篇笔记，它就把那篇作为上下文传进去。Windows 用户偶尔会遇到小坑，但大部分时候很丝滑。

**Agent Client 插件**（[入门 33](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)）像万能跑鞋。支持 ACP 协议，什么工具都能接进来。如果你同时用多个 AI 工具，它是最省心的那一个。

这三个插件有一个共同的优势：**不离开 Obsidian**。你的笔记、你的侧栏、你的 AI 对话，都在同一个软件里。你不需要切窗口，不需要复制路径（Claudian/Agent Client 自动读上下文），非常适合写作和整理素材的场景。

不过它们的共同限制是：需要一套配置流程。你得装好 CC Switch，配好模型，再接上插件。如果你只是想快速试试 DeepSeek，这个门槛可能比你想象的高。

**适合谁**：已经在 Obsidian 里写作、不想切窗口的人。如果你已经装了其中一个插件，配好 CC Switch 就能直接用 DeepSeek。

---

## 姿势四：Reasonix 直连 DeepSeek

这是我现在的选择。

[之前写过](/blog/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F)，Reasonix 针对 DeepSeek 做了极致的缓存优化，缓存命中率 95-100%。同样的提问第二次几乎零成本，这个对于日常重度使用的人来说，账单差距肉眼可见。

Reasonix 有两个版本：

**CLI 版本**：`npm i -g reasonix` 或者 `brew install`，装完在终端里直接用。如果你想在 Obsidian 侧栏里用，可以用 Terminal 插件开一个面板跑它。我早期就是这么用的。因为 Reasonix CLI 的终端界面做得还是挺漂亮的，不是那种丑黑屏。

![Reasonix CLI 终端界面](/images/posts/CleanShot%202026-07-15%20at%2022.29.11%402x.webp)


**桌面 GUI 客户端**：后来 Reasonix 出了独立的 APP，我就切过去了。原因很简单。CLI 黑终端对于大部分人来说，心理障碍太大了。你看 Codex，两天时间从600万到 800 万用户，为什么？因为它是图形界面，打开就能用，不用面对黑屏幕敲命令。人类天生喜欢图形化的东西，这没什么好否认的。

![Reasonix 桌面 GUI 客户端界面](/images/posts/CleanShot%202026-07-15%20at%2022.29.49%402x.webp)


GUI 版本的好处是你能直观地看到：当前缓存命中率是多少、这一轮对话花了多少钱、Context 还剩多少、账户还有多少余额。这些信息在终端里也能看到，但扫一眼就有的体验，跟敲命令去看，是完全不同的。

![Reasonix GUI 缓存命中与费用面板](/images/posts/20260715223721994.webp)


另外说一下我自己的使用习惯：AI 写长内容的时候，我其实不看过程中的输出。

比如 WeChat Writer Skill 跑一篇文章，出的策划案和初稿我是不看的，我只等最终精校过的版本，然后在那个版本上去 review 和修改。所以我也没必要一直停留在 Obsidian 的侧栏里去盯过程。GUI 版本开在另一个窗口，跑完了回来看，对我来说更自然。

**适合谁**：重度使用 DeepSeek、在意缓存成本和账单的人。以及不习惯终端、想要图形界面的朋友。

---

## 选哪个？

如果你已经在用 Terminal / Claudian / Agent Client 中的一个，配好 CC Switch，先让它跑起来。不要在「选工具」上花太多时间。

如果你还没开始、想要一个省心的起点，Reasonix 桌面 GUI 是最直的路。装好就能用 DeepSeek，不用折腾转换器和插件配置。

如果你偶尔在手机上也需要，关注[笔记同步助手](/blog/Obsidian%20%E5%85%A5%E9%97%A856%EF%BC%9A%E4%BB%8E%E5%BE%AE%E4%BF%A1%E5%88%B0%20Obsidian%EF%BC%8C%E4%B8%80%E7%AF%87%E6%96%87%E7%AB%A0%E8%A3%85%E5%A5%BD%E3%80%8C%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%8A%A9%E6%89%8B%E3%80%8D)那套方案，或者像我一样配一个 Hermes Agent + 轻量模型处理临时需求。

**没有最好的姿势，只有最适合你当前阶段的那一个。**

---

## 写在最后

四条路都摊开了。你不需要全部学会，也不需要一开始就选对。先找一条自己最顺手的，用起来再说。

好了，下一篇见。

---

## 进阶阅读

### 本系列前篇
- [Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A) — DeepSeek 接入概览，油车转换器比喻
- [Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来](/blog/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5) — CC Switch 配置步骤
- [Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵”](/blog/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D) — Terminal 插件详解
- [Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6) — Claudian 插件详解
- [Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98) — Agent Client 插件详解

### 工具参考
- [我是怎么做到用 DeepSeek 达到 100% 缓存命中率的？](/blog/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F) — Reasonix 缓存机制实测
